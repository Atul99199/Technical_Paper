
#  Error Handling with try...catch

`try...catch` allows us to handle errors without stopping the entire program unexpectedly.

```js
try {
    const result = JSON.parse("invalid json");
} catch (error) {
    console.error("Something went wrong:", error.message);
}
```

Structure:

```js
try {
    // code that may fail
} catch (error) {
    // handle error
}
```
# Throwing Errors

Throwing an error means manually stopping normal execution and reporting a problem using the throw statement.

Handle it:

```js
try {
    throw new Error("Invalid age");
} catch (error) {
    console.error(error.message);
}
```


# `throw new Error()` vs `throw "message"`

Creates a proper Error object containing useful information like the error message and stack trace.

**Prefer:**

- ` throw new Error("Something went wrong"); `

Throws a simple string instead of an Error object, so it does not provide a proper stack trace and is generally not recommended.

**Avoid:**

- ` throw "Something went wrong"; `

# Reading Error Messages and Stack Traces

Read the error type, message, file name, and line number in the stack trace to identify where and why the error occurred

Look at:

1. Error type
2. Error message
3. File name
4. Line number
5. Function name
6. Previous function calls



Error:

```text
TypeError: Cannot read properties of undefined
```

# Importance of the catch Block

The catch block handles errors from the try block, preventing the program from stopping unexpectedly and allowing us to respond appropriately.

```js
try {
    riskyOperation();
} catch (error) {
    console.error("Operation failed:", error.message);
}
```

Without proper error handling, an application may fail unexpectedly.

The catch block can:

* Show a useful message
* Log the error
* Return a fallback value
* Clean up resources

---