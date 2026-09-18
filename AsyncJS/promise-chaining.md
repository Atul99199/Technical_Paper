# Promises - Chaining, Error Handling and Promise APIs

## 1. How to chain promises using `.then`?

We can chain multiple `.then()` methods, where the result returned from one `.then()` is passed to the next `.then()`.

```js
Promise.resolve(10)
  .then((value) => {
    return value + 5;
  })
  .then((value) => {
    return value * 2;
  })
  .then((value) => {
    console.log(value);
  });
```

**Output:**

```text
30
```

---

## 2. How to handle errors in a promise chain using `.catch`?

We use `.catch()` to handle rejected Promises or errors thrown inside `.then()`.

```js
Promise.resolve("Start")
  .then(() => {
    throw new Error("Something went wrong");
  })
  .catch((error) => {
    console.log(error.message);
  });
```

## 3. How does `finally()` work in a promise chain?

`finally()` runs after the Promise is settled, whether it is fulfilled or rejected. It is commonly used for cleanup work.

```js
Promise.resolve("Success")
  .then((data) => {
    console.log(data);
  })
  .finally(() => {
    console.log("Operation finished");
  });
```

## 4. What happens when an Error gets thrown inside `.then()` when there is a `.catch`?

The error makes the current Promise rejected, and the nearest following `.catch()` handles the error.

```js
Promise.resolve()
  .then(() => {
    throw new Error("Error occurred");
  })
  .catch((error) => {
    console.log(error.message);
  });
```


## 5. What happens when an Error gets thrown inside `.then()` when there is no `.catch`?

The Promise becomes rejected, but there is no handler to handle the error. This results in an **unhandled Promise rejection**.

```js
Promise.resolve()
  .then(() => {
    throw new Error("Something went wrong");
  });
```

The runtime reports an unhandled rejection because no error handler was provided.

## 6. Why must `.catch` be placed towards the end of the promise chain?

`.catch()` is usually placed near the end so that it can handle errors from multiple steps in the chain.

```js
getUser()
  .then((user) => getOrders(user))
  .then((orders) => getPayment(orders))
  .then((payment) => {
    console.log(payment);
  })
  .catch((error) => {
    console.log(error);
  });
```

## 7. How to consume multiple promises by chaining?

We can return a Promise from one `.then()` and use its result in the next `.then()`.

```js
getUser()
  .then((user) => {
    return getOrders(user);
  })
  .then((orders) => {
    return getPayment(orders);
  })
  .then((payment) => {
    console.log(payment);
  })
  .catch((error) => {
    console.log(error);
  });
```

## 8. How to consume multiple promises using `Promise.all()`?

`Promise.all()` runs multiple Promises together and waits until all of them are fulfilled.

```js
const promise1 = Promise.resolve("User");
const promise2 = Promise.resolve("Orders");
const promise3 = Promise.resolve("Payment");

Promise.all([promise1, promise2, promise3])
  .then((results) => {
    console.log(results);
  })
  .catch((error) => {
    console.log(error);
  });
```
If any Promise is rejected, `Promise.all()` is rejected.

---

## 9. How to do error handling when using Promises?

We can use `.catch()` with Promise chains.

```js
getData()
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log("Error:", error);
  });
```

With `async/await`, we can use `try...catch`.

```js
async function getData() {
  try {
    const data = await fetchData();
    console.log(data);
  } catch (error) {
    console.log("Error:", error);
  }
}
```

---

## 10. Why is error handling the most important part of using a Promise?

Error handling prevents application failures from going unnoticed and allows us to show a proper response or take another action when an asynchronous operation fails.

```js
fetchData()
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log("Unable to fetch data");
  });
```

Without error handling, rejected Promises can become unhandled rejections.

---

# Promisifying Callback-Based Functions

## 11. How to promisify an asynchronous callback-based function?

Promisification means converting a callback-based function into a function that returns a Promise.

For example, `setTimeout()` can be wrapped inside a Promise.

### Promisifying `setTimeout()`

```js
function wait(ms) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve("Time completed");
    }, ms);
  });
}

wait(2000)
  .then((message) => {
    console.log(message);
  });
```


## 12. How to promisify `fs.readFile()`?

Node.js provides a Promise-based version of many file-system APIs.

```js
const fs = require("fs").promises;

fs.readFile("data.txt", "utf8")
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log(error);
  });
```

# Promise APIs

## 13. How to use `Promise.resolve()`?

`Promise.resolve()` creates a fulfilled Promise with the given value.

```js
Promise.resolve("Success")
  .then((value) => {
    console.log(value);
  });
```

## 14. How to use `Promise.reject()`?

`Promise.reject()` creates a rejected Promise with the given error or reason.

```js
Promise.reject("Something went wrong")
  .catch((error) => {
    console.log(error);
  });
```

## 15. How to use `Promise.all()`?

`Promise.all()` waits for all given Promises to fulfill and returns their results in the same order.

```js
const p1 = Promise.resolve("A");
const p2 = Promise.resolve("B");
const p3 = Promise.resolve("C");

Promise.all([p1, p2, p3])
  .then((results) => {
    console.log(results);
  });
```

## 16. How to use `Promise.allSettled()`?

`Promise.allSettled()` waits for all Promises to finish, whether they are fulfilled or rejected.

```js
const p1 = Promise.resolve("Success");
const p2 = Promise.reject("Failed");

Promise.allSettled([p1, p2])
  .then((results) => {
    console.log(results);
  });
```

Unlike `Promise.all()`, one rejected Promise does not stop the results from being returned.

## 17. How to use `Promise.any()`?

`Promise.any()` returns the first Promise that is fulfilled.

```js
const p1 = Promise.reject("Failed 1");
const p2 = Promise.resolve("Success");
const p3 = Promise.resolve("Success 2");

Promise.any([p1, p2, p3])
  .then((result) => {
    console.log(result);
  });
```

It ignores rejected Promises until it finds a fulfilled Promise.

If all Promises are rejected, `Promise.any()` rejects with an `AggregateError`.

## 18. How to use `Promise.race()`?

`Promise.race()` returns the result of the first Promise that settles, whether it is fulfilled or rejected.

```js
const p1 = new Promise((resolve) => {
  setTimeout(() => resolve("First"), 1000);
});

const p2 = new Promise((resolve) => {
  setTimeout(() => resolve("Second"), 2000);
});

Promise.race([p1, p2])
  .then((result) => {
    console.log(result);
  });
```

