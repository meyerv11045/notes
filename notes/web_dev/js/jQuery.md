# jQuery

- An easy to learn JS library that simplifies JS web programming
  - Wraps common, lengthy tasks into methods that can be called in a single line
  - Simplifies complicated JS things such as AJAX calls & DOM manipulation
- Contains Following Features:
  - HTML/DOM manipulation
  - CSS manipulation
  - HTML event methods
  - Effects and animations
  - AJAX
  - Utilities
  - Many other plugins for other tasks

## Add to Webpages:

1. Download production or development version from jQuery.com into project folder and add it to your project file

   ```html
   <head>
   	<script src="jquery-3.5.1.min.js"></script>
   </head>
   ```

2. Include it from a CDN (Content Delivery Network) such as google:

   ```html
   <head>
   <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
   </head>
   ```

   - Loaded from users cache when they visit your site and it uses google's CDN (faster loading)

 ## Syntax

- Tailor-made for *selecting* HTML elements and performing some *action* on the element(s).
- Basic syntax is:` $(selector).action()`
  - A `$` sign to define/access jQuery
  - A `(selector)` to "query (or find)" HTML elements
  - A jQuery `action()` to be performed on the element(s)

### Document Ready Event

- All jQuery methods are inside a document ready event to prevent any jQuery code from running before the document is finished loading (is ready)
  - Actions on the DOM can fail if document is fully loaded before code is executed

```javascript
$(document).ready(function(){
  // jQuery methods go here..
});

//or the shorter version:

$(function(){
  // jQuery methods go here...
});
```

## Selectors

- Allow you to select and manipulate HTML elements 
- Used to "find" (or select) HTML elements based on their name, id, classes, types, attributes, values of attributes and much more. 
  - Based on the existing CSS Selectors andit has some own custom selectors

### Element: `$("p")`

### Id: `$(#ex_id)`

### Class: `$(".ex_class")

## Event Methods

