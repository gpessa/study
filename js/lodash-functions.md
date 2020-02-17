## Exercise

Creates a duplicate-free version of an array, using SameValueZero for equality comparisons, in which only the first occurrence of each element is kept. The order of result values is determined by the order they occur in the array.

#### Sample

```js
uniq([2, 1, 2]);
// => [2, 1]
```

#### Answer

```js
function uniq(array) {
  let result = [];

  while (array.length) {
    const el = array.splice(0, 1)[0];
    if (array.indexOf(el) === -1)  && result.push(el);
  }

  return result;
}
```

## Exercise

#### Sample

```js
```

#### Answer

```js
```

If Type(x) is different from Type(y), return false.
If Type(x) is Number, then
If x is NaN and y is NaN, return true.
If x is +0 and y is -0, return true.
If x is -0 and y is +0, return true.
If x is the same Number value as y, return true.
Return false.
Return SameValueNonNumber(x, y).
