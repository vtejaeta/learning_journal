# Promise.resolve()

This static method is used to convert a given value to `promise`. Here is how it behaves in different cases:

### 1. If value is native promise:

- `Promise.resolve(value)` will return same promise without any changes

```js
let promiseObject = new Promise((resolve, reject) => {
  resolve("Hello");
});

let resolvedPromise = Promise.resolve(promiseObject);

console.log(promiseObject === resolvedPromise); // true (both are same promise)
```

<br>

### 2. If value is a thenable (an object that has a `then()` method):

- `Promise.resolve(value)` will treat it like a promise. It will call
  <br>

### 3. If value is neither a promise nor a thenable (like a regular value):

- `Promise.resolve(value)` will wrap value in a resolved promise, meaning the promise is immediately fulfilled with that value

```js
let value = 11;

Promise.resolve(value).then((result) => {
  console.log(result); // 11
});
```

<br>

> [!CAUTION]
> If evaluating the `value` expression may synchronously throw an error, this error won't be caught and wrapped in a rejected promise by `Promise.resolve()`. Consider using `Promise.try(() => value)` in this case.

```js
function throwError() {
  throw new Error("Synchronous Error!");
}

Promise.resolve(throwError()); // callbacks of `then` and `catch` method will not be invoked
```

Since the value passed to `Promise.resolve()` causes error during evaluation (i.e., it throws error before promise is actually created), `Promise.resolve()` will not be able to handle or catch that error. The error will propagate immediately and won't result in a rejected promise.
