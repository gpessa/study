## Reect Hooks

### useState

How to use it:

```js
const [value, setValue] = useState(initialValue);
```

#### Expensive initial value

In case I need to provide an expensive initial value, and calculating only once on component init, I can use this:

```js
const expensiveInitialValue = () => {
    return ....
}
const [value, setValue] = useState(() => expensiveInitialValue))
```

#### Getting previous value

I can easily retrieve the previous value in this way:

```js
<button onClick={() => setValue(oldValue => oldValue + 1)}>Add one</button>
```

### useEffect

How to use it:

```js
const [value, setValue] = useEffect(() => {
  // this is called every time the component is re-rendered
});
```

How to call the function on each render

```js
const [value, setValue] = useEffect(() => {
  // this is called only the first time the component is rendered
}, []);
```

How to pass some dependencies:

```js
const [value, setValue] = useEffect(() => {
  // this is called only when value is updated
}, [value]);
```

### useRef

Create a reference that can use to interact with a html element.

```js
function TextInputWithFocusButton() {
  const inputEl = useRef(null);

  const onButtonClick = () => {
    inputEl.current.focus(); // `current` points to the mounted text input element
  };

  return (
    <>
      <input ref={inputEl} type="text" />
      <button onClick={onButtonClick}>Focus the input</button>
    </>
  );
}
```

### useLayoutEffect

Is like the useEffect but the function is called after the dom is updated.

### useCallback

It's a difficult one :)
It can be used with functional component that use `React.memo`.
`React.memo` can be used to create simple presentational components, with memo, those component can be cached and they are re-rendered only of `props` change.
If I pass a callback function to those component, the function usually change each time the parent is re-render. in order not to do that I can wrap the callback with `useCallback`, in this way we prevent the re-rendering.
