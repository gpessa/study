## Exercise

```js
const elements = document.querySelectorAll("[data-tooltip]");

class Tooltip {
  constructor(elm) {
    this.elm = elm;
    this.elm.addEventListener("mouseover", this.showTooltip.bind(this));
    this.elm.addEventListener("mouseout", this.hideTooltip.bind(this));
  }

  getPosition() {
    const rect = this.elm.getBoundingClientRect();
    return {
      left: rect.left + window.scrollX + rect.width / 2,
      top: rect.top + window.scrollY + rect.height
    };
  }

  showTooltip() {
    clearTimeout(this.timeout);
    if (this.tooltip) {
      this.tooltip.parentElement.removeChild(this.tooltip);
      delete this.tooltip;
    }

    var text = this.elm.dataset.tooltip;
    var { left, top } = this.getPosition();

    this.tooltip = document.createElement("div");
    this.tooltip.classList.add("tooltip");
    this.tooltip.innerHTML = text;
    this.tooltip.style.top = `${top}px`;
    this.tooltip.style.left = `${left}px`;

    document.body.appendChild(this.tooltip);
  }

  hideTooltip() {
    this.timeout = setTimeout(() => {
      this.tooltip.parentElement.removeChild(this.tooltip);
      delete this.tooltip;
    }, 200);
  }
}

elements.forEach(elm => new Tooltip(elm));
```

```html
<!DOCTYPE html>
<html>
  <head>
    <link rel="stylesheet" href="style.css" />
  </head>

  <body>
    Lorem Ipsum is simply dummy text of the printing and typesetting industry.
    Lorem <strong data-tooltip="test">Ipsum has been</strong> the industry's
    standard dummy text ever since the 1500s, when an unknown printer took a
    galley of type and scrambled it to make a type specimen book. It has
    survived not only five centuries, but also the leap into electronic
    typesetting, remaining essentially unchanged. It was popularised in the
    1960s with the release of Letraset sheets containing Lorem Ipsum passages,
    and more recently with desktop publishing software like Aldus PageMaker
    including versions of Lorem Ipsum.
    <button data-tooltip="Ciccio e' bravo">Submit</button>
    <script src="script.js"></script>
  </body>
</html>
```

```css
.tooltip {
  display: inline-block;
  padding: 5px 10px;
  background: #ccc;
  z-index: 1;
  font-size: 70%;
  position: fixed;
  margin-top: 8px;
  transform: translateX(-50%);
}

.tooltip::before {
  content: "";
  width: 10px;
  height: 10px;
  top: -5px;
  left: 50%;
  margin-left: -5px;
  display: block;
  background: #ccc;
  position: absolute;
  transform: rotate(45deg);
  z-index: -1;
}
```
