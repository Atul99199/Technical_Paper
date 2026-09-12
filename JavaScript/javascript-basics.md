# Different Data Types in JavaScript

JavaScript has **primitive** and **non-primitive** data types.

### Primitive


1. String
2. Number
3. BigInt
4. Boolean
5. Undefined
7. Null
8. Symbol


### Non-Primitive

1. Array
2. Object

**Important:** Arrays and functions are technically objects in JavaScript.

---

# Scope in JavaScript

Scope decides **where a variable can be accessed**.

### Global Scope :

A variable declared outside all functions and blocks can be accessed from anywhere in the program.

### Function Scope :

A variable declared inside a function can only be accessed within that function. var is function-scoped.

### Block Scope :

A variable declared inside `{}` can only be accessed within that block. let and const are block-scoped.


#  let, var and const


| Keyword | Reassign | Redeclare | Scope    |
| ------- | -------- | --------- | -------- |
| `let`   | Yes      | No        | Block    |
| `const` | No       | No        | Block    |
| `var`   | Yes      | Yes       | Function |




#  Why We Must Not Use `var`

`var` is function-scoped, allows redeclaration, and can cause unexpected behavior because it ignores block scope.

# Why Global Variables Are Bad

Global variables can be changed from many places.

```js
let score = 100;

function updateScore() {
    score = 50;
}

function anotherFunction() {
    score = 10;
}
```

Now it becomes difficult to know **which function changed `score`**.


# Truthy and Falsy Values

JavaScript treats some values as `false` in conditions.

### Falsy values

```js
false
0
-0
""
null
undefined
NaN
```

Example:

```js
let name = "";

if (name) {
    console.log("Name exists");
} else {
    console.log("Name is empty");
}
```

Most other values are truthy.

```js
if ("hello") {
    console.log("Truthy");
}
```

## Reference :

- MDN — Var : https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/var