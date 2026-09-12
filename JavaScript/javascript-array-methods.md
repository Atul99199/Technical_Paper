

# Popular Array Utility Methods

Assume:

```js
const numbers = [10, 20, 30, 40];
```

## Array.pop()

Removes the last element.

**Mutable**

```js
numbers.pop();
console.log(numbers); // [10, 20, 30]
```


## Array.push()

Adds an element at the end.

**Mutable**

```js
numbers.push(50);
console.log(numbers); // [10, 20, 30, 40, 50]
```


## Array.concat()

Combines two arrays.

**Immutable**

```js
const result = first.concat(second);
```


## Array.slice()

Copies a part of an array. Original array is unchanged.

**Immutable**

```js
const result = numbers.slice(1, 3);
```


## Array.splice()

Adds, removes or replaces elements.

**Mutable**

```js
const numbers = [10, 20, 30];
numbers.splice(1, 1);
console.log(numbers); // [10, 30]
```

## Array.join()

Converts array elements into a string.

**Immutable**

```js
const names = ["Atul", "Rahul", "Amit"];
const result = names.join(", ");
console.log(result); // Atul, Rahul, Amit
```

## Array.flat()

Flattens nested arrays.

**Immutable**

```js
const numbers = [1, [2, 3], [4, 5]];
console.log(numbers.flat()); // [1, 2, 3, 4, 5]
```

# 14. Array Finding Methods

## find()

Returns the first matching element.

**Immutable**

```js
const numbers = [10, 20, 30, 40];
const result = numbers.find(number => number > 20);
console.log(result); // 30
```

## indexOf()

Returns the index of a value. If not found return `-1`.

**Immutable**

```js
const numbers = [10, 20, 30];
console.log(numbers.indexOf(20)); // 1
```

## includes()

Checks whether a value exists in the array.

**Immutable**

```js
const numbers = [10, 20, 30];
console.log(numbers.includes(20)); // true
```

## findIndex()

Returns the index of the first matching element.

**Immutable**

```js
const numbers = [10, 20, 30];
const index = numbers.findIndex(number => number > 15);
console.log(index); // 1
```

---

# 15. Higher Order Array Functions

A **higher-order function** is a function that receives another function or returns a function.

## forEach()

Used when you want to perform an action for every item.

```js
const numbers = [1, 2, 3];
numbers.forEach(number => {
    console.log(number);
});
```
Returns:
```js
undefined
```

---

## filter()

Creates a new array containing matching elements.

**Immutable**

```js
const numbers = [10, 15, 20, 25];
const result = numbers.filter(number => number > 15);
console.log(result); // [20, 25]
```

## map()

Creates a new array by transforming every element.

**Immutable**

```js
const numbers = [1, 2, 3];
const result = numbers.map(number => number * 2);
console.log(result); // [2, 4, 6]
```

## reduce()

Reduces an array to one value.

**Immutable**

```js
const numbers = [10, 20, 30];
const total = numbers.reduce((sum, number) => {
    return sum + number;
}, 0);
console.log(total); // 60
```

## sort()

Sorts an array. Without the callback, JavaScript sorts values as strings.

**Mutable**

```js
const numbers = [10, 2, 30];
numbers.sort((a, b) => a - b);
console.log(numbers); // [2, 10, 30]
```

# 16. Array Method Chaining

Multiple array methods can be connected.

```js
const numbers = [1, 2, 3, 4, 5];

const result = numbers
    .filter(number => number % 2 === 0)
    .map(number => number * 10);
console.log(result); // [20, 40]
```

Think of it as:

```text
array
  ↓
filter
  ↓
map
  ↓
result
```

---