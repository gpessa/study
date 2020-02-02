## Import/Export modules: different versions

#### CommonJS

```js
//importing
const doSomething = require("./doSomething.js");

//exporting
module.exports = function doSomething(n) {
  // do something
};
```

- Is the syntax used by node.
- Modules are imported synchronously
- When CJS imports, it will give you a copy of the imported object.

#### AMD Asynchronous Module Definition

```js
define(["dep1", "dep2"], function(dep1, dep2) {
  //Define the module value by returning a value.
  return function() {};
});
```

- AMD is made for frontend
- Modules are imported asynchronously
- Was popular when RequireJs was a thing

#### UMD Universal Module Definition

```js
(function (root, factory) {
    if (typeof define === "function" && define.amd) {
        define(["jquery", "underscore"], factory);
    } else if (typeof exports === "object") {
        module.exports = factory(require("jquery"), require("underscore"));
    } else {
        root.Requester = factory(root.$, root._);
    }
}(this, function ($, _) {
    // this is where I defined my module implementation

    var Requester = { // ... };

    return Requester;
}));
```

- Works on front and back end (hence the name universal).

#### ES Modules

```js
import React from "react";
import { foo, bar } from "./myLib";
```

```js
export default function() {
// your Function
};

export const function1() {...};
```

- Is now the standard
- ESM is the best module format thanks to its simple syntax, async nature, and tree-shakeability.
- Works in many modern browsers
- Tree-shakeable, due to ES6's static module structure
