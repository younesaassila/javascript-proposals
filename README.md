# ECMAScript Proposals

My proposals to improve the ECMAScript programming language.

## `Math.random(min, max)`

**Polyfill:**

```js
const Random = Math.random;

function random(min, max) {
  if (min == null && max == null) {
    min = 0;
    max = 1;
  } else if (max == null) {
    max = min;
    min = 0;
  }

  if (typeof min !== "number") {
    throw new TypeError("min is not a number");
  }

  if (typeof max !== "number") {
    throw new TypeError("max is not a number");
  }

  return Random() * (max - min) + min;
}
```

**Example:**

```js
const price = Math.random(4.5, 10);
console.log(price);
```

## `Math.randomInt(min, max)`

**Polyfill:**

```js
const Random = Math.random;

function randomInt(min, max) {
  if (min == null && max == null) {
    min = 0;
    max = Number.MAX_VALUE;
  } else if (max == null) {
    max = min;
    min = 0;
  }

  if (typeof min !== "number") {
    throw new TypeError("min is not a number");
  }

  if (typeof max !== "number") {
    throw new TypeError("max is not a number");
  }

  max = Math.ceil(max);
  min = Math.ceil(min);

  return Math.floor(Random() * (max - min) + min);
}
```

**Example:**

```js
const age = Math.randomInt(18, 35);
console.log(age);
```

## `Number.isEven(number)`

**Reasoning:** This method would provide a more understandable syntax for beginners and would improve code quality overall.

**Polyfill:**

```js
function isEven(number) {
  if (typeof number !== "number") {
    throw new TypeError("number is not a number");
  }

  return number % 2 === 0;
}
```

**Examples:**

```js
Number.isEven(42); // true
Number.isEven(69); // false
```

## `Number.isOdd(number)`

**Reasoning:** This method would provide a more understandable syntax for beginners and would improve code quality overall.

**Polyfill:**

```js
function isOdd(number) {
  if (typeof number !== "number") {
    throw new TypeError("number is not a number");
  }

  return number % 2 === 1;
}
```

**Examples:**

```js
Number.isOdd(42); // false
Number.isOdd(69); // true
```

## `Array.prototype.groupBy(fn)`

**Polyfill:**

```js
function groupBy(keyGetter) {
  const map = new Map();
  this.forEach((item) => {
    const key = keyGetter(item);
    const collection = map.get(key);
    if (!collection) {
      map.set(key, [item]);
    } else {
      collection.push(item);
    }
  });
  return map;
}
```

**Example:**

```js
const pets = [
  { type: "Dog", name: "Spot" },
  { type: "Cat", name: "Tiger" },
  { type: "Dog", name: "Rover" },
  { type: "Cat", name: "Leo" },
];

pets.groupBy((pet) => pet.type);
```

## `Array.prototype.shuffle()`

**Example:**

```js
const numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
numbers.shuffle(); // [5, 1, 7, 6, 0, 3, 2, 4, 9, 8]
```
