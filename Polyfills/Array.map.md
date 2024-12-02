## Definition

The `map()` method on `Array` instances creates a new array populated with result of calling a provided function on every element in the calling array

```js
const array = [1, 4, 9, 16];

// Pass a function to map
const map = array.map((x) => x * 2);

console.log(map);
// Expected output: Array [2, 8, 18, 32]
```

## Edge Cases

#### 1. Sparse Arrays(Holes):

When the array has missing elements, `map` skips them during iteration:

```js
const sparse = [1, , 3];
const result = sparse.map((eachElement) => (eachElement || 0) * 2);

console.log(result);
// Expected output: [2, <1 empty item>, 6]
```

#### 2. Non-Function Callback

If the callback is not a function, `map` throws `TypeError`:

```js
try {
  [1, 2, 3].map(null);
} catch (error) {
  console.log(error.message);

  // Expected output: "null is not a function"
}
```

#### 3. `undefined` or `null` as `this`

If `map` is called on `null` or `undefined`, it throws a `TypeError`:

```js
try {
  Array.prototype.map.call(null, (eachElement) => eachElement);
} catch (error) {
  console.log(error.message);

  // Expected output: "Array.prototype.map called on null or undefined"
}
```

## Implementation

```js
if (!Array.prototype.map) {
  Array.prototype.map = function (callback, thisArg) {
    if (this == null) {
      throw new TypeError(`Array.prototype.map called on null or undefined`);
    }

    if (typeof callback !== "function") {
      throw new TypeError(`${callback} is not a function`);
    }

    const result = [];

    for (let index = 0; index < this.length; index++) {
      if (Object.prototype.hasOwnProperty.call(this, index)) {
        const mappedValue = callback.call(thisArg, this[index], index, this);

        result.push(mappedValue);
      }
    }

    return result;
  };
}
```
