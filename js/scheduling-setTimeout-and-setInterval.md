## Scheduling: setTimeout and setInterval

We may decide to execute a function not right now, but at a certain time later. That’s called “scheduling a call”.

There are two methods for it:

- `setTimeout`
- `setInterval`

#### Nested setTimeout

```js
/** instead of:
let timerId = setInterval(() => alert('tick'), 2000);
*/

let timerId = setTimeout(function tick() {
  alert('tick');
  timerId = setTimeout(tick, 2000); // (*)
}, 2000
```

The nested setTimeout is a more flexible method than setInterval. This way the next call may be scheduled differently, depending on the results of the current one.

#### Zero delay setTimeout

There’s a special use case: setTimeout(func, 0), or just setTimeout(func).

This schedules the execution of func as soon as possible. But the scheduler will invoke it only after the currently executing script is complete.

So the function is scheduled to run “right after” the current script.

For instance, this outputs “Hello”, then immediately “World”:

```js
setTimeout(() => alert("World"));

alert("Hello");
```
