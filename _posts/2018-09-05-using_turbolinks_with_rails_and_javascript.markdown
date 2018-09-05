---
layout: post
title:      "Using Turbolinks with Rails and JavaScript"
date:       2018-09-05 23:11:02 +0000
permalink:  using_turbolinks_with_rails_and_javascript
---

Turbolinks is a feature included Rails 4 and 5. It's purpose is to speed up loading times of web pages. Per its [github documentation](https://github.com/turbolinks/turbolinks "Turbolinks Documentation"), Turbolinks gives "the performance benefits of a single-page application without the added complexity of a client-side JavaScript framework". For the web developer, there is no need for additional server side code nor rendering of either partials or JSON.

Turbolinks functions by taking advantage of HTML5's [history.pushState()](https://developer.mozilla.org/en-US/docs/Web/API/History_API#Adding_and_modifying_history_entries "MDN history.pushState()") method to manipulate the URL bar display in the browser, then making an XMLHttpRequest and rendering the HTML response. It's a win-win for everyone.

Well, not always. A potential breakdown occurs when custom scripts are meant to be executed after page or DOM load. Take the following example:
```javascript
$(document).ready(function() {
  $('#element').on('click', (event) => {
    event.preventDefault();
    doThisInstead();
  });
});
```
The code above states that once the document or DOM is loaded and ready, the code within the function will then execute. In this case, this guarantees that script event listeners have an element that is loaded and actually exists. Great! So what's the big deal?

Turbolinks bypasses this whole process. Other than the initial page load, any subsequent site navigation will not result in full page loads, only changes. What this means is, using the same example as before, the script may execute before the DOM is ready, before the `$('#element')` exists, and therefore, will not properly attach the event listener. And our site functionality is kaput!

How then can we take advantage of Turbolink's features without breaking down our site? When Turbolink takes over after navigating through our website, it fires various events. One of these events is `turbolinks:load`, which occurs not only upon initial page load, but also upon any subsequent navigation. We can tweak our code the following way:
```javascript
$(document).on('turbolinks:load', function() {
  $('#element').on('click', (event) => {
    event.preventDefault();
    doThisInstead();
  });
});
```
By listening to the `turbolinks:load` event, we can be sure that our custon scripts are executed once our page is truly ready.
