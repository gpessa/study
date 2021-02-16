## Calculate Fibonacci

1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, ...

To remember that:

`F(n) = F(n-1) + F(n-2)`

#### My Answer

```js
function fibonacci(num) {
  const arr = [0, 1];
  while (num >= 2) {
    arr.push(arr[arr.length - 2] + arr[arr.length - 1]);
    num--;
  }
  return arr[arr.length - 2] + arr[arr.length - 1];
}
```

#### Answer

This solution is an evolution of the previous one. If you try to optimize you find out you don't need an array to store the data:

```js
function fibonacci2(num) {
  var last = 1;
  var previous = 0;

  while (num >= 2) {
    var temp = last;
    last = previous + last;
    previous = temp;
    num--;
  }
  return last + previous;
}
```

#### Answer Recursive

```js
function fibonacci(num) {
  if (num <= 1) return 1;
  return fibonacci(num - 1) + fibonacci(num - 2);
}
```
