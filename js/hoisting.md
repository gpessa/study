## Hoisting

Hoisting is JavaScript's default behavior of moving all declarations to the top of the current scope (to the top of the current script or the current function).

When we do something like:

```javascript
var foo = "bar";
```

Two things happen:

- A variable is declared/created
- A value is assigned

Hosting means that all the declaration are moved on top so you can access them at any point inside the scope.
Hosting works with functions too.

Let see what happen in case of anonymous functions:

```javascript
console.log(a());

var a = function() {
  var foo = "bar";
  return foo;
};
```

Whith this kind of function we do not have hosting and the code above would not work. Given that hosting slow down performance this could be a way to improve performance

#### Sample

```javascript
console.log(foo);

var foo;
```

This code do not create an error. The browser get the declaration on top and I get an undefined and not an error

#### Sample

```javascript
foo = "bar";

console.log(d);

var foo;
```

In this case too things work despite the weird look of it.
The declaration is moved on the top and the code is valid.

#### Sample

```javascript
foo = "bar";

console.log(d);

var foo;
```

In this case too things work despite the weird look of it.
The declaration is moved on the top and the code is valid.

#### Sample

```javascript
console.log(foo());

function foo() {
  console.log("bar");
}
```

Also in this case the code is valid. Createing a function with a certain name follow the same pattern of declaration and assignment.

#### Important

- Variables and constants declared with let or const are not hoisted!
- To avoid bugs, always declare all variables at the beginning of every scope.
- Hoisting, because of the moving, slow down the performance of a browser
