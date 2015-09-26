---
layout: post
title: Bootstrap Components
tags:
- Bootstrap
- Web Development
published: true
date: 2015-07-04 01:10:00
---

Components such as buttons, headers, navigation menus, and comments system are commonly found on websites. Through its components, Bootstrap helps us add such features to our sites quickly and easily.

## Page Components
Page components form the basic structure of a web page. Examples of page components include page headers, standout panels for displaying important information, nested comments sections, image thumbnails, and stacked lists of links.

### Page Headers
Bootstrap has created an HTML component to be used as a __page headers__ that takes care of all these additional tasks for us. Before we check out the markup for the page header, let's first set up the project that we'll be using:

Now, let's add the markup for a page header:

```html
<div class="page-header">
  <h1>Chapter 3</h1>
</div>
```

Whenever you want to use the ```<h1>``` tag for a page title, you can wrap it in a ```<div>``` element that has a class of page-header to create a page header component. The page header component doesn't add any additional styles for the h1 other than a thin gray bottom border. It only comes with styles for adding subtitles.

A small issue that we see here is that the page header has stuck to the browser's left border. That's because we haven't defined a container for all the contents of our web page. So let's create a global container:

```html
<div class="container">

</div>
```
Let's see the united version:

```html
<div class="container">
  <div class="page-header">
    <h1>Chapter 3</h1>
  </div>
</div>
```

If you want to add a subtitle beside the title of the page, you can put it inside the same ``` <h1>``` tag that we used before. Make sure you wrap the subtitle inside a ``` <small></small> ``` tag.

### Panels
Panels are used to display text or images within a box with rounded corners. Here's how to create a panel

```html
<div class="panel panel-default">
  <div class="panel-heading">ATTENTION</div>
  <div class="panel-body">Lorem ipsum dolor sit ametnim ...</div>
  <div class="panel-footer">
    <a href="#" class="btn btn-danger btn-sm">Agree</a>
    <a href="#" class="btn btn-default btn-sm">Decline</a>
  </div>
</div>
```

![Bootstrap-panels](http://eneskemalergin.github.io/images/bootstrap_panel.png)

As you can see, the panel div has been divided into three parts: the panel-head , panel-body , and panel-footer . Each of these panel parts is optional.

Panels come with various color options. In the previous code, I've used the default color with the help of the panel-default class. You can also use other classes for different colors:

 - panel-primary for dark blue
 - panel-success for green
 - panel-info for sky blue
 - panel-warning for yellow
 - panel-danger for red

### Media Object
Media object is used for creating components that should contain left or right-aligned media (image, video, or audio) alongside some textual content. You need to carefully design some reusable HTML markup that supports nested commenting. Bootstrap's media object comes in handy here, as you can quite easily create multiple levels of nested comments using it.

```html
<div class="media">
  <a class="pull-left" href="#">
    <img class="media-object" src="path/to/image" alt="Syed Fazle Rahman">
  </a>
  <div class="media-body">
    <h4 class="media-heading">Awesome piece of work!</h4>
    <p>Lorem ipsum dolor sit amet, consectetur ...</p>
  </div>
</div>
```

To produce a media object you need to create a div with a class of media . Then you put two necessary components within it: the media itself (here it's an image) and the media-body .

### Thumbnails
It is used for displaying images and videos with clickable appeal by applying a border that forms a box around them. It also comes with a neat hover effect that highlights the focused thumbnail by changing its border color to blue.

```html
<a href="#" class="thumbnail">
  <img src="path/to/image">
</a>
```

we'll use the class col-xs-3 to create a four-column design:

```html
<div class="row">
  <div class="col-xs-3">
    <a href="#" class="thumbnail">
      <img src="path/to/image">
      </a>
  </div>

  <div class="col-xs-3">
    <a href="#" class="thumbnail">
      <img src="path/to/image">
    </a>
  </div>

  <div class="col-xs-3">
    <a href="#" class="thumbnail">
      <img src="path/to/image">
    </a>
  </div>

  <div class="col-xs-3">
    <a href="#" class="thumbnail">
      <img src="path/to/image">
    </a>
  </div>
</div>
```

![bootstrap-thumbnail](http://eneskemalergin.github.io/images/bootstrap-thumbnail.png)

Try hovering your mouse icon over each image and you should get a nice highlighted effect. Let's give a caption to each thumbnail. We just need to add an extra div with class caption just below the <img> tag. Our snippet for a thumbnail with a caption should be:

```html
<a href="#" class="thumbnail">
  <img src="path/to/image">
  <div class="caption">
    <h3>Caption Goes Here!</h3>
  </div>
</a>
```

You can also add some excerpts to each thumbnail and a Read More button for linking to different pages in your website. For this we need to first replace the link element with the class thumbnail with a div element. Then we add an excerpt using ```<p>``` inside the “ caption ” div and a link with a “Read More ” anchor and classes ```btn``` and ```btn-primary``` inside the same “caption ” div . After making these changes, our final markup for a post thumbnail will be as follows:

```html
<div class="thumbnail">
  <img src="images/microsoft.png">
  <div class="caption">
    <h3>Microsoft</h3>
    <p>Lorem ipsum dolor sit amet, consectetur ...</p>
    <p><a href="#" class="btn btn-primary">Read More</a></p>
  </div>
</div>
```

### List Group
List group is a useful component for creating lists, such as a list of useful resources or a list of recent activities. You can also use it for a complex list of large amounts of textual content.

```html
<ul class="list-group">
  <li class="list-group-item">Inbox</li>
  <li class="list-group-item">Sent</li>
  <li class="list-group-item">Drafts</li>
  <li class="list-group-item">Deleted</li>
  <li class="list-group-item">Spam</li>
</ul>
```

![bootstrap-list-groups](http://eneskemalergin.github.io/images/bootstrap-list-groups.png)

You need to add the class list-group to a ul element or a div element to make its children appear as a list. The children can be li elements or a elements, depending on your parent element choice. The child should always have the class list-group- item.

 > When you want to display a list of links, you should use the anchor element a
instead of list elements li (that also means using a parent div, instead of a ul).

We can also display a number (such as those used to indicate pending notifications) beside each list item using the badge component. Now you can add the following snippet inside each “list-group-item ” to display a number beside each one:

```html
<span class="badge">14</span>
```

![bootstrap-list-groups-item](http://eneskemalergin.github.io/images/bootstrap-list-groups-item.png)

As you can see, the badges beautifully align themselves to the right of each list item. We can also apply various colors to each list item by adding ```list-group-item-*``` classes along with list-group-item . They are as follows:

 - list-group-item-success for green
 - list-group-item-info for sky blue
 - list-group-item-warning for pale yellow
 - list-group-item-danger for light red

Adding list-group-item-success to the list-group-item class in the following list will give it a light green background color:

```html
 <li class="list-group-item list-group-item-success">Inbox</li>
```

> Will be continued...
