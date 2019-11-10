## CSS Behind the Scene

```yml
Load HTML --> Parse HTML --------------------------> Document Object Model (DOM)
                 |                                             |
                 ˇ                                             ˇ
              Load CSS   ------ Parse CSS ---------> CSS Object Model (CSSOM)
                         (resolve conflicts-cascade)           |
                            (process CSS values)               |
                                                               |
                                                               ˇ
                                                         Render tree
                                                               |
                                                               ˇ
                                                       Website rendering
                                                   (visual formatting model)
```

## `resolve conflicts-cascade`

> Process of combining different stylesheets and resolving conflicts between different CSS rules and declarations, when more than one rule applies to a certain element.

```yml
 ==========================================================================
|  IMPORTANCE (WEIGHT) ---------> SPECIFICITY ----------> SOURCE ORDER     |
 ==========================================================================
|  1. User `!important`         1. Inline styles        > Last declaration |
|  2. Author `!important`       2. IDs                    in the code      |
|  3. Author declarations       3. (pseudo)classes        will win.        |
|  4. User declarations         4. (pseudo)elements                        |
|  5. Default Browser decl.                                                |
 ==========================================================================
```

## `process CSS values`

> How browser translates `rem`, `%` etc. on `px`.

```yml
            1. Declared value 
          (author declarations)

            2. Cascaded value 
           (after the cascade)

            3. Specified value
 (defaulting, if there is no cascade value)

            4. Computed value
  (converting relative values to absolute)

            5. Used value
  (final calculations, based on layout)

            6. Actual value
     (browser and device restrictions)

```

### 4.Computed value -> 5.Used value

```yml
% (fonts)    : x% * parents computed font-size
% (lenghts)  : x% * parents computed width

em (font)    : x * parent computed font size              /*            */
em (lengts)  : x * current element computed font-size     /* FONT BASED */
rem          : x * root computed font-size                /*            */

vh           : x * 1% of viewport height                  /*  VIEWPORT  */
vw           : x * 1% of viewport width                   /*   BASED    */
```

> Every CSS property **must** have a value. If nothing is declared or inherited then initial value is used.

> Browser specify a root font size for each page (usually 16px).

## Inheritance in CSS

```yml
   if there is none cascaded value 

                &&

   (
      if the property inherited  =>  **computed** value of parent element is used
        (depends on element)

      else                       =>  **initial** value is used (depends on element)
   )
```

> Usually properties related to fonts are inherited (`font-family`, `font-size` etc.)

> The computed value of a parent property is inherited, **not** the declared value.

> `inherit` keyword forces inheritance on a certain property.

> `initial` keyword resets a property to its initial value. 

### Usage `rem`

```scss
html {
    font-size: 62.5%; // 10px
}
```
> `rem` is computed on root element. Now 1 `rem` would be 10px.

> 10/16=0.625 - in order to have root font size of 10px.

## Website rendering (visual formatting model)

> Algorithm that calculates boxes and determines the layout of these boxes, for each element in the render tree, in order to determine the final layout of the page. Depends on:

- Dimensions of boxes: the box model
- Box type: `inline`, `block` and `inline-block`
- Positioning scheme: `floats` and positioning
- Stacking contexts;

### Box model

> Every element on the web page is in the form of a box. Box contains:

```yml
- margin -              // space between boxes
| border |              // around padding and content
- padding -             // space around content, inside box
  CONTENT <- width ->   // text, images etc.
  CONTENT ^ height ˇ
```

> FILL AREA - content + padding + border: used in background selectors

#### `box-sizing`

- `content-box` (default)
> total width = right border + right padding + specified width + left padding + left border

- `border-box`
> total width = specified width

### Box Types

#### `block`
- 100% of parent's width
- vertically layed
- `block`, `flex`, `list-item`, `table`

#### `inline`
- occupies only content's space
- no line breaks
- no heights and widths
- padding and margin only horizontal 

#### `inline-block`
- occupies only content space
- no line breaks
- box-model as `block`

### Positioning Schemes 

#### Normal flow (default)
- `relative`
- Elements laid out according to source order;
- **NOT** floated;
- **NOT** absolutely positioned;

#### Floats
- `float:left`, `float:right`
- **Element is removed from the normal flow**
- Impact on surrounding content or elements;

> Parent thatn contains only floated elements is set height to 0 (parent collapsing). 
In order to fix this - `clearfix`.

```css
.clearfix::after {
    content: "";
    clear: both;
    display: table;
}
```

#### Absolutes
- `position: absolute`, `position: fixed`
- **Element is removed from the normal flow**
- **NO** impact on surrounding content or elements;

### Stacking context
- which element is in front
- `z-index` 

## BEM (Block Element Modifier)

```css
.block__element--modifier {}
```

- Block		: standalone component that its meaningful on its own
- Element	: part of a block that has no standalone meaning
- Modifier 	: a different version of a block **or** an element

## Basic principles of Responsive design

- Fluid grids and layouts (float, flexbox, css grid)
- Flexible/responsive images
- Media queries

## Appendix
### CSS naming

```css
/*selector*/ .my-class { /* declaration block */
                 color: blue;
                 text-align: center; /* declaration */
/*property*/     font-size: 20px; /* delcared value */
             }
```

### Origin of different css

- Author (our css)
- User (e.g. change of input size)
- Browser (e.g. color of link href)

### Example of cascading calculation

```css
/* (0, 0, 1, 0)
.button {  
    color: blue
}

/* (0, 1, 2, 2)
nav#nav div.pull-right .button {
    color: blue
}

/* (0, 0, 0, 1)
a {
    color: blue
}

/* (0, 1, 2, 1)
#nav a.button:hover {
    color: blue
}

```
> winner is (0, 1, 2, 2)
> A selector with 1 ID is more specific than the one with 1000 classes.
> A selector with 1000 classes is more specific than the one with 1000 elements.
> Universal selector `*` has no value (0,0,0,0).
> Always rely on specificity rather than order.


### Universal selector
```css
* { /* used on every element on the page */
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}
```

### `box-sizing`
> If padding and border is included to the total width and height of the element.

- `content-box`	: default, padding and border not included;
- `border-box`	: padding and border included;

### Fonts
`<link href="https://fonts.googleapis.com/css?family=Lato:100,300,400,700,900" rel="stylesheet">`

```css
body {
  font-family: "Lato", sans-serif;
  font-weight: 400;
  font-size: 16px;
  line-height: 1.7;
  color: #777;
  padding: 30px; /* border for body */
  box-sizing: border-box;
}
```

#### `font-weight`
- 100
- 400
- normal
- 700
- bold
- 900

#### `line-height`
- normal 
- px
- %
- number

### `vh` `vw`
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

### Background

#### `background-size`
- auto auto	: the background image will retain its original size;
- px px		: horizontal and vertical size in px;
- % %		: horizontal and vertical size in % (unexpected results);
- contain	: will resize the background image to make sure it remains fully **visible**;
- cover		: will resize the background image to make sure the element is fully **covered**;

#### `linear-gradient`
`background-image: linear-gradient(direction, color-stop1, color-stop2, ...);`

#### `clip-path`
> Creates a clipping region that sets what part of an element should be shown. Parts that are inside the region are shown, while those outside are hidden.

> [clip-path examples](https://developer.mozilla.org/en-US/docs/Web/CSS/clip-path)

> [clippy](https://bennettfeely.com/clippy/)




## Sources
[1]:[Advanced CSS cource](https://github.com/jonasschmedtmann/advanced-css-course)
[2]:[HTML Standard - text level semantics](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-var-element)
[3]:[HTML semantics](https://html.spec.whatwg.org/multipage/text-level-semantics.html#the-var-element)

