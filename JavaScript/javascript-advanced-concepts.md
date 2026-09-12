
# Spread Operator in JS

The spread operator (...) is used to expand the elements of an array or properties of an object into another array or object.

### Copy an array

```js
const numbers = [1, 2, 3];
const copy = [...numbers];
console.log(copy); // [1, 2, 3]
```
### Combine arrays

```js
const result = [...first, ...second];
console.log(result); // [1, 2, 3, 4]
```

### Copy an object

```js
const user = {
    name: "Atul",
    age: 25
};
const copy = { ...user };
```


# Template Literals in JS

Template literals use backticks (`) to create strings and allow variable interpolation using ${} and multi-line strings.

```js
const message = `My name is ${name} and I am ${age} years old.`;
```

# Default  in JS

Default parameters allow us to provide a default value for a function parameter when no value is passed.

```js
function greet(name = "Guest") {
    console.log(`Hello ${name}`);
}
greet();
greet("Atul");
```

#  Destructuring in JS

Destructuring is a JavaScript feature used to extract values from arrays or properties from objects and store them in variables.

### Array

```js
const numbers = [10, 20, 30];
const [first, second] = numbers;
console.log(first);  // 10
console.log(second); // 20
```

### Object
```js
const student = {
    name: "Atul",
    age: 25
};
const { name, age } = student;
```
# Closures in JS

A closure is created when an inner function remembers and can access variables from its outer function even after the outer function has finished executing.

```js
function counter() {
    let count = 0;
    return function () {
        count++;
        return count;
    };
}
const increment = counter();
console.log(increment()); // 1
console.log(increment()); // 2
```

---

# Arrow Functions vs Regular Functions

### Syntax

```js
function add(a, b) {
    return a + b;
}
```

Arrow:

```js
const add = (a, b) => a + b;
```

### `this` keyword in JS

The this keyword refers to the object that is currently calling the function; its value depends on how the function is called.

Arrow functions do **not** create their own `this`; they use `this` from the surrounding scope.

```js
const student = {
    name: "Atul",
    greet() {
        console.log(this.name);
    }
};
student.greet();
```

Arrow functions are commonly useful for callbacks:

```js
numbers.map(number => number * 2);
```

---

# `===` vs `==` in JS

`===` checks **value and type**.

`==` performs type conversion before comparison.

```js
console.log(5 === "5"); // false
console.log(5 == "5"); // true
```

# Why `value === undefined` is Better Than `!value`

These are not equivalent.

```js
const value = 0;
console.log(!value); // true
console.log(value === undefined); // false
```

`!value` is true for many falsy values:

`
0,
"",
false,
null,
undefined,
NaN
`. 
If you specifically want to check for `undefined`:

```js
if (value === undefined) {
    // value is specifically undefined
}
```

This is clearer and safer.

---

# `null` vs `undefined` in JS?

### undefined
Usually means a value has not been assigned.

```js
let name;
console.log(name); // undefined
```
### null

Usually means we intentionally have no value.
```js
let selectedUser = null;
```

# CommonJS Modules

JavaScript files can share code using `require()` and `module.exports`.

### math.js

```js
function add(a, b) {
    return a + b;
}
module.exports = {
    add
};
```

### app.js

```js
const { add } = require("./math");
console.log(add(10, 20));
```

# Console Methods

`console` is useful for debugging.

### console.log()

```js
console.log("Hello");
```

### console.error()

```js
console.error("Something failed");
```

### console.warn()

```js
console.warn("Be careful");
```

### console.info()

```js
console.info("Server started");
```

---


# Passing Functions to Other Functions

Functions can be passed as arguments.

```js
function greet(name) {
    console.log(`Hello ${name}`);
}
function processUser(callback) {
    callback("Atul");
}
processUser(greet);
```



# Named vs Anonymous Functions

### Named function
A function that has its own name, making it easier to reuse and identify in debugging.

```js
function calculateTotal(price, quantity) {
    return price * quantity;
}
```

### Anonymous function
A function without its own name, commonly used as a callback or assigned to a variable.

```js
const calculateTotal = function (price, quantity) {
    return price * quantity;
};
```

#  Variable Number of Arguments

JavaScript allows functions to receive different numbers of arguments.

Use the rest operator `...`.

```js
function addAll(...numbers) {
    return numbers.reduce((sum, number) => sum + number, 0);
}
console.log(addAll(10, 20));
console.log(addAll(10, 20, 30, 40));
```

# Debugging Strategies

When something doesn't work, follow a process.

### Step 1: Read the error

Don't ignore:

```text
TypeError
ReferenceError
SyntaxError
```

### Step 2: Find the line

Go directly to that line.

### Step 3: Check the values

Use:

```js
console.log(user);
console.log(user.age);
```

### Step 4: Trace the function calls

Understand:

```text
main()
  ↓
processUser()
  ↓
calculateAge()
  ↓
error
```

### Step 7: Test again

After fixing:

```text
Run → Check output → Test edge cases
```
