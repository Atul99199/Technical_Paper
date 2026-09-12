
# Popular String Utility Methods

Strings are immutable in JavaScript. This means string methods do not change the original string; they return a new value.

```js
const message = "Hello JavaScript";
```
### toUpperCase()

```js
console.log(message.toUpperCase()); // HELLO JAVASCRIPT
```
### toLowerCase()

```js
console.log(message.toLowerCase()); // hello javascript
```
### includes()

```js
console.log(message.includes("JavaScript")); // true
```
### startsWith()

```js
console.log(message.startsWith("Hello")); // true
```
### endsWith()

```js
console.log(message.endsWith("Script")); // true
```
### slice()

```js
console.log(message.slice(0, 5)); // Hello
```
### replace()

```js
const result = message.replace("JavaScript", "World");

console.log(result); // Hello World
```
### split()

Converts a string into an array.

```js
const words = message.split(" ");
console.log(words); // ["Hello", "JavaScript"]
```
### trim()

Removes whitespace from the beginning and end.

```js
const name = "  Atul  ";
console.log(name.trim()); // Atul
```

# Popular Object Utility Methods

Object utility methods are built-in methods used to easily work with object keys, values, entries, copying, and properties.

```js
const student = {
    name: "Atul",
    age: 25
};
```

## Object.keys()

Returns keys of the objects.

```js
console.log(Object.keys(student)); // ["name", "age"]
```
## Object.values()

Returns values of the objects.

```js
console.log(Object.values(student)); // ["Atul", 25]
```

## Object.entries()

Returns key-value pairs of objects. These methods **do not modify the original object**.

```js
console.log(Object.entries(student)); // [["name", "Atul"], ["age", 25]]
```

## Object.assign()

Copies properties into a target object.

**Mutable for the target object**

```js
const student = {
    name: "Atul"
};
Object.assign(student, {
    age: 25
});
console.log(student); // { name: "Atul", age: 25 }
```

# 19. forEach vs map, filter and reduce

### Use `forEach` when:

You want to perform an action on every array element without creating a new array or returning a result.

```js
users.forEach(user => {
    console.log(user.name);
});
```

### Use `map` when:

You want to transform every element of an array and create a new array with the results.

```js
const names = users.map(user => user.name);
```

### Use `filter` when:

You want to select elements from an array that match a specific condition and create a new array.

```js
const adults = users.filter(user => user.age >= 18);
```

### Use `reduce` when:

You want to combine all array elements into one final value, such as a sum, total, or object.

```js
const total = numbers.reduce((sum, number) => sum + number, 0);
```

# 20. Mutable and Immutable Methods

### Mutable

Changes the original array/object.

`
push(), 
pop(),
splice(),
sort(),
`

Example:
```js
const numbers = [1, 2, 3];
numbers.push(4);
console.log(numbers); // [1, 2, 3, 4]
```

### Immutable

Creates or returns a new value without changing the original.

`
map(),
filter(),
slice(),
concat(),
flat()
`

Example:

```js
const numbers = [1, 2, 3];
const result = numbers.map(number => number * 2);
console.log(numbers); // [1, 2, 3]
console.log(result); // [2, 4, 6]
```
Prefer immutable operations when possible because they make code easier to reason about.

