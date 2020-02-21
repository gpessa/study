## Exercise

Develop the data structure and javascript/html code for a table with stock info that refreshes each 5 min

#### Answer

```js
const formatPercentage = value => (value / 100).toLocaleString('en-US', { 
  style: 'percent', 
  minimumFractionDigits:2
})

const formatCurrency = value => value.toLocaleString('en-US', { 
	style: 'currency', 
  currency: 'USD' 
})

class Table {
	get intervall () {
  	return 3000
  }
  
  constructor(element) {
    this.element = element;
    this.periodicallyFetch()
  }

  async periodicallyFetch() {
    const data = await this.fetch()
    this.renderTable(data)
    setTimeout(() => this.periodicallyFetch(), this.intervall)
  }
  
  fetch() {
    return fetch(`https://financialmodelingprep.com/api/v3/quotes/crypto`)
    	.then(res => res.json())
      .then(data => data.map(({ symbol, price, changesPercentage }) => ({
        symbol,
        price: formatCurrency(price),
        changesPercentage: formatPercentage(changesPercentage)
      })))
  }

  getHeader(data) {
    return `
      <thead>
    		${Object.keys(data[0]).reduce((header, key) => header + `<th>${key}</th>`, '')}
      </thead>
    `    
  }

  getBody(data) {
    return `
			<tbody>
      	${data.map(d => `
        	<tr>
          	${Object.keys(d).reduce((body, key) => body + `<td>${d[key]}</td>`, '')}
          </tr>
       `).join('')}
      </tbody>
    `
  }

  renderTable(data) {
    this.element.innerHTML =  
      `
      	<table class="table">
      		${this.getHeader(data)}
      		${this.getBody(data)}
      	</table>
      `
  }

}

var element = document.querySelector('#output')
var car = new Table(element);
```

```css
.table {
  border: 1px solid #ccc;
  text-align: left;
}

.table td,
.table th {
  padding: 0.3rem;
}

.table tr:nth-child(even) {
  background: #CCC;
}
```


```html
<div id="output"></div>
```