## Exercise

Identify whether there exists a pair of numbers in an array such that their sum is equal to N

#### Answer

```js
var array = [12, 3, 4, 5, 6, 11, 1, 13, 8, 7, 9];
var sum = 18;

var find = (array, total) => {
  const solutions = [];

  for (var i = 0; i < array.length; i++) {
    for (var j = i; j < array.length; j++) {
      const a = array[j];
      const b = array[i];

      if (a + b === sum) {
        solutions.push([a, b]);
      }
    }
  }

  return solutions;
};

console.log(find(array, sum));
```

#### Answer

Definitely a better solution. Much faster

```js
var array = [12, 3, 4, 5, 6, 11, 1, 13, 8, 7, 9];
var sum = 18;

var find = (array, total) => {
  let hashMap = {};
  let results = [];

  for (let i = 0; i < array.length; i++) {
    if (hashMap[array[i]]) {
      results.push([hashMap[array[i]], array[i]]);
    } else {
      hashMap[total - array[i]] = array[i];
    }
  }

  return results;
};

console.log(find(array, sum));
```
