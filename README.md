# Javascript Practice Problems

> *Click &#9733; if you like the project. Your contributions are heartily ♡ welcome.*

<br/>

**Table Contents**
- [Javascript Practice Problems](#javascript-practice-problems)
  - [Find a prime number in an array](#find-a-prime-number-in-an-array)
  - [Find an object in an array by one of its properties](#find-an-object-in-an-array-by-one-of-its-properties)
  - [Find the index of a prime number in an array](#find-the-index-of-a-prime-number-in-an-array)
  - [Sorting array of objects](#sorting-array-of-objects)
  - [Undo/Redo Functionality](#undoredo-functionality)
  - [Matching Brackets](#matching-brackets)
  - [Min Stack](#min-stack)


## Find a prime number in an array

```js
function isPrime(element, index, array) {
  let start = 2;
  while (start <= Math.sqrt(element)) {
    if (element % start++ < 1) {
      return false;
    }
  }
  return element > 1;
}

console.log([4, 6, 8, 12].find(isPrime)); // undefined, not found
console.log([4, 5, 8, 12].find(isPrime)); // 5
```


## Find an object in an array by one of its properties

```js
const inventory = [
  { name: "apples", quantity: 2 },
  { name: "bananas", quantity: 0 },
  { name: "cherries", quantity: 5 },
];

function isCherries(fruit) {
  return fruit.name === "cherries";
}

console.log(inventory.find(isCherries));
// { name: 'cherries', quantity: 5 }
```

## Find the index of a prime number in an array

```js
function isPrime(element) {
  if (element % 2 === 0 || element < 2) {
    return false;
  }
  for (let factor = 3; factor <= Math.sqrt(element); factor += 2) {
    if (element % factor === 0) {
      return false;
    }
  }
  return true;
}

console.log([4, 6, 8, 9, 12].findIndex(isPrime)); // -1, not found
console.log([4, 6, 7, 9, 12].findIndex(isPrime)); // 2 (array[2] is 7)

```

## Sorting array of objects

```js
const items = [
  { name: "Edward", value: 21 },
  { name: "Sharpe", value: 37 },
  { name: "And", value: 45 },
  { name: "The", value: -12 },
  { name: "Magnetic", value: 13 },
  { name: "Zeros", value: 37 },
];

// sort by value
items.sort((a, b) => a.value - b.value);

// sort by name
items.sort((a, b) => {
  const nameA = a.name.toUpperCase(); // ignore upper and lowercase
  const nameB = b.name.toUpperCase(); // ignore upper and lowercase
  if (nameA < nameB) {
    return -1;
  }
  if (nameA > nameB) {
    return 1;
  }

  // names must be equal
  return 0;
});
```

## Undo/Redo Functionality

```js
const undoStack = [];
const redoStack = [];

function doAction(action) {
  undoStack.push(action);
  // perform action
}

function undo() {
  const lastAction = undoStack.pop();
  redoStack.push(lastAction);
  // reverse action
}
```

## Matching Brackets - Valid Parenthesis

- Time complexity - O(n)
- Space complexity - O(n) `minStack` tracks min values

```js
function isValid(s) {
  const stack = [];
  const map = { ')': '(', '}': '{', ']': '[' };

  for (let char of s) {
    if (['(', '{', '['].includes(char)) {
      stack.push(char);
    } else {
      if (stack.pop() !== map[char]) return false;
    }
  }
  return stack.length === 0;
}
```

## Min Stack

[Min stack leetcode problem](https://leetcode.com/problems/min-stack/description/)

- Time complexity - O(1) per *operation*
- Space complexity - O(n) `minStack` tracks min values

| Stack |	Purpose|
|---|---|
|mainStack | Stores all values |
|minStack |	Tracks current minimums|

```js
class MinStack {
  constructor() {
    this.mainStack = [];
    this.minStack = [];
  }

  push(value) {
    this.mainStack.push(value);
    if (
      this.minStack.length === 0 ||
      value <= this.getMin()
    ) {
      this.minStack.push(value);
    }
  }

  pop() {
    const removed = this.mainStack.pop();
    if (removed === this.getMin()) {
      this.minStack.pop();
    }
    return removed;
  }

  peek() {
    return this.mainStack[this.mainStack.length - 1];
  }

  getMin() {
    return this.minStack[this.minStack.length - 1];
  }

  size() {
    return this.mainStack.length;
  }
}

// Example usage
const stack = new MinStack();
stack.push(5);
stack.push(3);
stack.push(7);
console.log(stack.getMin()); // 3
stack.pop();
console.log(stack.getMin()); // 3
stack.pop();
console.log(stack.getMin()); // 5

```
