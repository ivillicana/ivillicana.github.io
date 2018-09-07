---
layout: post
title:      "Coupon Manager 2.0 - Rails with JavaScript Portfolio Project"
date:       2018-09-06 21:37:22 -0400
permalink:  coupon_manager_2_0_-_rails_with_javascript_portfolio_project
---

This is a continuation of my pevious project: Coupon Manager. You can read about that project in my blog post [*Coupon Manager - Rails Portfolio Project*](http://isaacvillicana.com/coupon_manager).

Coupon Manager is a web app that allows thrifty shoppers to create, share, organize, and save coupons. It's built on the Ruby on Rails framework, taking advantage of ActiveRecord models, associations, routes/nested routes, and view helpers. The omniAuth gem is also included, allowing users to authenticate with a third-party provider, in this case, Facebook. User accounts can also be created within the application, using bCrypt to hash passwords in the database.

However, this version of Coupon Manager has two new features: JavaScript/jQuery and Handlebars Templates.

### JavaScript and jQuery
Version 2 of Coupon Manager leverages JavaScript and jQuery to manipulate the DOM, handle events, and make AJAX requests. To take advantage of these features, the Rails back-end code was altered to serve JSON instead of HTML in most instances, specifically when dealing with ActiveRecord model objects, e.g., coupons, stores, and users. The JSON responses are then translated to JavaScript model objects, which facilitates the use of Handlebars templates. Prototype methods are also made available by creating prototype objects.

```javascript
// JSON response sent by Rails Controller
// data = {
//   id: 1,
//   couponCode: "ABC123",
//   item: "Water Bottles",
//   store: {
//      id: 3,
//      name: "Target"
//   } 
// }

class Coupon {
  constructor(data) {
    this.id = data.id;
    this.couponC...
  }

  couponPrototypeMethodExample() {
    
  }
}
```

### Handlebars Templates
Handlebars.js is used to build templates allowing JavaScript objects to be displayed with ease. Here is and example:
```javascript
// coupons.js
$('#display').html( HandlebarsTemplates['coupon_template'](jsObject) );

// coupon_template.hbs
<h1>{{ item }}</h1>
<h4>{{ couponCode }}</h4>

<p>{{ store.name }}</p>
<p>{{ description }}</p>
```
which renders the following HTML:
```html
<h1>Water Bottles</h1>
<h4>ABC123</h4>

<p>Target</p>
<p>This is a description of this item</p>
```
Notice then that rather than loading a new page with the rendered HTML output by the Handlebars template, the response is simply rendered on the page with the `$('#display')` jQuery selector and `$.html()` method.
