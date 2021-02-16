## Exercise

Find the 3 numbers on an array that give the sum of something

```js
var findNumbers = (arr, tot) => {
  for (var i = 0; i <= arr.length; i++) {
    for (var j = i + 1; j <= arr.length; j++) {
      for (var k = j + 1; k <= arr.length; k++) {
        const sum = arr[i] + arr[j] + arr[k];

        if (sum === tot) {
          return [arr[i], arr[j], arr[k]];
        }
      }
    }
  }
};

findNumbers([1, 4, 6, 10, 20, 21], 26);
```
