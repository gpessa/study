## Exercise

Write a sum method which will work properly when invoked using either syntax below.

```js
console.log(sum(2, 3)); // Outputs 5
console.log(sum(2)(3)); // Outputs 5
```

#### Answer

```js
function sum(x) {
  if (arguments.length == 2) {
    return arguments[0] + arguments[1];
  } else {
    return function(y) {
      return x + y;
    };
  }
}
```

## Exercise

What will be the output of the following code:

```js
for (var i = 0; i < 5; i++) {
  setTimeout(function() {
    console.log(i);
  }, i * 1000);
}
```

#### Answer

It will display 5, 5, 5, 5, and 5.
The reason for this is that each function executed within the loop will be executed after the entire loop has completed and all will therefore reference the last value stored in i, which was 5.

A way to make it running correctly is using a closure:

```js
for (var i = 0; i < 5; i++) {
  (function(x) {
    setTimeout(function() {
      console.log(x);
    }, x * 1000);
  })(i);
}
```

## Exercise

```js
(function() {
  try {
    throw new Error();
  } catch (x) {
    var x = 1,
      y = 2;
    console.log(x);
  }
  console.log(x);
  console.log(y);
})();
```

#### Answer

```js
1;
undefined;
2;
```

`var` statements are hoisted (without their value initialization) to the top of the global or function scope it belongs to, even when it’s inside a with or catch block. However, the error’s identifier is only visible inside the catch block. It is equivalent to:

```js
(function() {
  var x, y; // outer and hoisted
  try {
    throw new Error();
  } catch (x /* inner */) {
    x = 1; // inner x, not the outer one
    y = 2; // there is only one y, which is in the outer scope
    console.log(x /* inner */);
  }
  console.log(x);
  console.log(y);
})();
```

## Exercise

```js
```

#### Answer

## Exercise

```js
```

#### Answer
