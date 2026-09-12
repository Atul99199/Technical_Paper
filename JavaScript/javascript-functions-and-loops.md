# Function Hoisting

Function declarations can be called before they are written.

```js
greet();

function greet() {
    console.log("Hello");
}
```

This works because function declarations are hoisted.

But this does not work:

```js
greet();

const greet = function () {
    console.log("Hello");
};
```

# Function Without a Return Statement

If a function does not return anything, it returns `undefined`.

```js
function greet() {
    console.log("Hello");
}

const result = greet();

console.log(result);
```

Output:

```
Hello
undefined
```


# Different Ways of Declaring a Function

### Function Declaration

```js
function add(a, b) {
    return a + b;
}
```

### Function Expression

```js
const add = function (a, b) {
    return a + b;
};
```

### Arrow Function
- Arrow function, a Lambda function or Anonymous funtion

```js
const add = (a, b) => a + b;
```


#  Pass by Value and Pass by Reference

JavaScript passes arguments **by value**. The function receives a copy. 

For primitive values:

```js
let age = 25;
function changeAge(value) {
    value = 30;
}
changeAge(age);
console.log(age); // 25
```


For objects, the copied value is a **reference to the same object**.

```js
const student = {
    name: "Atul"
};

function changeName(person) {
    person.name = "Rahul";
}
changeName(student);
console.log(student.name); // Rahul
```

The object was changed because both variables refer to the same object.



#  Different Types of Loops

## for Loop

Useful when working with numbers or indexes.

```js
for (let index = 0; index < 5; index++) {
    console.log(index);
}
```

## for...in

Used mainly for object keys.

```js
const student = {
    name: "Atul",
    age: 25
};
for (const key in student) {
    console.log(key, student[key]);
}
```

## for...of

Used for values of iterable objects such as arrays.

```js
const numbers = [10, 20, 30];

for (const number of numbers) {
    console.log(number);
}
```

## forEach

Runs a function for every array item.

```js
const numbers = [10, 20, 30];

numbers.forEach((number) => {
    console.log(number);
});
```

## while

Runs while a condition is true.

```js
let count = 0;

while (count < 3) {
    console.log(count);
    count++;
}
```
# 12. Searching MDN

**MDN (Mozilla Developer Network)** is one of the best references for JavaScript.

When you don't know how something works, search for the exact method.

Examples:

```text
MDN Array.map
MDN Array.filter
MDN String.includes
MDN Object.keys
```

Check:

* Syntax
* Parameters
* Examples



