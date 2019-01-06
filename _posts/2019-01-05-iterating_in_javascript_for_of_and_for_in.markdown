---
layout: post
title:      "Iterating in JavaScript: for..of and for..in"
date:       2019-01-06 01:29:45 +0000
permalink:  iterating_in_javascript_for_of_and_for_in
---

Back in the older days (pre-ES2015), the only way to iterate through a collection using JavaScript was to use a loop, such as a `for` loop.
```javascript
for (let i = 0; i < array.length; i++) {
  console.log(array[i]);
}
```
This most definitely got the job done, but more complicated than was necessary. Enter the `for...of` statement.
```javascript
for (const element of someArray) {
  console.log(element);
}
```
Same task accomplished, but in a much cleaner manner - no need for a counter or condition. JavaScript currently allows `for...of` statements to be used with any iterable types. This includes array, strings, array-like objects (e.g., `arguments` or `NodeList`), maps, and sets.

Note that, by default, objects are not iterables. Therefore, `for...of` won't work with objects out of the box. There is a way for us to do this by creating a `Symbol.iterator` key for the object we want to iterate over and providing a custom iterator. However, that is out of the scope of this article. If you'd like more information, I thoroughly enjoyed the examples provided by [Brandon Morelli on Medium](https://codeburst.io/a-simple-guide-to-es6-iterators-in-javascript-with-examples-189d052c3d8e).

Okay, but what about objects? Enter the `for...in` statement, which iterates over the properties of an object. Keep in mind, however, that the entire property is not passed in, only the keys. We can then use those keys to access the object's values.
```javascript
const user = {
  firstName: 'John',
  lastName: 'Doe',
  gender: 'male'
}

for (const key in user) {
  console.log(key)
}

// LOG: firstName
// LOG: lastName
// LOG: gender

for (const key in user) {
  console.log(user[key])
}

// LOG: John
// LOG: Doe
// LOG: male
```
Again, very simple way to iterate over the properties of an object. It should be noted that `for...in` should generally not be used with arrays if the order of the iteration matters. This is because different browsers implement this statement in different ways. And per documentation, 'a `for...in` loop iterates over the properties of an object in an arbitrary order'.
