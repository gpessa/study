## Exercise

Create a simple form validation functionality

```js
const form = document.querySelector('#form')

const { required, minValue, maxValue } = {
  required: (val) => !!!val && 'Field is required',
  minValue: (min) => (val) => !(!!val && (Number(val) > Number(min))) && `Field value should be at least ${min}`,
  maxValue: (max) => (val) => !(!!val && (Number(val) < Number(max))) && `Field value should be max ${max}`,
}

const rules = {
	username: [
    required
  ],
  password: [
		required,
    minValue(3)
	]
}

const validateField = (field, value, rules) => {
  const errors = rules.map(rule => rule(value)).filter(value => value !== false)
  const hasErrors = errors.length > 0
  field.classList[hasErrors ? 'add' : 'remove']('error')

  const previousError = field.parentNode.querySelector(`.error-item`)

  if (previousError) {
    previousError.parentNode.removeChild(previousError);
  }

  if (hasErrors) {
    const errorElement = document.createElement("p")
    errorElement.classList.add('error-item')
    errorElement.innerHTML = errors[0]; 
    field.insertAdjacentElement('afterend', errorElement);
  }
}

const validate = (form, rules) => {
	form.addEventListener('submit', (evt) => {
		evt.preventDefault()
    var data = new FormData(form);
		
		Object.keys(rules).map(name => {
      const field = form.querySelector(`[name='${name}']`)
			const value = data.get(name)
			const fieldRules = rules[name]
			
			validateField(field, value, fieldRules)
		})
	})

  Object.keys(rules).map(name => {
    const field = form.querySelector(`[name='${name}']`)
    const fieldRules = rules[name]
    
		field.addEventListener('change', () => {
    	const data = new FormData(form);
    	const value = data.get(name)
			validateField(field, value, fieldRules)
    })
  })
}


validate(form, rules)
```

```html
<form id="form">
  <div>
    <label for="uname"><b>Username</b></label>
    <input type="text" placeholder="Enter Username" name="username">
  </div>
  <div>
    <label for="psw"><b>Password</b></label>
    <input type="password" placeholder="Enter Password" name="password">
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