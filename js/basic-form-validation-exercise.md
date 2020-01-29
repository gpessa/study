## Exercise

Create a simple form validation functionality

```js
const { required, minValue, maxValue } = {
  required: val => !val && `Field required`,
  minValue: min => val =>
    Number(val) < Number(min) && `Min value should be ${min}`,
  maxValue: max => val =>
    Number(val) > Number(max) && `Max value should be ${max}`
};

const rules = {
  username: [required],
  password: [required, minValue(3)]
};

const form = document.querySelector("#form");

class FormValidator {
  constructor(form, rules) {
    this.form = form;
    this.rules = rules;

    form.addEventListener("submit", evt => {
      const hasError = Object.keys(rules).reduce((valid, name) => {
        const errors = this.getFieldErrors(name);
        this.updateErrors(name, errors);
        if (errors.length) return true;
      }, false);

      hasError && evt.preventDefault();
    });

    Object.keys(rules).forEach(name => {
      const field = this.getFieldElement(name);
      field.addEventListener("input", evt => {
        const errors = this.getFieldErrors(name);
        this.updateErrors(name, errors);
      });
    });
  }

  updateErrors(name, errors) {
    const field = this.getFieldElement(name);
    const errorLabel = field.parentNode.querySelector(`.error-item`);

    field.classList.remove("error");
    errorLabel && errorLabel.parentNode.removeChild(errorLabel);

    if (errors.length) {
      const errorElement = document.createElement("p");
      errorElement.classList.add("error-item");
      errorElement.innerHTML = errors[0];
      field.classList.add("error");
      field.insertAdjacentElement("afterend", errorElement);
    }
  }

  getFieldErrors(name) {
    const value = this.getFieldValue(name);
    const rules = this.rules[name];
    const errors = rules
      .map(rule => rule(value))
      .filter(value => value !== false);
    return errors.length ? errors : false;
  }

  getFieldElement(name) {
    return this.form.querySelector(`[name='${name}']`);
  }

  getFieldValue(name) {
    var data = new FormData(this.form);
    return data.get(name);
  }
}

new FormValidator(form, rules);
```

```html
<form id="form">
  <div>
    <label>Username</label>
    <input type="text" placeholder="Enter Username" name="username" />
  </div>
  <div>
    <label>Password</label>
    <input type="text" placeholder="Enter Password" name="password" />
  </div>
  <button type="submit">Login</button>
</form>
```

```css
.error {
  border: 1px solid red;
}

.error-item {
  font-size: 0.7em;
  color: red;
}
```
