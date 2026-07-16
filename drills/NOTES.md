# JavaScript Practice Notes

## 1. What is the difference between `let` and `const`? When would you use each?

`let` is used when the value of a variable needs to change later in the program. `const` is used when the variable should not be reassigned. I use `const` by default and only use `let` when I know the value will change.

Example:

```javascript
let score = 10;
score = 20;

const name = "Angad";
// name = "Rahul"; // Error
```

---

## 2. Explain `map`, `filter` and `reduce` to someone who has never seen them.

- **map()** creates a new array by changing every item in the original array.
- **filter()** creates a new array containing only the items that match a condition.
- **reduce()** combines all the items in an array into a single value, such as a total, average, or object.

Examples:

```javascript
const numbers = [1, 2, 3];

numbers.map(n => n * 2);
// [2, 4, 6]

numbers.filter(n => n > 1);
// [2, 3]

numbers.reduce((sum, n) => sum + n, 0);
// 6
```

---

## 3. What is a closure? Use an example from your own drill code.

A closure is when a function remembers the variables from the place where it was created, even after the outer function has finished running.

Example from `makeCounter()`:

```javascript
function makeCounter() {
  let count = 0;

  return {
    increment() {
      count++;
      return count;
    },
    getValue() {
      return count;
    }
  };
}
```

The `increment()` and `getValue()` functions remember the `count` variable because of the closure.

---

## 4. What does an "immutable update" mean, and why not simply change the original array?

An immutable update means creating a new array or object instead of changing the original one. This makes the code easier to understand and helps prevent unexpected bugs. React also relies on immutable updates to detect changes and update the UI correctly.

Example:

```javascript
const students = ["Aarav", "Diya"];

const updatedStudents = [...students, "Kabir"];
```

The original `students` array stays unchanged.

---

## 5. What is the difference between `value ?? fallback` and `value || fallback`? When does it matter?

The `||` operator returns the fallback for any falsy value like `0`, `false`, `""`, `null`, or `undefined`.

The `??` operator only returns the fallback when the value is `null` or `undefined`.

Example:

```javascript
0 || 100
// 100

0 ?? 100
// 0
```

This matters when values like `0` or an empty string are valid and should not be replaced.

---

## 6. What does `await` actually do? What is the difference between doing three things one after another and doing all three at once?

`await` pauses the current async function until a Promise is completed. It makes asynchronous code easier to read.

Doing tasks one after another (sequential) waits for each task to finish before starting the next one.

```javascript
await loader(1);
await loader(2);
await loader(3);
```

Doing tasks at the same time (parallel) starts all of them together using `Promise.all()`, making the program faster.

```javascript
await Promise.all([
  loader(1),
  loader(2),
  loader(3)
]);
```

If each request takes 50 ms:

- Sequential execution takes about **150 ms**.
- Parallel execution takes about **50 ms**.

Using `Promise.all()` is usually the better choice when the tasks do not depend on each other.