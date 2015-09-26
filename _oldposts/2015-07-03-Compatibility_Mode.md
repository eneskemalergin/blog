---
layout: post
title: Compatibility Mode
tags:
- Web Development
- HTML tags
published: true
date: 2015-07-03 03:30:00
---

First, we should tell browsers that our website contains characters from the Unicode character set, a superset of the ASCII character set. This is done using the following meta tag:

```html
<meta charset="utf-8">
```

Sometimes, Internet Explorer may run in __compatibility mode__. Using the following code snippet would force IE to use the latest rendering engine to render our website. This will prevent our website from breaking as older rendering engines do not support all properties of CSS:

```html
<meta http-equiv="X-UA-Compatible" content="IE=edge">
```
Next, weʼll make our site consume all the space available inside the browser window, whether itʼs a tablet or a mobile or even a desktop screen. We tell the browser to scale our application to the size of window space available:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```
hereʼs one final step we need to deal with in the above code. Bootstrap 3 uses many HTML5 elements and CSS3 properties that wonʼt work in Internet Explorer 8. We now have to add some scripts that will only be called into action when the website is opened in IE8, bringing support for HTML5 and CSS3 in it. These scripts included in head are __html5shiv.js__ and __respond.js__ :

```html
<!--[if lt IE 9]>
<script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
<script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
<![endif]-->
```

> You donʼt have to download html5shiv.js and r espond.js . You can simply directly link to their CDN, as shown above.
