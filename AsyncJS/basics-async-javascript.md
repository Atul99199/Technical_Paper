# JavaScript Execution and Asynchronous JavaScript


#  How JavaScript Executes Code?

- JavaScript is a **single-threaded** programming language.
- This means JavaScript normally executes one piece of code at a time.

JavaScript uses a few important components to execute our code:

- Call Stack
- Web APIs
- Callback Queue
- Event Loop

The JavaScript engine first reads our code and executes synchronous code using the **Call Stack**.


## What is the Call Stack?

The Call Stack is a data structure used by JavaScript to keep track of function calls during execution. It follows the LIFO principle.


##  What is asynchronous JavaScript?
Asynchronous JavaScript allows an operation to complete later without stopping the execution of other JavaScript code.



##  What are Web APIs?

Web APIs are browser-provided features that JavaScript can use for tasks such as timers, network requests, DOM manipulation, and browser storage.

Examples include:

- `setTimeout()`
- `fetch()`
- DOM APIs
- Event APIs
- `localStorage`
- Geolocation APIs

## What is the Event Loop?

The **Event Loop** is a mechanism that helps JavaScript handle asynchronous operations even though JavaScript is single-threaded.

The Event Loop continuously checks:

1. Is the Call Stack empty?
2. Are there callbacks waiting to be executed?

If the Call Stack is empty, the Event Loop can move appropriate callbacks into the Call Stack.


##  What is Callback Hell?


Callback Hell happens when multiple callbacks are nested inside each other, making the code difficult to read, debug, and maintain.

## What is Inversion of Control?


Inversion of Control in callbacks means giving another function control over when and how our callback function is executed.


## What is a Promise?


A Promise is an object that represents the eventual success or failure of an asynchronous operation.

##  Callbacks vs Promises

**Why are Promises preferred over callbacks in many cases?**

Callbacks are useful, but when many asynchronous operations depend on each other, callbacks can become difficult to manage.

Promises provide a structured way to represent asynchronous results.

### Callback

```js
getData(function(data) {
  console.log(data);
});
```

### Promise

```js
getData()
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log(error);
  });
```

Promises make chaining and error handling easier.

---
