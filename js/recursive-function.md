## Exercise

Write a function called power which takes in a base and an exponent. If the exponent is 0, return 1.

#### Sample

```js
SAMPLE: power(2, 4); // 16
power(2, 3); // 8
power(2, 2); // 4
power(2, 1); // 2
power(2, 0); // 1
```

#### Answer

```js
function power(base, exp) {
  if (exp === 0) return 1;
  return base * power(base, --exp);
}
```

## Exercise

Write a function that returns the factorial of a number.
As a quick refresher, a factorial of a number is the result of that number multiplied by the number before it, and the number before that number, and so on, until you reach 1.
The factorial of 1 is just 1.

#### Sample

```js
factorial(5); // 5 * 4 * 3 * 2 * 1 === 120
```

#### Answer

```js
function factorial(value) {
  if (value === 1) return 1;
  return value * factorial(--value);
}
factorial(5);
```

## Exercise

Write a function called all which accepts an array and a callback and returns true if every value in the array returns true when passed as parameter to the callback function

#### Sample

```js
var allAreLessThanSeven = all([1, 2, 9], function(num) {
  return num < 7;
}); // false
```

#### Answer

```js
function all([value, ...values], test) {
  if (!test(value)) return false;
  if (values.length === 0) return true;
  return all(values, test);
}
var allAreLessThanSeven = all([1, 2, 3], function(num) {
  return num < 7;
});
```

## Exercise

Write a function called productOfArray which takes in an array of numbers and returns the product of them all

#### Sample

```js
var six = productOfArray([1, 2, 3]); // 6
var sixty = productOfArray([1, 2, 3, 10]); // 60
```

#### Answer

```js
function productOfArray(array) {
  if (array.length === 0) return 1;
  return array.shift() * productOfArray(array);
}
productOfArray([1, 2, 3, 10]); // 60
```

## Exercise

Write a function called contains that searches for a value in a nested object. It returns true if the object contains that value.

#### Sample

```js
var nestedObject = {
  data: {
    info: {
      stuff: {
        thing: {
          moreStuff: {
            magicNumber: 44,
            something: "foo2"
          }
        }
      }
    }
  }
};

var nestedObject = {
  data: {
    info: {
      stuff: {
        thing: {
          moreStuff: {
            magicNumber: 44,
            something: "foo2"
          }
        }
      }
    }
  }
};
let hasIt = contains(nestedObject, 44); // true
let doesntHaveIt = contains(nestedObject, "foo"); // false
```

#### Answer

```js
var nestedObject = {
  data: {
    info: {
      stuff: {
        thing: {
          moreStuff: {
            magicNumber: 44,
            something: "foo2"
          }
        }
      }
    }
  }
};

function contains(obj, valueToSearch) {
  const isObject = typeof obj === "object";
  if (isObject) {
    for (var key in obj) {
      const result = contains(obj[key], valueToSearch);
      if (result) return true;
    }
  } else {
    return obj === valueToSearch;
  }
  return false;
}
contains(nestedObject, 44); // true
contains(nestedObject, "foo"); // false
```
