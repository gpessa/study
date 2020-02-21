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

Creates a slice of array with `n` elements taken from the end.

```js
takeRight([1, 2, 3], 2);
// => [2, 3]
```

#### Answer

```js
var takeRight = (array, n) => array.slice(-n);

result = takeRight([1, 2, 3]);
```

## Exercise

This method is like `pullAll` except that it accepts an array of values to remove.
This method mutates array.

#### Sample

```js
var array = ["a", "b", "c", "a", "b", "c"];
pullAll(array, ["a", "c"]);
// => ['b', 'b']
```

#### Answer

```js
var pullAll = (array, values) => {
  for (let index = 0; index < values.length; index++) {
    const value = values[index];
    let fromIndex = 0;

    while ((fromIndex = array.indexOf(value, fromIndex)) > -1) {
      array.splice(fromIndex, 1);
    }
  }
  return array;
};

var array = ["a", "a", 1, "a", 3, "n"];

const result = pullAll(array, ["a", "c"]);
```
