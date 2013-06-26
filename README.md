Keynavigator
======

[![Build Status](https://travis-ci.org/nekman/keynavigator.png?branch=master)](https://travis-ci.org/nekman/keynavigator)

Key navigaton plugin for <a href="http://jquery.com">jQuery</a>/<a href="http://zeptojs.com">Zepto</a>.
<br/>
Makes it possible to use arrow keys (or any key) for navigation in eg. `ul` or `table` elements.

###Usage
Include keynavigator.js after having included jQuery or Zepto:
```html
<script src="jquery.js"></script>
<script src="keynavigator.js"></script>
```
Start the keynavigator plugin.
```javascript
$(document).ready(function() {
  $('ul#example li').keynavigator(/* optional settings */);
});  
```

####RequireJS
Include <a href="http://requirejs.org">RequireJS</a>.
```html
<script src="require.js"></script>
```
Start the keynavigator plugin.
```javascript
require(['keynavigator'], function($) {
  $('ul#example li').keynavigator(/* optional settings */);
});  

```
####Settings
```
 cycle: {boolean} - If true, use cycle navigation
  - default: false     

 activeClass: {string} - The name of the class that should be used for the active element.
  - default: 'active'
 
 keys: {object} (keyCode: callback): Callback functions that executes when a key is pressed.

 tabindex: {number} - The tabindex that should be used on the parent element.
  - default: -1

 useCache: {boolean} - If false, run the selector on each keydown. 
                       Useful if elements are added/removed from the DOM.
  - default: true
```

<strong>Custom events</strong><br/>
Subscribe to ```up``` and ```down``` events using:
```javascript
$('ul#example li').keynavigator()
                  .on('up', function(e) {
                    console.log('Pressed up on', $(this));
                  })
                  .on('down', function(e) {
                    console.log('Pressed down on', $(this));
                  });
```

<strong>Example with callbacks</strong><br/>
Key handlers and custom settings:
```javascript
$('ul#example li').keynavigator({
  cycle: true, /* Restart from top/bottom */
  useCache: false, /* Useful if elements are added/removed  */
  activeClass: 'active-blue', /* Class on the active element */
  keys: {
    /* Callback when key 'a' is pressed */
    65: function($el, e) {
      // 'this' - will be the KeyNavigator instance.
      // $el - the element
      // e - the event
      console.log('pressed "a" on', $el);

      // Create a new element and add it to the list.
      $('<li>Appended</li>').insertAfter($el);
      
      this.setActive();
    },

    /* Callback when key 'd' is pressed */
    68: function($el, e) { /* Key 'd' */
      // 'this' - will be the KeyNavigator instance.
      // $el - the element
      // e - the event      
      console.log('pressed "d" on', $el);
      
      // Remove the element.
      $el.remove();

      this.setActive();
    }
  }
});
```
#### Demos and examples
Is available on the project web page - http://nekman.github.io/keynavigator

###License

Licensed under MIT license

Copyright (c) 2013 Nils Ekman

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.