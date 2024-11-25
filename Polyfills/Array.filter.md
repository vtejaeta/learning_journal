# Definition

The `filter()` method on `Array` instances creates a shallow copy of a portion of given array, filtered down to just the elements from the given array that pass the test implemented by the provided function.

```js
const words = [` spray`, `elite`, `exuberant`, `destruction`, `present`];

const result = words.filter((word) => word.length > 6);

console.log(result);
// Expected output: Array ["exuberant", "destruction", "present"]
```

## Edge Cases

#### 1. Non-Function Callback

If the callback is not a function, `filter` throws `TypeError`:

```js
try {
  [1, 2, 3].filter(null);
} catch (error) {
  console.log(error.message);

  // Expected output: "null is not a function"
}
```

#### 2. `undefined` or `null` as `this`

If `filter` is called on `null` or `undefined`, it throws a `TypeError`:

```js
try {
  Array.prototype.filter.call(null, (eachElement) => eachElement);
} catch (error) {
  console.log(error.message);

  // Expected output: "Array.prototype.filter called on null or undefined"
}
```

## Implementation

```js
if (!Array.prototype.filter) {
  Array.prototype.filter = function (callback, thisArg) {
    if (this == null) {
      throw new TypeError(`Array.prototype.filter called in null or undefined`);
    }

    if (typeof callback !== "function") {
      throw new TypeError(`${callback} is not a function`);
    }

    const result = [];

    for (let index = 0; index < this.length; index++) {
      if (Object.prototype.hasOwnProperty.call(this, index)) {
        const isTruthyValue = callback.call(thisArg, this[index], index, this);

        if (isTruthyValue) {
          result.push(this[index]);
        }
      }
    }

    return result;
  };
}
```
