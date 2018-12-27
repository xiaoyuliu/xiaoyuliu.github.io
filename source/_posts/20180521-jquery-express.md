---
title: 16 jQuery, 23-24 Express
date: Mon May 21 23:33:11 2018
categories: Web Developer Bootcamp
tags:
- front end
- javascript
---


## jQuery

### Introduction to [jQuery](https://jquery.com)

A Javascript DOM manipulation library. Compared to vanilla DOM, jQuery can speed up some operations by fewer scripts.

### jQuery Selectors

Using `$` to select everything you want in css format. Always return a list, even there's only one item.

```javascript
// select a tag
$("img")

// select a class
$(".sale")

// select an id
$("#bonus")

// select an embeded tag
$("li a")

// select i-th specific target
$("div:nth-child(N)")
$("div:first-of-type")
$("div").first ()
$("div").last()
```

### Manipulate Style

`.css(property, value)`

```javascript
$("h1").css("color", "yellow")

// get text
$("h1").text()

// get html format
$("ul").html()

// get attr and modify it
$("img").attr()

// get the value of an input for text or color or etc.
$("input").val()

// modify class
$("h1").addClass()
$("h1").removeClass()
$("h1").toggleClass()

```
More on the [website](http://api.jquery.com/).

### jQuery Events

#### The most useful three events:

- click()
```javascript
// add an alert when any button is clicked
$("button").click(function() {
    alert("someone clicked a button");
    });
```
- keypress()
```javascript
// every time you input one letter
$("#target").keypress(function() {
    console.log("Handler for .keypress() called");
    });

// if you want to add an event for different letter
$("#target").keypress(function(event) {
    // event.which, the name of event variable can be any
    if (event.which === SOME_NUMBER) {
        console.log("You hit the key");
    }
    });
```
- on()
```javascript
// the most frequently used event
$("#submit").on('click', function() {
    // do something
    });
```

#### Difference between `click()` and `on('click)`:

- `click()` only adds listeners for existing elements
- `on()` will add listeners for all potential future elements

### jQuery Effects

List several common effects.

`.fadeOut`/`.fadeIn`/`.fadeToggle`

`.slideDown`/`.slideUp`/`.slideToggle`


```javascript
// all divs will be removed after 4s fading out when clicking the button
$("button").on("click", function() {
    $("div").fadeOut(1000, function() {
        $(this).remove();
        });
    });
```

## Express

### Introduction to [Express](https://expressjs.com/)

A fast web framework for Node.js, which is a javascript runtime environment to allow the server to run javascript.

### Environment preparation

```bash
cd /path/to/web/folder
npm init
npm install express --save
npm install ejs --save
```

### Common functions

#### Import Express to `app.js`

```js
var express = require('express');
var app = express();
```

#### Start the server

```js
app.listen(process.env.PORT, process.env.IP, function() {
    console.log('Server is listening');
    });
```

#### Set default engine/folder to look for `css` files

```js
// look for .ejs for rendering
app.set('view engine', 'ejs');
// defaultly look for .css files inside public folder
app.use(express.static('public'));
```

#### Refer a `.css` file in `.ejs` file

```html
<link rel="stylesheet" href='/app.css'>
```

We must use <span style="background: yellow">/app</span> instead of `app`, because `/` can force the web not looking for the `.css` file under the same folder.

#### Render a page with a specific route

```js
// Fix route
app.get('/', function(req, res) {
    res.send('This is the root page.');
    });

// route with a variable
app.get('/homepage/:name', function(req, res) {
    var name = req.params.name;
    res.send('This is the homepage of ' + name);
    });

// send route variable to ejs file
app.get('/homepage/:name', function(req, res) {
    var name = req.params.name;
    res.render('homepage', {name: name})
    });
```

And inside `homepage.ejs` file:

```html
This is the page of <%= name %>
```

#### difference between `<%=` and `<%`

For contents between `<%=` and `%>`, they will be added to the html file and berendered. But with `<%`, the contents will not be rendered. For example, we need to run some conditions inside the `ejs` file but we don't want to display them then we should use `<%`.


