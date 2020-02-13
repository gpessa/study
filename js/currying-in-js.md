## Currying

Currying is a process in functional programming in which we can transform a function with multiple arguments into a sequence of nesting functions. It returns a new function that expects the next argument inline.

The idea behind currying is to take a function and derive a function that returns specialized function(s).

To be able to talk about currying we need 2 things:

- Currying works for functions with more than two arguments
- Currying transforms a function into a sequence of functions each taking a _single argument_ of the function.

### Arity

The term arity, refers to the number of arguments a function takes. For example:

```js
// Arity: 2
function fn(a, b) {
  //...
}
```

```js
// Arity: 3
function _fn(a, b, c) {
  //...
}
```

### What is currying with an example

Let’s look at a simple example:

```js
function multiply(a, b, c) {
  return a * b * c;
}

multiply(1, 2, 3); // 6
```

Let’s create a curried version of it

```js
function multiply(a) {
  return b => {
    return c => {
      return a * b * c;
    };
  };
}
multiply(1)(2)(3); // 6
```

### Why currying

There are many example where it's pretty useful:

**Write little code modules** that can be reused and configured with ease, much like what we do with npm.
For example to have a function that can be re-used to calculate a discounted price.

```js
function discount(discount) {
  return price => {
    return price * discount;
  };
}
const tenPercentDiscount = discount(0.1);
const twentyPercentDiscount = discount(0.2);
```

**Avoid frequently calling a function with the same argument**

### First, Implement `add(2)(3)`

A function can be passed as an argument to other functions, can be returned by another function and can be assigned as a value to a variable.
This would work only if the function is called twice

```js
function add(x) {
  return function(y) {
    return x + y;
  };
}
```

Or in ES6:

```js
const add = x => y => x + y;
```
