## Universal selector
```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

## `box-sizing`
> If padding and border is included to the total width and height of the element.

- `content-box`	: default, padding and border not included;
- `border-box`	: padding and border included;

## Fonts
`<link href="https://fonts.googleapis.com/css?family=Lato:100,300,400,700,900" rel="stylesheet">`

```css
body {
  font-family: "Lato", sans-serif;
  font-weight: 400;
  font-size: 16px;
  line-height: 1.7;
  color: #777;
  padding: 30px; /* border for body */
}
```

### `font-weight`
- 100
- 400
- normal
- 700
- bold
- 900

### `line-height`
- normal 
- px
- %
- number

## `vh` `vw`
- `vh`	: view height in %
- `vw`  : view width in %

```css
.header {
  height: 95vh;
  background-image: linear-gradient(to right bottom, grey, blue), url(../img/foo.png);
  background-size: cover;
  background-position: top;
  clip-path: polygon(0 0, 100% 0, 100% 75vh, 0 100%); /* xy */
}
```

> Size can't be bigger than % of the view.

## Background

### `background-size`
- auto auto	: the background image will retain its original size;
- px px		: horizontal and vertical size in px;
- % %		: horizontal and vertical size in % (unexpected results);
- contain	: will resize the background image to make sure it remains fully **visible**;
- cover		: will resize the background image to make sure the element is fully **covered**;

### `linear-gradient`
`background-image: linear-gradient(direction, color-stop1, color-stop2, ...);`

### `clip-path`
> Creates a clipping region that sets what part of an element should be shown. Parts that are inside the region are shown, while those outside are hidden.

> [clip-path examples](https://developer.mozilla.org/en-US/docs/Web/CSS/clip-path)

> [clippy](https://bennettfeely.com/clippy/)


## Sources
[1]:[Advanced CSS cource](https://github.com/jonasschmedtmann/advanced-css-course)

