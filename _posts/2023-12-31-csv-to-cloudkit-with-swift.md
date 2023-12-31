---
layout: post
title: Using Swift and CSVs to send data to CloudKit DB
excerpt_separator:  <!--more-->
categories:
  - Code
tags:
  - Learning
  - Boulderbook
---

**Pre-requisite:** Don't forget to read the section "Accessing CloudKit Using a Server-to-Server Key" [in this page here](https://developer.apple.com/library/archive/documentation/DataManagement/Conceptual/CloudKitWebServicesReference/SettingUpWebServices.html#//apple_ref/doc/uid/TP40015240-CH24-SW1). You will need to create a key that you can work with.

TL;DR: [This GitHub repository](https://github.com/theholy7/csv-to-cloudkit-db) has the code I wrote to upload a CSV to CloudKit Database. Scroll to the bottom for a quick heads-up on a hard to find (un)documented behaviour.

Try the code by forking it and first adjusting the `Location` struct to your needs and then running:

```text
$ swift build
$ swift run csvToCloudKit \
	--ck-key-id "your/key/id" \
	--private-key-file-path "path/to/file.pem" \
	--csv-file-path "path/to/file.csv"
```

Ideally, a blog post has something new to say. I am not sure my post fits that category to everyone, but it does to me.

A while ago, I had an idea for an app, and I decided to learn SwiftUI and Swift to make it happen. Why those technologies? Because I am a Mac and iPhone user, and I wanted to take full advantage of the libraries available. I wanted to be able to integrate with any possible Apple services.

I have not gotten far in my app, but I did solve one of my first hurdles. As such, I want to share some of the things that I have learned, and the code that I have built.

Let me set the scene:  I want to learn how to user CloudKit DB, and I want to seed it with data that will be viewable in my app.

In my case, the seed data consists of a set of locations that are relevant to the users. Though seeding databases is such a common problem, I did not find a trivial solution to seed my database, say: using a CSV and importing it into the table (or set of records) that match the CSV's schema.

I know that spreadsheets and CSVs are the devil - I have talked about that at previous jobs many times - however, for this quick script, it should be fine. I am only using it for 28 locations, and by the time I need to manage more, I will have a better solution. This is just a proof of concept and a learning experience.

Back to our problem, some of the solutions I saw involved adding the CSV as a part of the app Bundle, and then creating a button that would push the data to the database from my iOS app. This way, it is possible to use the CloudKit library, and a lot of the functionality built into the environment that is used to build iOS apps.

I don't know if this is the right way, but it doesn't feel like it. So I decided I wanted to create a [Swift CLI script](https://www.swift.org/getting-started/cli-swiftpm/) that would take a file and parse each row to create it as an record in the database. Nevertheless, what sounds like an easy task is not. We can’t use CloudKit, we need to use [CloudKit Web Services](https://developer.apple.com/library/archive/documentation/DataManagement/Conceptual/CloudKitWebServicesReference/index.html#//apple_ref/doc/uid/TP40015240-CH41-SW1).

I divided my code in three parts:
- The reader that loads and parses my CSV - [here](https://github.com/theholy7/csv-to-cloudkit-db/blob/b0568c070b938806ed64e0d86cb73bd3696e9155/Sources/csvToCloudKit.swift#L38-L53)
- The models that represent my record and the CloudKit requests - [here](https://github.com/theholy7/csv-to-cloudkit-db/blob/b0568c070b938806ed64e0d86cb73bd3696e9155/Sources/Models.swift#L14-L102)
- The requests that I need to use to create my records - [here](https://github.com/theholy7/csv-to-cloudkit-db/blob/b0568c070b938806ed64e0d86cb73bd3696e9155/Sources/Models.swift#L176-L231)

The biggest hurdle was that the `type` values in the **Record Field Dictionary** must be upper case! The documentation reads:

> A record field dictionary represents the value of a field and is of the form `{ value: CKValue, type: string (optional) }`. [CKValue](https://developer.apple.com/library/archive/documentation/DataManagement/Conceptual/CloudKitWebServicesReference/Types.html#//apple_ref/doc/uid/TP40015240-CH3-SW1) represents field values of type String, Number, Boolean, Reference, Asset, and Location.

But nowhere does it say that `type` needs to exactly match the text schema of the database, such as:

```text
primitive-type:
    | ASSET
    | BYTES
    | DOUBLE
    | [ ENCRYPTED ] { BYTES | STRING | DOUBLE | INT64 | LOCATION | TIMESTAMP }
    | INT64
    | LOCATION
    | NUMBER [ PREFERRED AS { INT64 | DOUBLE } ]
    | REFERENCE
    | STRING
    | TIMESTAMP
```

Once I tried with upper case values and the code worked, I was super happy!

That's it! Shoot me any questions if you have them! :)
