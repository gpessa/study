## Exercise

Create a simple form validation functionality

```js
const validateValue = (value, rules) =>
  rules
    .reduce((results, rule) => [...results, rule(value)], [])
    .filter((results) => results !== true);

const getFormValue = (form) =>
  Array.from(new FormData(form)).reduce(
    (values, [key, value]) => ({
      ...values,
      [key]: value,
    }),
    {}
  );

const required = (value) => (value ? true : "This field is required");

const min = (length) => (value) =>
  value && value.length >= length ? true : "The field is too short";

const addError = (input, errors) => {
  if (errors.length === 0) return;

  const name = input.getAttribute("name");
  const error = document.createElement("div");
  error.id = `error_${name}`;
  error.className = "error";
  error.innerHTML = errors[0];
  input.insertAdjacentElement("afterend", error);
};

const removeError = (input) => {
  const name = input.getAttribute("name");
  const error = document.querySelector(`#error_${name}`);
  if (error) {
    error.remove();
  }
};

const formValidator = ({ form, rules }) => {
  const formElement = document.querySelector(form);

  Object.keys(rules).forEach((name) => {
    const input = document.querySelector(`[name='${name}']`);

    input.addEventListener("change", ({ currentTarget }) => {
      const errors = validateValue(input.value, rules[name]);
      addError(input, errors);
    });

    input.addEventListener("focus", () => removeError(input));
  });

  formElement.addEventListener("submit", (evt) => {
    const hasErrors = Object.keys(rules).reduce((result, name) => {
      const input = document.querySelector(`[name='${name}']`);
      const errors = validateValue(input.value, rules[name]);
      addError(input, errors);

      if (errors.length > 0) {
        return true;
      }
    }, false);

    if (hasErrors) {
      evt.preventDefault();
    }
  });
};

formValidator({
  form: "#loginForm",
  rules: {
    name: [required],
    password: [required, min(6)],
  },
});
```

```html
<form id="loginForm">
  <label class="field">
    Name
    <input class="field__controll" placeholder="type your name" name="name" />
  </label>

  <label class="field">
    Password
    <input
      class="field__controll"
      placeholder="type your password"
      name="password"
      type="password"
    />
  </label>

  <button type="submit" class="button">Send</button>
</form>
```

```css
.error {
  color: red;
  font-size: 0.7rem;
  text-transform: uppercase;
  margin-top: 0.2rem;
}

.field {
  display: block;
  margin-bottom: 1rem;
}

.field__controll {
  box-sizing: border-box;
  width: 100%;
  border: 2px solid solid;
  border-radius: 0;
  padding: 0.5rem 0.8rem;
}

.button {
  padding: 0.5rem 0.8rem;
  display: block;
  text-transform: uppercase;
  width: 100%;
}
```
