---
layout: post
title: Fix for failed GitHub Pages
excerpt_separator:  <!--more-->
categories:
  - Random Code
tags:
  - Jekyll
  - GitHub Pages
---
Did you ever get this email?

```
The page build failed for the `master` branch with the following error:

The hydeout theme is not currently supported on GitHub Pages. For more information, see https://help.github.com/articles/adding-a-jekyll-theme-to-your-github-pages-site/.

For information on troubleshooting Jekyll see:

  https://help.github.com/articles/troubleshooting-jekyll-builds

If you have any questions you can contact us by replying to this email.
```

I finally tracked down my problem... <!--more-->

In my `_config.yml` file I had set the variable:

```yml
github:
  repository: https://github.com/theholy7
```

and this was in conflict with Github's metadata variable. As soon as I removed it from my file, the build went through!

Hope this helps,

Jose
