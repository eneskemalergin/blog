---
layout: post
title: Bootstrap Grid System
tags:
- Bootstrap
- Web Development
published: true
date: 2015-07-03 06:39:00
---

Grid system is one of the most important feature of Bootstrap.

## What is a Grid System?
Grid system divides the screen into multiple rows and columns that can be used to create various types of layouts. Once we have the rows and columns defined, we can decide which HTML element will be placed where.

 * Bootstrap's grid system divides the screen into columns―up to 12 in each row.
 * Bootstrap's grid system is responsive, as the columns resize themselves dynamically when the size of browser window changes.
 * You can create an infinite number of rows depending on your design's requirements.

## Building a Basic Grid
Bootstrap recommends that we should place all the rows and columns inside a container to ensure proper alignment and padding. There are two types of container classes in Bootstrap: container and container-fluid.

The former creates a fixed-width container in the browser window, while the latter creates a full-width fluid container. The fixed-width container is styled to appear at the center of the screen,omitting extra space on both sides. Hence, it is a good practice to wrap all the contents within a container.

We will use the fixed-width container in our demo. Let's go ahead and create a container in our HTML page:

```html
<div class="container">
</div>
```

Next, we'll create a row inside a container. Once the row is defined, we can start creating the columns. Bootstrap has a class row for creating rows:

```html
<div class="container">
  <div class="row">
  </div>
</div>
```

You can create an infinite number of rows but they must be placed within a contain- er. For better results, it is recommended to have a single container with all the rows inside it.

In Bootstrap, columns are created by specifying how many of the 12 available Bootstrap columns you wish to span. Suppose we want to have only a single column. It should span across all twelve available Bootstrap columns. For this we'll use the class col-xs-12 , with the number 12 specifying the amount of columns to span.

Similarly, to create two equal-width columns in a row, we'd use the class col-xs- 6 for each one. This tells Bootstrap that we want two columns that span across six of Bootstrap's columns, as follows:

```html
<div class="container">
  <div class="row">
    <div class="col-xs-6">
      <h4>Column 1</h4>
    </div>
    <div class="col-xs-6">
      <h4>Column 2</h4>
    </div>
  </div>
</div>
```

But what does the xs stand for in the class col-xs-6 ? Bootstrap has four types of class prefixes for creating columns for different size displays:

 1. col-xs for extra small displays (screen width < 768px)
 2. col-sm for smaller displays (screen width ≥ 768px)
 3. col-md for medium displays (screen width ≥ 992px)
 4. col-lg for larger displays (screen width ≥ 1200px)

Let's examine the following markup:

```html
<div class="container">
  <div class="row">
    <div class="col-xs-12 col-sm-6 col1">
      <h4>Column 1</h4>
    </div>
    <div class ="col-xs-12 col-sm-6 col2">
      <h4>Column 2</h4>
    </div>
  </div>
</div>

```

In this code we have used the class col-xs-12 for an extra small display and class col-sm-6 for a smaller sized display. Hence, each column in an extra small-sized display will occupy all the 12 available Bootstrap columns, which will appear as a stack of columns. Yet on a smaller display, they will occupy only six Bootstrap columns each to achieve a two-column layout as shown below:

![grid-columns](http://eneskemalergin.github.io/images/grid-columns.png)

## Nesting Columns
You can always create a new set of 12 Bootstrap columns within any column in your layout. This can be done by building a new row element within an existing column and then filling this row with custom columns.

Let's illustrate this with an example. Make a new HTML file in the project called nested.html. Form the HTML markup with Bootstrap set up in it as discussed in the  last chapter. In addition, link the CSS file styles.css that we created earlier in this chapter. The markup of this new HTML file should look this:

```html
<!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="utf-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width,initial-scale=1">

      <title>My First Bootstrap Website</title>
      <link rel="stylesheet" type="text/css" href="css/bootstrap.css">

      <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/libs/html5shiv/3.7.0/html5shiv.js"></script>
      <script src="https://oss.maxcdn.com/libs/respond.js/1.4.2/respond.min.js"></script>
      <![endif]-->

    </head>
    <body>
      <script src="js/jquery.js"></script>
      <script src="js/bootstrap.js"></script>
    </body>
    </html>
```
Let's create a container and a row within it. Targeting medium-sized displays, we'll construct a two-column layout. By now, we know that to create a two-column layout, we should span our columns to six Bootstrap columns. Hence, the class for generating such columns will be ```col-md-6``` . Let's add two columns to the previous markup:

```html
<div class="container">
  <div class="row">

    <div class="col-md-6 col1">
      <h3>Column 1</h3>
    </div>

    <div class="col-md-6 col2">
      <h3>Column 2</h3>
    </div>
    </div>
</div>
```

Let's now nest the first column “Column 1” and start a new row within it:

```html
<div class="container">
  <div class="row">
    <div class="col-md-6 col1">
      <h3>Column 1</h3>
      <!-- Nesting Starts -->
      <div class="row">

      </div>

    </div>

    <div class="col-md-6 col2">
      <h3>Column 2</h3>
    </div>

  </div>
</div>
```

As we have a new row , let's form two columns again within it:

```html
<div class="container">
  <div class="row">
    <div class="col-md-6 col1">
      <h3>Column 1</h3>
      <!-- Nesting Starts -->
      <div class="row">
        <div class="col-md-6 col3">
          <h3>Column 4</h3>
        </div>

        <div class="col-md-6 col4">
          <h3>Column 5</h3>
        </div>
      </div>
    </div>

    <div class="col-md-6 col2">
      <h3>Column 2</h3>
    </div>

  </div>
</div>
```

## Offsetting Columns
Offsetting is another great feature of Bootstrap's grid system. It is generally used to increase the left margin of a column. For example, if you have a column that should appear after a gap of three Bootstrap columns, you can use the offsetting feature.

Classes that are available for offsetting are:
 - col-xs-offset-*
 - col-sm-offset-*
 - col-md-offset-*
 - col-lg-offset-*

Suppose we want to move a column three Bootstrap columns towards the right in
extra-small displays, we can use the class ```col-xs-offset-3```.

> Note that there's a three-column gap on both the left and right side of this column. This is one of the best ways of centering a 50% width column in the middle of the screen.
