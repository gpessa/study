## The old "var"

While `let` and `const` behave exactly the same way in terms of Lexical Environments.
But var is a very different beast, that originates from very old times.

#### 1. “var” has no block scope

Variables, declared with var, are either function-wide or global. They are visible through blocks.

```js
if (true) {
  var test = true; // use "var" instead of "let"
}

alert(test); // true, the variable lives after if
```

```js
for (var i = 0; i < 10; i++) {
  // ...
}

alert(i); // 10, "i" is visible after loop, it's a global variable
```

#### “var” declarations are processed at the function start

var declarations are processed when the function starts (or script starts for globals).

In other words, var variables are defined from the beginning of the function, no matter where the definition is (assuming that the definition is not in the nested function).

```js
function sayHi() {
  phrase = "Hello";

  alert(phrase);

  var phrase;
}
sayHi();
```

People also call such behavior “hoisting” (raising), because all var are “hoisted” (raised) to the top of the function.

We should remember that something like this:

```js
function sayHi() {
  alert(phrase);

  var phrase = "Hello";
}

sayHi();
```

is transformed in:

```js
function sayHi() {
  var phrase; // declaration works at the start...

  alert(phrase); // undefined

  phrase = "Hello"; // ...assignment - when the execution reaches it.
}

sayHi();
```

The declaration is processed at the start of function execution (“hoisted”), but the assignment always works at the place where it appears. So the code works essentially like this:
