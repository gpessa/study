## Scope and Context

Scope pertains to the visibility of variables, and context refers to the object to which a function belongs.

First let's clear that every function invocation has both a scope and a context associated with it.
Fundamentally, scope is function-based while context is object-based.
In other words:

- Scope pertains to the variable access of a function when it is invoked and is unique to each invocation.
- Context is always the value of the this keyword which is a reference to the object that “owns” the currently executing code.

#### Scope in JavaScript

Scope has to do with the the visibility of variables. In JavaScript, scope is achieved through the use of functions. When you use the keyword “var” inside of a function, the variable that you are initializing is private to the function, and cannot be seen outside of that function. But if there are functions inside of this function, then those “inner” functions can “see” that variable, and that variable is said to be “in-scope”. Functions can “see” variables that are declared inside of them. They can also “see” any that are declared outside of them, but never those declared inside of functions that are nested in that function. This is scope in JavaScript.

### Context in JavaScript

Context is related to objects. It refers to the object to which a function belongs. When you use the JavaScript “this” keyword, it refers to the object to which function belongs.

Scope refers to the visibility of variables, and content refers to the object to which a function belongs.
For example, inside of a function, when you say: “this.accoutNumber”, you are referring to the property “accoutNumber”, that belongs to the object to which that function belongs. If the object “foo” has a method called “bar”, when the JavaScript keyword “this” is used inside of “bar”, it refers to “foo”. If the function “bar” were executed in the global scope, then “this” refers to the window object (except in strict mode). It is important to keep in mind that by using the JavaScript call() or apply() methods, you can alter the context within which a function is executed. This, in-turn, changes the meaning of “this” inside of that function when it is executed.

### Sample

```javascript
var obj = {
  foo: function() {
    return this;
  }
};
obj.foo() === obj; // true
```

### Important

ECMAScript 6 (ES6/ES2015) introduced the **let** and **const** keywords that support the declaration of block scope local variables. This means the variable will be confined to the scope of a block that it is defined in, such as an **if** statement or **for loop** and will not be accessible outside of the opening and closing curly braces of the block. This is contrary to var declarations which are accessible outside blocks they are defined in. The difference between let and const is that a const declaration is, as the name implies, constant - a read-only reference to a value. This does not mean the value is immutable, just that the variable identifier cannot be reassigned.
