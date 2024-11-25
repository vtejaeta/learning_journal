# Closure

Definition of Closures as per MDN is as follows

> A closure is the combination of a function bundled together (enclosed) with references to its surrounding state (the lexical environment). In other words, a closure gives you access to an outer function's scope from an inner function. In JavaScript, closures are created every time a function is created, at function creation time.

<br>

Some refer `closure` as the ability of function to read/write variables that are declared outside of it.

When a closure is created, it maintains a reference to the variables in its outer function's scope. As a result, these outer variables remain in memory as long as the closure exists, even after the outer function has finished executing.

```js
function createCounter() {
  let count = 0; // This is a private variable

  return function () {
    count += 1;
    return count;
  };
}

const counter = createCounter(); // `counter` is now a closure

console.log(counter()); // Output: 1
console.log(counter()); // Output: 2
console.log(counter()); // Output: 3
```

### Application

- Some JavaScript design patterns(Module and Revealing Module Pattern) use closures to keep data private

- In Asynchronous operations, Closures help preserve the surrounding context such as timeout and event handlers.

- Closure can be used for memoization, a technique to optimize performance by caching the results of expensive function calls. The inner function can remember the results of previous calls and return the cached result if the same input is provided again.

### Drawback

- Since outer function's variables continue to exist in memory due to closure, if not handled properly they can cause memory leak. This can potentially degrade performance over time, as the garbage collector is unable to reclaim memory that's still being referenced by the closures.

- If shared variables are modified anywhere in code after closure is created, it may lead to bugs or unexpected behavior, because closure now has access to modified values, not the values they had at the time closure is created.
