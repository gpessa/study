## Strict mode

Strict mode makes several changes to normal JavaScript semantics:

- `Eliminates some JavaScript silent errors` by changing them to throw errors. It prevents, or throws errors, when relatively "unsafe" actions are taken (such as gaining access to the global object).
- Fixes mistakes that make it difficult for JavaScript engines to `perform optimizations`: strict mode code can sometimes be made to run faster than identical code that's not strict mode.
- `Prohibits some syntax` likely to be defined in future versions of ECMAScript. Words like: `implements`, `interface`, `let`, `package`, `private`, `protected`, `public`, `static`, `yield` can't be used as name of variables or functions

#### Example

Silent failing assignments will throw error in strict mode

```js
NaN = 5; // error
```

#### Example

Using an object, without declaring it, is not allowed:

```js
"use strict";
x = 3.14;
```

#### Example

Deleting a variable (or object) is not allowed.

```js
"use strict";
var x = 3.14;
delete x;
```

#### Example

Writing to a get-only property is not allowed:

```js
"use strict";
var obj = {
  get x() {
    return 0;
  }
};
obj.x = 3.14; // This will cause an error
```

#### Example

Deleting an undeletable property is not allowed:

```js
"use strict";
delete Object.prototype; // This will cause an error
```
