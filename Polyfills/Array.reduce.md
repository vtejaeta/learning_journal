## Definition

The `reduce()` method of `Array` instances executes a user-supplied "reducer" callback function on each element of the array, in order, passing in the return value from the calculation on the preceding element. The final result of running the reducer across all elements of the array is a single value.

The first time that the callback is run there is no "return value of the previous calculation". If supplied, an initial value may be used in its place. Otherwise the array element at index 0 is used as the initial value and iteration starts from the next element (index 1 instead of index 0).

```js
const array = [1, 2, 3, 4];

const initialValue = 0;
const sumWithInitial = array.reduce(
  (accumulator, currentValue) => accumulator + currentValue,
  initialValue
);

console.log(sumWithInitial);
// Expected output: 10
```

## Edge Cases

#### 1. Non-Function Callback

If the callback is not a function, `reduce` throws `TypeError`:

```js
try {
  [1, 2, 3].reduce(null, 0);
} catch (error) {
  console.log(error.message);

  // Expected output: "null is not a function"
}
```

#### 2. Empty Array Without Initial Value

Reduce throws a `TypeError` if the array is empty and no initial value is provided

```js
try {
  [].reduce((acc, val) => acc + val);
} catch (error) {
  console.log(error.message);

  // Expected output: "Reduce of empty array with no initial value"
}
```

## Implementation

```js
if (!Array.prototype.reduce) {
  Array.prototype.reduce = function (callback, initialValue) {
    if (this == null) {
      throw new TypeError(
        `Array.prototype.reduce called on null or undefined`
      );
    }

    if (typeof callback !== "function") {
      throw new TypeError(`${callback} is not a function`);
    }

    let accumulator = initialValue;
    let startIndex = 0;

    if (arguments.length > 1) {
      accumulator = initialValue;
    } else {
      while (startIndex < this.length && !this.hasOwnProperty(startIndex)) {
        startIndex++;
      }

      if (startIndex >= this.length) {
        throw new TypeError(`Reduce of empty array with no initial value`);
      }

      accumulator = this[startIndex++];
    }

    for (let index = startIndex; index < this.length; index++) {
      if (this.hasOwnProperty(index)) {
        accumulator = callback(accumulator, this[index], index, this);
      }
    }

    return accumulator;
  };
```
