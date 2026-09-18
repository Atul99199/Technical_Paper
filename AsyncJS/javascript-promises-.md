# JavaScript Promises

## Q1. What is a Promise?

**Answer:**

A Promise is a JavaScript object that represents the eventual result of an asynchronous operation. It can be pending, fulfilled, or rejected.

---

## Q2. How do you create a Promise?

We create a Promise using the `Promise` constructor.

The syntax is:

```js
const promise = new Promise((resolve, reject) => {
  // asynchronous operation

  resolve();
  // or
  reject();
});
```

The Promise constructor receives a function called the **executor function**.

The executor function receives two parameters:

```text
resolve
reject
```


## Q3. What is resolve?

**Answer:**

`resolve()` is used to indicate that a Promise operation was successful.

```js
resolve("Success");
```

---

## Q4. What is reject?

**Answer:**

`reject()` is used to indicate that a Promise operation failed.

```js
reject("Failed");
```

---

## Q5. What are the states of a Promise?

**Answer:**

A Promise has three states:

- Pending
- Fulfilled
- Rejected

---

## Q6. What is Pending?

**Answer:**

Pending means the asynchronous operation has not completed yet.

---

## Q7. What is Fulfilled?

**Answer:**

Fulfilled means the asynchronous operation completed successfully.

---

## Q8. What is Rejected?

**Answer:**

Rejected means the asynchronous operation failed.

---

## Q9. How do you consume a Promise?

**Answer:**

We can consume a Promise using `.then()`, `.catch()`, and `.finally()`.

```js
promise
  .then((result) => {
    console.log(result);
  })
  .catch((error) => {
    console.log(error);
  })
  .finally(() => {
    console.log("Finished");
  });
```

---

## Q10. What is `.then()`?

**Answer:**

`.then()` is used to handle the successful result of a Promise.
### Example

```js
const promise = new Promise((resolve, reject) => {
  resolve("Data received");
});

promise.then((data) => {
  console.log(data);
});
```

---

## Q11. What is `.catch()`?

**Answer:**

`.catch()` is used to handle errors or rejected Promises.

```js
const promise = new Promise((resolve, reject) => {
  reject("Something went wrong");
});

promise.catch((error) => {
  console.log(error);
});
```
---

## Q12. What is `.finally()`?

**Answer:**

`.finally()` runs after the Promise is settled, whether it was fulfilled or rejected.

### Example

```js
const promise = new Promise((resolve, reject) => {
  resolve("Success");
});

promise
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.log(error);
  })
  .finally(() => {
    console.log("Operation finished");
  });
```

---

## Q13. Can a Promise change its state multiple times?

**Answer:**

No. A Promise can settle only once.

It can change from:

```text
Pending → Fulfilled
```

or:

```text
Pending → Rejected
```

After that, its state cannot change.

---