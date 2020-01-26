## Closures

Accessing variables outside of the immediate lexical scope creates a closure. In other words, **_a closure is formed when a nested function is defined inside of another function, allowing access to the outer functions variables_**. Returning the nested function allows you to maintain access to the local variables, arguments, and inner function declarations of its outer function. This encapsulation allows us to hide and preserve the execution context from outside scopes while exposing a public interface and thus is subject to further manipulation. A simple example of this looks like the following:

```javascript
function foo() {
  var localVariable = "private variable";
  return function() {
    return localVariable;
  };
}

var getLocalVariable = foo();
getLocalVariable(); // "private variable"
```

### Module pattern

One of the most popular types of closures is what is widely known as the module pattern; it allows you to emulate public, private, and privileged members:

```javascript
var Module = (function() {
  var privateProperty = "foo";

  function privateMethod(args) {
    // do something
  }

  return {
    publicProperty: "",

    publicMethod: function(args) {
      // do something
    },

    privilegedMethod: function(args) {
      return privateMethod(args);
    }
  };
})();
```

### Immediately-invoked function expression (IIFE)

Another type of closure is what is called an immediately-invoked function expression (IIFE) which is nothing more than a self-invoked anonymous function executed in the context of the window:

```javascript
(function(window) {
  var foo, bar;

  function private() {
    // do something
  }

  window.Module = {
    public: function() {
      // do something
    }
  };
})(this);
```

This expression is most useful when attempting to preserve the global namespace as any variables declared within the function body will be local to the closure but will still live throughout runtime. This is a popular means of encapsulating source code for applications and frameworks, typically exposing a single global interface in which to interact with: `window.Module`
