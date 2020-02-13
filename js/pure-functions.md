## Pure functions

A function is a process which takes some input, called arguments, and produces some output called a return value. Functions may serve the following purposes:

- **Mapping**: Produce some output based on given inputs. A function maps input values to output values.
- **Procedures**: A function may be called to perform a sequence of steps. The sequence is known as a procedure, and programming in this style is known as procedural programming.
- **I/O**: Some functions exist to communicate with other parts of the system, such as the screen, storage, system logs, or network.

#### What is a pure function

A pure function is a function which:

- Given the same input, will always return the same output.
- Produces no side effects.

##### Produce no side effects

If a function were to mutate a property on an object or array parameter, that would mutate state that is accessible outside the function this would violate the pure function requirement. Pure functions must not mutate external state.

```js
const addToCart = (cart, item, quantity) => {
  cart.items.push({
    // We mutate the external array
    item,
    quantity
  });
  return cart;
};
```
