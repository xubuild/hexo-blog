---
layout: post
title: Learn Redux and React-Redux - Tutorials Dehydrated (WIP)
category: Dev
tags: [JS, Redux, React, Flux, dehydration]
---

The best way to learn Redux: 

- [videos by redux author](https://egghead.io/series/getting-started-with-redux)
- read the doc and source code!

## Disclaimer and References
This post is a dehydration and restructuring of different articles and most content are copied WITHOUT quotation for easier reading. All credits go to those nice articles!

- [Redux doc](http://rackt.org/redux/index.html)
- [React 数据流管理架构之 Redux 介绍](http://www.alloyteam.com/2015/09/react-redux/)

<!--more-->

## Redux
>Redux is a predictable state container for JavaScript apps.

> - The whole state of your app is stored in an object tree inside a single **store**.
> - The only way to change the state tree is to emit an **action**, an object describing what happened.
> - To specify how the actions transform the state tree, you write pure **reducers**.

<a name="action"></a>
### Action
`action` is plain JS object used to define/trigger a change in store. 

```JavaScript
{
  type: 'ADD_FILM',
  name: 'Mission: Impossible'
}
```

<a name="helper-action-creator"></a>
#### Helper: Action Creator 
Helper functions to create actions:

```JavaScript
function addFilm(name) {
  return { type: 'ADD_FILM', name: name };
}
```

<a name="reducer"></a>
### Reducer
Reducer is a function. It takes an **action** and transform the **old state** to **new state**:

```JavaScript
let reducer = (oldState, action) => newState;
```

It should stay **pure**, so you should **NOT**:

- Mutate the old state and action;
- Perform side effects like API calls and routing transitions;
- Calling non-pure functions, e.g. `Date.now()` or `Math.random()`.

In a reducer, the previous state should be returned in the `default` case. It's important to return the previous state for any unknown action.

[object spread syntax] (https://github.com/sebmarkbage/ecmascript-rest-spread)

filmReducer:

```JavaScript
function filmReducer(state = [], action) {
  switch (action.type) {
    case 'ADD_FILM':
      return [{
          id: action.id,
          name: action.name
      }, ...state];

    case 'DELETE_FILM':
      return state.films.filter(film =>
          film.id !== action.id
          );
    default:
      return state;
  }
}
```

Combined rootReducer:

```JavaScript
function rootReducer(state = {}, action) {
  return {
    films: filmReducer(state.films, action),
    filter: filterReducer(state.filter, action)
  };
}
```

rootReducer will pass different part of `state` to corresponding `reducers`, and combine the results to a new `state`.

<a name="helper-combinereducers"></a>
#### Helper: combineReducers
`combineReducers()` is used to simplify the combination:

```JavaScript
var rootReducer = combineReducers({
    films: filmReducer,
    filter: filterReducer
});
```

One `action` will go through all `reducers`. There will be **one single root reducer**.

<a name="store"></a>
### Store
There is only one store in a Redux app and it has the following responsibilities:
- Holds application state;
- Allows access to state via `getState()`;
- Allows state to be updated via `dispatch(action)`;
- Registers listeners via `subscribe(listener)`.

You'll only have a single store in a Redux application. When you want to split your data handling logic, you'll use reducer composition instead of many stores.

```JavaScript
let store = createStore(REDUCER, INITIAL_STATE);
```

Store provides 3 methods: `dispatch`, `subscribe` and `getState`. It could be sth like:

```JavaScript
function createStore(reducer, initialState) {

    var currentReducer = reducer;
    var currentState = initialState;
    var listeners = [];
 
    function getState() {
      return currentState;
    }
 
    function subscribe(listener) {
      listeners.push(listener);
 
      return function unsubscribe() {
        var index = listeners.indexOf(listener);
        listeners.splice(index, 1);
      };
    }
 
    function dispatch(action) {
        currentState = currentReducer(currentState, action);
        listeners.slice().forEach(listener => listener());
        return action;
    }
 
    return {
      dispatch,
      subscribe,
      getState
    };
}
```

## React and Redux
[Why use Redux over Facebook Flux](https://stackoverflow.com/questions/32461229/why-use-redux-over-facebook-flux)

<a name="provider"></a>
### Provider 
`Provider` makes our `store` instance available to the components below. (Internally, this is done via React's [context](https://facebook.github.io/react/docs/context.html) feature.)

```JavaScript
import React from 'react';
import { render } from 'react-dom';
import { createStore } from 'redux';
import { Provider } from 'react-redux';
import App from './containers/App';
import todoApp from './reducers';

let store = createStore(todoApp);

let rootElement = document.getElementById('root');
render(
  <Provider store={store}>
    <App />
  </Provider>,
  rootElement
);
```

In `App` component and its sub-components, you can use `connect` to make `store` available for them.

<a name="connect"></a>
### Connect

`Connect` will Wrap the top-level component or route handlers and return a new component. It will do the following things:

- passing `store`'s `dispatch` function as *wrapped component*'s prop `dispatch`
- passing data (from the global state, part which it needs) as *wrapped component*'s prop
- internally, `store` will `subscribe` the *wrapper component*'s `handleChange()`. So is the store's state changes, it will call `handleChange`, which calls `this.setState` and triggers re-render.  

```JavaScript
class FilmApp extends Component {
  render() {
    // injected from connect()
    const { films, dispatch } = this.props;
    return (
        <div>
          // addFilm is action creator which returns action object
          <AddFilm 
            films={films} 
            onAddClick={name => dispatch(addFilm(name))}
          />
        </div>
    );
  }
}

// select which part of state is needed from global state
function select(state) {
  return {
    films: state.films
  };
}

export default connect(select)(FilmApp);
```

<a name="helper-bindactioncreators"></a>
### Helper: bindActionCreators 

Normally you should just call `dispatch` directly on your Store instance. 
When you want to pass some action creators down to a component that isn't aware of Redux, and you don't want to pass `dispatch` or the Redux `store` to it, use `bindActionCreators`. It is a encapsulation of `action` (action creator) and `store.dispatch`.

It turns an object whose values are `action creators`, into an object with the same keys, but with every `action creator` wrapped into a `dispatch` call so they may be invoked directly.

FilmActionCreators.js:

```JavaScript
function addFilm(name) {
  return { type: 'ADD_FILM', name: name };
}
function deleteFilm(name) {
  return { type: 'ADD_FILM', name: name };
}
```

```JavaScript
import * as FilmActionCreators from './FilmActionCreators';
render() {
let filmActions = bindActionCreators(FilmActionCreators, dispatch);
// console.log(filmActions);
// {
//    addFilm : function,
//    deleteFilm : function
// }
return (
      <AddFilm action={filmActions.addFilm} />
      <Main actions={filmActions}>
    );
}
```


