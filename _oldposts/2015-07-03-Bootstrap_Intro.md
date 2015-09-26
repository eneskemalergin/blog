---
layout: post
title: Bootstrap Introduction
tags:
- Bootstrap
- Web Development
published: true
date: 2015-07-03 04:30:00
---

## What is Bootstrap?
Bootstrap is a front-end framework that helps developers to jump start the web de- velopment process.

## Why there is Bootstrap?
Imagine you have to design a website with an attractive navigation bar, stylish buttons, nice typography, placeholders for texts and images, a big image slider, and more—yet you arenʼt a front end development expert.But what if these features were already coded for you, and you just had to write a little HTML to use them? This is Bootstrap.

Yet Bootstrap is more than just decorating links, images and typography. One of its most important features is the grid system. You cannot create a mobile-friendly and responsive website without the grid system.

Bootstrap allows you to customize its styles through the use of Less and Sass. Developers acquainted with these technologies can completely modify Bootstrapʼs default look and feel.

## Responsive Design
Responsive web design allows developers to create a website that can change its layout on the go. Developers can then create a single design that works on any kind of device: mobiles, tablets, smart TVs, and PCs.

Suppose we have the layout shown here for desktop screen:

![responsive_design1](http://eneskemalergin.github.io/images/responsive_design1.png)

We have three main sections in our desktop layout: the header, the content section, and the footer area. The header section contains a logo and a rectangular ad. The content section contains four smaller posts placed side by side horizontally. We then have two bigger posts placed underneath the smaller posts. Finally, we have a footer section in which there is simple copyright text.

When we used Bootstrap's grid system in our code, so the layout will automatically
adjust to suit tablets and mobile devices. In tablets:

![responsive_tablet](http://eneskemalergin.github.io/images/responsive_tablet.png)

In smartphones we can see that the header section continues to follow the tablet view but thereʼs a major change in the content sectionThe posts reflow themselves to the bottom forming two rows, each containing two posts. The bigger posts are now placed on top of each other—one post in one row (the second big post is off the bottom of the screen):

![responsive_smart](http://eneskemalergin.github.io/images/responsive_smart.png)

## Getting Bootstrap
Go to [Bootstrap](http://getbootstrap.com) and download the latest version available. Extract the archive file and copy the following folders:
 - css
 - fonts
 - js

Also you need your html files as well. It must be your own work. Then you will make its make-up.

Here is the folder called Bootstrap_demos with copied files from Bootstrap and our index file(html)

![responsive_smart](http://eneskemalergin.github.io/images/bootstrap_demo.png)

### What's bootstrap.min.css ?
Thereʼs also another file named bootstrap.min.css , which is the minified version of bootstrap.css . It is called minified because it has no spaces and no comments, which reduces the size of the file. It will be used when your project is completed and is ready for production.

Letʼs link our CSS file into index.html . Place the following inside the ```<head>``` tag and below the ```<title>``` tag:

```html
<link rel="stylesheet" type="text/css" href="css/bootstrap.css">
```

Bootstrap requires jQuery for its JavaScript components to work. Go to jquery.com 20 and download jQuery version 1.11.0. Bootstrap supports Internet Explorer 8 and above.

Let's link jquery.js file into index.html. and Bootstrap's JavaScript file as well:

```html
<script src="js/jquery.js"></script>

<script src="js/bootstrap.js"></script>

```

In total it should look like this:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title> Bootstrap Practice </title>
    <link rel="stylesheet" type="text/css" href="css/bootstrap.css">
  </head>
  <body>
    <script src="js/jquery.js"></script>
    <script src="js/bootstrap.js"></script>
  </body>
</html>
```

In order to make Bootstrap completely compatible with every kind of device, we need to include some necessary meta tags. Here is a simple guideline for [compatibility mode](http://eneskemalergin.github.io/Compatibility_Mode/).
