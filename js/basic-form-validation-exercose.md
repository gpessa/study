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
  
const validate = (form, rules) => {
	form.addEventListener('submit', (evt) => {
		evt.preventDefault()
    var data = new FormData(form);
		
		Object.keys(rules).map(name => {
      const field = form.querySelector(`[name='${name}']`)
			const fieldRule = rules[name]
			const value = data.get(name)
			const errors = fieldRule.map(rule => rule(value)).filter(value => value !== false)
			const hasErrors = errors.length > 0
      field.classList[hasErrors ? 'add' : 'remove']('error')
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