---
layout: post
title: Bootstrap Components-2
tags:
- Bootstrap
- Web Development
published: true
date: 2015-07-04 01:10:00
---

## Navigation Components
Features such as navigation bars and breadcrumbs have become an essential part of many websites. Bootstrap comes with many components built in to help build such features.

### Navs

__Navs__ are a group of links that are placed inline with each other to be used for navigation. We have options to make this group of links appear either as tabs or small buttons, the latter known as __pills__ in Bootstrap.

```html
<ul class="nav nav-tabs">
  <li class="active"><a href="#">About</a></li>
  <li><a href="#">Activity</a></li>
  <li><a href="#">Liked Pages</a></li>
</ul>
```

![bootstrap-tab-navigation](http://eneskemalergin.github.io/images/bootstrap-tab-navigation.png)


The class nav is common to both tabs and pills. We've added the nav-tabs class to make our navigation bar look like tabs.

```html
<ul class="nav nav-pills">
  <li class="active"><a href="#">About</a></li>
  <li><a href="#">Activity</a></li>
  <li><a href="#">Liked Pages</a></li>
</ul>
```
![bootstrap-pill-navigation](http://eneskemalergin.github.io/images/bootstrap-bill-navigation.png)

Here, we have replaced the class nav-tabs with class nav-pills , which make the same list look like pills.

### Navbar
The Navbar is one of the most interesting Bootstrap components.

Bootstrap makes creating navigation bars very easy. It comes with various options to build all types of navigation bars that are responsive, automatically collapsing when the screen's size is small.

First, we'll build a div element, with two classes navbar and navbar-default . These classes are important to Bootstrap as they identify where to apply the navigation bar styles and effects:

```html
<div class="navbar navbar-default">
</div>
```

Next, we'll use a div with class container-fluid inside this navbar element. This will wrap all the contents of the navbar and create a full-width container inside it:

```html
<div class="navbar navbar-default">
  <div class="container-fluid">

  </div>
</div>
```

Now, let's start inserting other elements inside the navbar. First, we'll place a div with class navbar-header. This hidden button will be later used to expand the collapsed menu in smaller screens:

```html
<div class="navbar navbar-default">
  <div class="container-fluid">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#mynavbar-content">
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
    </button>
    <a class="navbar-brand" href="#">SitePoint</a>
    </div>
  </div>
</div>
```
In the code, we have placed a button with a class navbar-toggle that is used by Bootstrap to activate the navbar's toggling behavior. It should have two custom data-* type attributes: data-toggle and data-target . data-toggle tells the script what to do when the button is clicked, whereas data-target tells which section to toggle when clicked. Here, the data-target attribute is holding an id of a section that we're yet to define. That section will be toggled when the button is clicked. The span elements inside the button are used for displaying the icon.

We have also defined an a element with class navbar-brand that holds the name of our website

![bootstrap-navbar](http://eneskemalergin.github.io/images/bootstrap-navbar.png)

![bootstrap-navbar2](http://eneskemalergin.github.io/images/bootstrap-navbar2.png)

Next, we'll create another div that will be the sibling of navbar-header ; that is, it is present at the same level in the markup hierarchy. We will give two classes to this element: collapse and navbar-collapse . As this div will contain all the navbar content, we'll give the id mynavbar-content to it, the same id that is mentioned inside the data-toggle attribute of the hidden button.

```html
<div class="navbar navbar-default">
  <div class="container-fluid">
    <div class="navbar-header">
      <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#mynavbar-content">
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
        <span class="icon-bar"></span>
      </button>
      <a class="navbar-brand" href="#">Sitepoint</a>
      </div>
      <div class="collapse navbar-collapse" id="mynavbar-content"></div>
  </div>
</div>
```

Now let's start filling up the navbar-collapse element with the set of links we want to place inside the navigation bar. We'll use the ul element with classes nav and navbar-nav here. These classes are used to align the links properly with the navigation bar:

```html
<div class="navbar navbar-default">
  <div class="container-fluid">
    <div class="navbar-header">
    <button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#mynavbar-content">
      <span class="icon-bar"></span>
      <span class="icon-bar"></span>
      <span class="icon-bar"></span>
    </button>
    <a class="navbar-brand" href="#">SitePoint</a>
  </div>
  <div class="collapse navbar-collapse" id="mynavbar-content">
    <ul class="nav navbar-nav">
      <li class="active"><a href="#">Home</a></li>
      <li><a href="#">About</a></li>
      <li><a href="#">Pricing</a></li>
      <li><a href="#">Contact</a></li>
      <li><a href="#">Feedback</a></li>
    </ul>
  </div>
</div>
</div>
```

## Standing Out
Sometimes we need to design components that when used with other HTML elements grab visitors' attention immediately. They can be labels, notification icons, or huge buttons such as “Buy now”, “Grab it”, and so on. Bootstrap ships with many such components out of the box.

### Label
Labels are the best way to display short text beside other components. Sometimes we may need to display text such as “New” or “Download now”, for example, beside some other HTML elements. Labels come in handy in such places.

To display a label, you need to add a label class to inline HTML elements such as span and i . Here, we'll use a span to show a label beside an h3 element:

```html
<h3>Jump Start Bootstrap <span class="label label-default">New</span></h3>
```

![bootstrap-labels](http://eneskemalergin.github.io/images/bootstrap-labels.png)

There's an additional class, label-default , that is necessary to tell Bootstrap which variant of label we want to use. The available label variants are:

 - label-default for gray
 - label-primary for dark blue
 - label-success for green
 - label-info for light blue
 - label-warning for orange
 - label-danger for red

### Buttons
You can easily create a button in Bootstrap. You just have to add the btn class to convert an a , button , or input element into a fancy bold button in Bootstrap:

```html
<a href="#" class="btn btn-primary">Click Here</a>
```

![bootstrap-button](http://eneskemalergin.github.io/images/bootstrap-button.png)

Buttons come in various color options:

 - btn-default for white
 -  btn-primary for dark blue
 - btn-success for green
 - btn-info for light blue
 - btn-warning for orange
 - btn-danger for red

And in various sizes:

 - btn-lg for large buttons
 - btn-sm for small buttons
 - btn-xs for extra small buttons
 
