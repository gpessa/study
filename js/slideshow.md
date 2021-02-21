## Strict mode

Create a photo carousel using the large photos linked from the thumbnails currently in the page. Some ideas you may consider: include an automatic slideshow mode, add prev/next buttons to manually controll the carousel, add a layer that shows the contents of the images alt text.

```html
<div class="carousel">
  <ul class="carousel__list">
    <li class="carousel__item">
      <figure class="carousel__figure">
        <img
          class="carousel__item__image"
          src="https://picsum.photos/900/300?a=1"
        />
        <figcaption class="carousel__item__figcaption">Bill murray 1</figcaption>
      </figure>
    </li>
    <li class="carousel__item">
      <figure class="carousel__figure">
        <img
          class="carousel__item__image"
          src="https://picsum.photos/900/300?a=2"
        />
        <figcaption class="carousel__item__figcaption">Bill murray 2</figcaption>
      </figure>
    </li>
    <li class="carousel__item">
      <figure class="carousel__figure">
        <img
          class="carousel__item__image"
          src="https://picsum.photos/900/300?a=3"
        />
        <figcaption class="carousel__item__figcaption">Bill murray 3</figure>
    </li>
  </ul>
  <button class="carousel__button carousel__button--prev">PREV</button>
  <button class="carousel__button carousel__button--next">NEXT</button>
</div>
```

```css
body {
  margin: 100px auto;
  width: 980px;
  border: 1px solid;
  padding: 10px;
}

.carousel {
  width: 100%;
  padding-bottom: 33%;
  position: relative;
  overflow: hidden;
}

.carousel__list {
  list-style-type: none;
  margin: 0;
  padding: 0;
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  display: flex;
  transition: transform 0.5s;
}

.carousel__figure,
.carousel__item {
  margin: 0;
  padding: 0;
  flex: 0 0 100%;
  width: 100%;
  position: relative;
}

.carousel__item__image {
  width: 100%;
}

.carousel__item__figcaption {
  position: absolute;
  bottom: 0;
  left: 0;
  background: white;
  z-index: 1;
  text-transform: uppercase;
  padding: 1rem;
}

.carousel__button {
  position: absolute;
  top: 50%;
  background: white;
  border-radius: none;
  border-color: none;
}

.carousel__button--prev {
  left: 0;
}

.carousel__button--next {
  right: 0;
}
```

```js
function moveSlideshowToIndex(element, total, index) {
  const n = (index % total) * -1;
  element.style.transform = `translateX(${n * 100}%)`;
}

function slideshow({ selector, initialIndex, autoscroll }) {
  var current = initialIndex || 0;
  const slideshow = document.querySelector(selector);
  const slides = document.querySelector(".carousel__list");
  const total = slideshow.querySelectorAll(".carousel__item").length;

  const prev = slideshow.querySelector(".carousel__button--prev");
  const next = slideshow.querySelector(".carousel__button--next");

  next.addEventListener("click", () => {
    current = current + 1;
    moveSlideshowToIndex(slides, total, current);
  });

  prev.addEventListener("click", () => {
    current = current - 1;
    moveSlideshowToIndex(slides, total, current);
  });

  if (!autoscroll) return;

  setInterval(() => {
    current = current + 1;
    moveSlideshowToIndex(slides, total, current);
  }, 3000);
}

slideshow({
  selector: ".carousel",
  autoscroll: true,
});
```
