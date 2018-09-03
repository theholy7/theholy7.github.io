---
layout: post
title: Raising Custom Exceptions in Flask Restplus for wrong POST JSON payloads
excerpt_separator:  <!--more-->
categories:
  - Random Code
tags:
  - Flask
  - Flask Restplus
  - Python
  - API development
---
If you have checked my LinkedIn, you know I am a Data Engineer at [Cytora](https://www.cytora.com).
Part of my job is to work in our product, the API that serves our AI models to our clients.

Part of a good product is to be able to provide the users with a good experience while they use it,
or develop tools that interact with it. To do so, you need to be able to tell them exaclty what is going wrong.
A simple 400 Bad Request won't work, you need to be able produce custom error messages and codes.

However, what should be an easy task, isn't. <!--more-->[Flask-Restplus](https://github.com/noirbizarre/flask-restplus/) 
(or at least the fork we use internally) doesn't seem
to support raising custom Exceptions for JSON payloads that are sent to a POST endpoint. So how did we solve this problem?

Internally, when a request is made to an endpoint, the _dispatch\_request_ will handle it. Let's look at it:

```python
def dispatch_request(self, *args, **kwargs):
    # Taken from flask
    meth = getattr(self, request.method.lower(), None)
    if meth is None and request.method == 'HEAD':
        meth = getattr(self, 'get', None)
    assert meth is not None, 'Unimplemented method %r' % request.method

    for decorator in self.method_decorators:
        meth = decorator(meth)

    self.validate_payload(meth)

    resp = meth(*args, **kwargs)

    if isinstance(resp, BaseResponse):
        return resp

    representations = self.representations or {}

    mediatype = request.accept_mimetypes.best_match(representations, default=None)
    if mediatype in representations:
        data, code, headers = unpack(resp)
        resp = representations[mediatype](data, code, headers)
        resp.headers['Content-Type'] = mediatype
        return resp

    return resp
```

We can see that after some logic, the method _self.validate\_payload_ is called. By inspecting the code a bit more we can
understand that the method that needs to be overwritten is the _validate_ method that exists inside the _ModelBase_ class.
 Investigating this method shows that Flask-Restplus is internally using _jsonschema_ to validate the payloads being sent
 to an endpoint.

JSONschema is a very useful way of defining properties of a certain json object.

We want to leverage this to:
1. Prevent our payload of taking any extra fields
2. Prevent certain properties from taking unexpected types
  a. i.e. an _id_ key is a _string_ and not a _boolean_

So lets start!

First we define a new model that inherits from the Flask-Restplus model. 
To solve point _1._ in our list, we want to add the JSONschema property 
_"additionalProperties": false_ to the model's schema.

```python
from flask_restplus import Model
from jsonschema import Draft4Validator

class ValidationModel(Model):
    """
    Extend the Model class provided by flask-restplus so that we can add the
    additionalProperties key to the schema, thus preventing additional properties to
    be sent in the payload.
    """

    def __init__(self, *args, **kwargs):
        # pop strict, otherwise it will end up in __apidoc__ and things crash
        self.strict = kwargs.pop('strict', False)
        super().__init__(*args, **kwargs)

    @property
    def _schema(self):
        """
        Get the base schema from the parent class which handles all the logic
        to convert the fields into json schemas, and add `additionalProperties`
        to the schema of the current object, to prevent new properties
        from being passed in the payload.

        :returns dict: dictionary containing schema
        """
        base_schema = super()._schema

        if self.strict:
            base_schema['additionalProperties'] = False

        return base_schema

    def __deepcopy__(self, memo):
        """
        If you create a new class you NEED
        to overwrite this method to take new parameters you
        need in it.
        Otherwise things will break, not exactly sure why.
        """

        obj = self.__class__(self.name,
                             [(key, copy.deepcopy(value, memo)) for key, value in self.items()],
                             mask=self.__mask__, strict=self.strict)
        obj.__parents__ = self.__parents__
        return obj

```

This makes sure that the property we added is always passed to copies of the object. This is something that happens internally with Flask-Restplus that I haven't had time to investigate properly.

The next step is to validate the entire JSON payload. To do so we override the _validate_ method as we concluded in the beginning.

```python
def validate(self, data, resolver=None, format_checker=None):
    """
    Override the parent class validate method to raise custom errors
    in our API when payloads don't follow the schema rules.

    This collects a list of errors and delivers it to the user so one
    request is enough to get all the errors.
    """
    validator = Draft4Validator(self.__schema__, resolver=resolver, format_checker=format_checker)
    type_errors = [err for err in validator.iter_errors(data)]
    
    if len(type_errors) >= 1:
        # Raise for multiple errors
        exceptions = [self._convert_type_error_to_custom(err) for err in type_errors]
    
        raise MultipleErrorException(exceptions)
```

Inside the _\_convert\_type\_error\_to\_custom_ function, you can then do the logic that handles the jsonschema error that is returned, and return the appropriate Exception. Personally, I passed a list of exceptions to the MultipleErrorException to return all errors to the user with only one call of the endpoint.

For practicality when registering the models, and remaining Flask-esque you can create your own Namespace class too.

```python
class ValidationNamespace(Namespace):
    """
    Validation Namespace extends the normal Namespace class to
    overwrite the model function, so that we can register a ValidationModel
    by adding directly to the namespace with `ns.model(...)`.
    """

    def model(self, name=None, model=None, mask=None, **kwargs):
        """
        Register a validation model so that classes created with the model method
        can receive the `strict` kwarg.
        """
        model = ValidationModel(name, model, mask=mask, **kwargs)
        model.__apidoc__.update(kwargs)
        return self.add_model(name, model)
```

A problem that you will face is that the validation will be done before the authorization for the user is checked. This is a problem because an unauthorized user can sniff out the payload structure of your endpoint.

To avoid this, you can simply do the following:

```python
class AuthorizedResource(Resource):
    """
    We created this AuthorizedResource from Resource
    because the user authorization was being made after payload
    validation. This way a non-auth'ed user was able to sniff the
    payload that was required by the endpoint.
    By wrapping dispatch_request with the requires_auth function,
    we check for user authentication first.
    """
    @requires_auth
    def dispatch_request(self, *args, **kwargs):
        return super().dispatch_request(*args, **kwargs)
```

Hope this helps!

Thanks for reading,
Jose :)
