---
layout: post
title: Promise (Tutorials Dehydrated) and ajax request library
category: Dev
tags: [JS, Promise, Fetch, dehydration]
---

When I am working on refactoring the JS modules that do REST API calls, I got to think more about Promise and Ajax request.

## Disclaimer and References
The [Intro](#intro) part of this post is a dehydration and restructuring of different articles and most content are copied WITHOUT quotation for easier reading. All credits go to those nice articles!

- [JavaScript Promises](http://www.html5rocks.com/en/tutorials/es6/promises/)
- [ES6 Promises in Depth](https://ponyfoo.com/articles/es6-promises-in-depth)
- [jQuery deferred broken](https://thewayofcode.wordpress.com/tag/jquery-deferred-broken/)
- [That's so fetch!](https://jakearchibald.com/2015/thats-so-fetch/)

<!--more-->

## Intro
<a name="es6-promise"></a>
### ES6 Promise
ES6 implements `Promise` following [Promises/A+ standard] (http://wiki.commonjs.org/wiki/Promises/A). 

> - A promise represents the eventual value returned from the single completion of an operation. 
> - A promise may be in one of the three states, unfulfilled, fulfilled, and failed. The promise may only move from unfulfilled to fulfilled, or unfulfilled to failed. 
> - Once a promise is fulfilled or failed, the promise's value MUST not be changed, just as a values in JavaScript, primitives and object identities, can not change (although objects themselves may always be mutable even if their identity isn't).
> - A promise is defined as an object that has a function as the value for the property `then`: `then(fulfilledHandler, errorHandler, progressHandler)`

<a name="basics"></a>
#### Basics
A promise should have `resolve`, and uncatched error is considered `reject`.
`then` has a fulfilled handling function and a failed handling function:

```JavaScript
var promise = new Promise(function(resolve, reject) {

  // do async stuff
  if (/* OK */) {
    resolve("Stuff worked!");
  }
  else {
    reject(Error("It broke"));
  }
});

promise.then(function(result) {
  console.log(result); // OK
}, function(err) {
  console.log(err); // Error
});
```

```JavaScript
// in ES6:
new Promise(resolve => resolve()) // promise is fulfilled
new Promise((resolve, reject) => reject()) // promise is rejected
```

**NOTE:** It's recommended to pass an `Error` object since it contains stack trace information.

<a name="error-handling"></a>
#### Error handling
`.catch(function(error) {})`is the same as `.then(undefined, function(error){})`
**NOTE:** `then` and `catch` return a **new** promise every time, so the  `catch` will catch the error in last `then` too.

<a name="sequencing"></a>
#### Sequencing

```JavaScript
// Start off with a promise that always resolves
var sequence = Promise.resolve();

// Loop through our chapter urls
story.chapterUrls.forEach(function(chapterUrl) {
  // Add these actions to the end of the sequence
  sequence = sequence.then(function() {
    return getJSON(chapterUrl);
  }).then(function(chapter) {
    addHtmlToPage(chapter.html);
  });
});

// or simplify it with array.reduce
story.chapterUrls.reduce(function(sequence, chapterUrl) {
  // Add these actions to the end of the sequence
  return sequence.then(function() {
    return getJSON(chapterUrl);
  }).then(function(chapter) {
    addHtmlToPage(chapter.html);
  });
}, Promise.resolve());
```

<a name="parallelism"></a>
#### Parallelism
You get an array of results (whatever the promises fulfilled to) in the same order as the promises you passed in.

```JavaScript
Promise.all(arrayOfPromises).then(function(arrayOfResults) {
  //...
});
```

If a single promise is rejected, `Promise.all` method will be rejected entirely.

```JavaScript
getJSON('story.json').then(function(story) {
  addHtmlToPage(story.heading);

  // Take an array of promises and wait on them all
  return Promise.all(
    // Map our array of chapter urls to
    // an array of chapter json promises
    story.chapterUrls.map(getJSON)
  );
}).then(function(chapters) {
  // Now we have the chapters jsons in order! Loop through…
  chapters.forEach(function(chapter) {
    // …and add to the page
    addHtmlToPage(chapter.html);
  });
  addTextToPage("All done");
}).catch(function(err) {
  // catch any error that happened so far
  addTextToPage("Argh, broken: " + err.message);
}).then(function() {
  document.querySelector('.spinner').style.display = 'none';
});
```

We can fetch JSON for all our chapters at the same time, then create a sequence to add them to the document:

```JavaScript
getJSON('story.json').then(function(story) {
  addHtmlToPage(story.heading);

  // Map our array of chapter urls to
  // an array of chapter json promises.
  // This makes sure they all download parallel.
  return story.chapterUrls.map(getJSON)
    .reduce(function(sequence, chapterPromise) {
      // Use reduce to chain the promises together,
      // adding content to the page for each chapter
      return sequence.then(function() {
        // Wait for everything in the sequence so far,
        // then wait for this chapter to arrive.
        return chapterPromise;
      }).then(function(chapter) {
        addHtmlToPage(chapter.html);
      });
    }, Promise.resolve());
}).then(function() {
  addTextToPage("All done");
}).catch(function(err) {
  // catch any error that happened along the way
  addTextToPage("Argh, broken: " + err.message);
}).then(function() {
  document.querySelector('.spinner').style.display = 'none';
});
```

<a name="promiserace"></a>
#### Promise.race
```JavaScript
Promise.race([
  fetch('/'),
  fetch('foo')
])
  .then(response => console.log(response.statusText))
```
The first promise to `resolve` or `reject` will “win” the race, and `Promise.race` will `resolve` or `reject` as well.

<a name="jquery-promise"></a>
### jQuery Promise
jQuery's promises are broken:

`then` doesn't return a new promise object, so we can't chain `then` and error handling (`catch`).

## not jQuery then, what to use?
Since jQuery doesn't follow the standard, we should find sth else. The goal is to use a library that:

- support promise
- support running in server
- has easy API and is easily replaceable
- support request aborting


<a name="superagent"></a>
### superagent
[superagent](https://visionmedia.github.io/superagent/) is quite popular (5400+ stars!)
- it is a wrapper of XMLHTTPRequest
- it can be used on server side

BUT it doesn't have promise support build in, and it is too much to encapsulate superagent with promise.

<a name="fetch"></a>
### Fetch
`fetch` API is used for making network requests that replaces `XMLHttpRequest`. It naturally support promise. [isomorphic-fetch] is used in [Redux doc](http://rackt.org/redux/docs/advanced/AsyncActions.html). 

According to [That's so fetch!](https://jakearchibald.com/2015/thats-so-fetch/), it has the following benefits:

- Request/Response primitives: `Request` and `Response` constructors will give you the freedom to reuse and manipulate the request and response.
- make a `no-cors` request
- Streaming
- Stream readers & cloning: common data type readers like `response.json()`, `.text()`, etc.
- Headers class
- Cache control 
- No-credential same-origin requests

It is missing:

- Request aborting
- Progress events

We may need request aborting. Although `Fetch` seems quite promising, maybe it's too early to use it.

<a name="axios"></a>
### axios
[axios](https://github.com/mzabriskie/axios), 1400+ stars, seems to be the right choice. 

> - Make XMLHttpRequests from the browser
> - Make http requests from node.js
> - Supports the Promise API
> - Intercept request and response
> - Transform request and response data
> - Automatic transforms for JSON data
> - Client side support for protecting against XSRF

It support promise and request aborting, with a wrapper, we can easily replace it with some other library in the future.





