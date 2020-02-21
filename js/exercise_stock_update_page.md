## Exercise

Develop the data structure and javascript/html code for a table with stock info that refreshes each 5 min

class Table {

constructor(element) {
this.element = element;
this.periodicallyFetch()
}

async periodicallyFetch() {
const data = await this.fetch()
this.createTable(data)
setTimeout(() => this.periodicallyFetch(), 3000)
}
fetch(symbol) {
return fetch(`https://financialmodelingprep.com/api/v3/quotes/crypto`).then(response => response.json())
}

getHeader(data) {
return Object.keys(data[0]).reduce((header, key) => {
return header + `<th>${key}</th>`
}, '')
}

getRow(data) {
return Object.keys(data).reduce((header, key) => {
return header + `<td>${data[key]}</td>`
}, '')
}

    createTable(data) {
    		const table = `
    			<table>
    				<thead>
            <tr>${this.getHeader(data)}</tr>
    				</thead>
          <tbody>${data.map(d => `<tr>${this.getRow(d)}</tr>`)}</tbody>
    			</table>
    		`

    		this.element.innerHTML = table;
    	}

}

var element = document.querySelector('#output')
var car = new Table(element);
