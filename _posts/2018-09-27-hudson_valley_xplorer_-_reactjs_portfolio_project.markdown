---
layout: post
title:      "Hudson Valley Xplorer - ReactJS Portfolio Project"
date:       2018-09-27 07:42:47 -0400
permalink:  hudson_valley_xplorer_-_reactjs_portfolio_project
---


Hudson Valley Xplorer (HVX) is a web-based application built with ReactJS for the front-end and Ruby on Rails framework for the back-end API. HVX allows users to see information about various restaurants, parks, museums, etc. around New York's Hudson Valley. Users can also create posts to share information related to their neighborhoods in the Hudson Valley. Others can comment on posts to contribute to the friendly conversation. Let's talk about to technologies this application utilizes.

### ReactJS
ReactJS, or simply React, is a JavaScript library that facilitates building user interfaces (UI). It was created and first used by Facebook, which also uses it for its Instagram platform. 

One great thing about React is its use of JavaScript XML (JSX). JSX is simply a syntax extension of JavaScript. It doesn't have to be used in React; vanilla JS will work just fine. However, JSX is beneficial because it describes how the UI should look like. Take the following example:
```javascript

const userElement = (
  <div>
    <h2>Jack Nicholson</h2>
    <ul>
      <li>A Few Good Men</li>
      <li>One Flew Over the Cuckoos Nest</li>
      <li>The Shining</li>
    </ul>
  </div>
)

```
Looks just like HTML. Except it's not. It's JSX, which is then transpiled by Babel into JavaScript. Remember, React facilitates building the UI. So, why shouldn't the code we use to build our visual elements resemble the HTML that is rendered in a browser or application window?

Speaking of HTML and DOM, React includes a virtual DOM. What this means is rather than refreshing the entire DOM, React renders to a virtual DOM, computes the changes, and updates the DOM. Therefore, a small change won't cause an entire DOM refresh, and your application will load faster for the user. Win-win!

### Redux - One Source of Truth
  >"I want the truth!", begged Lt. Daniel Kaffee as he badgered the witness on the stand.
  >"You can't handle the truth!!!", resonated Col. Nathan Jessep, making sure the entire court heard him.
  > —A Few Good Men (1992)

Sorry, guys... I couldn't resist. Yes, this military law film is one of my favorites. But Tom Cruise sure does say something all React developers want in their application —the truth. On its own React can handle state within its components. That's all fine and dandy for a simple application, maybe even for a more complicated app with multiple nested components. But it can become difficult to manage. Just take a look at the following figure.

![React vs Redux State Management](https://i.imgur.com/Gmx7pNs.jpg?1)

Wow! Even that would make Col. Jessep order another Code Red (seriously, watch the movie). Without Redux, state and component props get passed around parent and child components. Again, that is doable. But it can cause growing pains when it comes time to expand the application. And we haven't even begun to mention having to pass state between two components that don't have a direct parent-child relationship, otherwise referred to as cousin components.

Enter Redux. Per its documentation, Redux is based on three fundamental principles:
  1. Single source of truth
  2. State is read-only
  3. Changes to state are made with pure functions

Essentially, Redux creates a single state, or source of truth, for the entire application within a single *store*. Views cannot alter the state directly, but they can emit *actions* that describe the change in store state. Actions are just plain objects with a key of type that describes the intent.
```javascript
// actionObject is declared/assigned, then passed to the dispatch method that is called on the store
const actionObject = {
  type: 'CREATE_USER',
  user: {name: 'Col. Jessep', playedBy: 'Jack Nicholson'}
}

store.dispatch(actionObject)
```
Redux then dispatches the action object to a *reducer*, a pure function that returns the new state. Say it with me one more time. Reducers are *pure functions*. That is, reducers return a new state rather than simply altering the current one. They also are used to set the initial state.
```javascript
// Reducer takes in two arguments: the state and action object
export default function userReducer (
  state = {
    user: {}
  },
  action
  ) {
  switch (action.type) {
    case 'CREATE_USER':
    // Our action will initiate this switch case and return a new state
    // Notice the spread operator used to prevent altering the current state
    // Object.assign() can also be used here
      return {...state,
        user: action.user
      }
    default:
    // Otherwise, the reducer will return the current state,
    // or the default state if initializing the Redux store
      return state;
  }
}
```
Container components within React can then subscribe to the Redux state. If the state changes, the subscribed component will in turn update with the new state, if needed. Subscribed container components also initiate actions that are dispatched to the reducers.

