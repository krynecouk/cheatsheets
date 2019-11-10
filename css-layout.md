## Layout Types

- Float layout 
- Flexbox
- Css Grid

## Float layout

```scss
$grid-width: 114rem; // 1140px
$gutter-vertical: 8rem;
$gutter-horizontal: 6rem;
@mixin clearfix {
  &::after {
    content: ""; // otherwise sudo element would be not rendered
    clear: both;
    display: table;
  }
}

.row {
    max-width: $grid-width
    margin: 0 auto; // center

    $:not(:last-child) {
        margin-bottom: $gutter-vertical; // last don't have to have gutter
    }

    @include clearfix;

    [class^="col-"] { // every element with attribute 'class' that starts on 'col-'
        background-color: orange;
        float: left;

        &:not(:last-child) {
            margin-right: $gutter-horizontal;
        }
    }

    .col-1-of-2 {
        width: calc((100% - #{$gutter-horizontal})/2);
    }
 
    .col-1-of-3 {
        width: calc((100% - 2 * #{$gutter-horizontal})/3);
    }

    .col-2-of-3 {
	// 2 cols with gutter
	width: calc(2 * ((100% - 2 * #{$gutter-horizontal}) / 3) + #{$gutter-horizontal});
    }

    .col-1-of-4 {
        width: calc((100% - 3 * #{$gutter-horizontal})/4);
    }

    .col-2-of-4 {
	// 2 cols with gutter
	width: calc(2 * ((100% - 3 * #{$gutter-horizontal}) / 4) + #{$gutter-horizontal});
    }

    .col-3-of-4 {
	// 3 cols with 2 gutter
	width: calc(3 * ((100% - 3 * #{$gutter-horizontal}) / 4) + 2*#{$gutter-horizontal});
    }
}
```

## Flexbox layout

### Flex Container

#### `flex-direction` (**row** | row-reverse | column | comlumn-reverse)
> Direction of Main/Cross axis. 

#### `flex-wrap` (**nowrap** | wrap | wrap-reverse)
> Should elements wrap if view width is smaller then width of elements?

#### `flex-flow` (**row** | column-wrap)
> Shortcut for `flex-direction` and `flex-wrap`.

#### `justify-content` (**flex-start** | flex-end | center | space-between | space-around | space-evenly)
> How flex items are laid horizontally in flex container. 

#### `align-items` (**stretch** | flex-start | flex-end | center | baseling)
> How flex items are laid vertically in flex container.

#### `align-content` (**stretch** | flex-start | flex-end | center | space-between | space-around)
> When flex items are wrapped then how they are layed vertically in flex container.

### Flex Item

#### `align-self` (**auto** | stretch | flex-start | flex-end | center | baseline)
> Vertical align of one flex item.

#### `order` (**0** | integer)
> Order of flex items. Normally depends on source code.

#### `flex-grow` (**0** | integer)
> How much flex item can grow in relation to others flex items `flex-grow`.

#### `flex-shrink` (**1** | integer)
> How much flex item can shrink in relation to others flex items `flex-shrink`. 

#### `flex-basis` (**auto** | px/%/rem)
> How much width has flex item. In _auto_ width is determined using content. 

> Shortcut: `flex: 1 1 150px` means: flex item with min width 150px, grows and shrinks same as others.

```scss
.container {
    display: flex; // automatically aligns all elements like float
}
```

## CSS Grid

### Grid Container

#### `grid-template`
> Shortcut for `grid-template-rows`, `grid-template-columns` and `grid-template-areas`.

```yml
  grid-template: [<grid-line-name>] "area-alias area-alias" <row-height> [<grid-line-name>]
                 / <column-width> <column-width>;
```

```scss
  grid-template: [header-left] "head head" 30px [header-right]
                 [main-left]   "nav  main" 1fr  [main-right]
                 [footer-left] "nav  foot" 30px [footer-right]
                 / 120px 1fr;
```

- `grid-template-rows`
> Used to set grid rows. 
```scss
grid-template-rows: none;
grid-template-rows: 150px auto 1fr 1fr;
grid-template-rows: [first] 150px [second] 1fr [end];
grid-template-rows: repeat(12, 1fr); // repeat 12 rows with width of height of 1fr
```

- `grid-template-columns`
> Used to set grid columns.

- `grid-template-areas`
> Naming and templating of grid areas. 

```scss
grid-template-areas: "head head"
                     "nav  main"
                     "nav  foot";
grid-template-rows: 50px 1fr 30px;
grid-template-columns: 150px 1fr;
```

#### `grid-gap`
> Shortcut for `row-gap` and `column-gap`.

- `row-gap`
> Size of row gutter.

- `column-gap`
> size of column gutter.

#### `justify-items` (stretch | center | start | end)
> Default `justify-self` for every item in container. `justify` is for **inline** (horizontal) axis.

#### `align-items` (stretch | center | start | end)
> Default `align-self` for every item in container. `align` is for **block** (vertical) axis.

#### `justify-content` (start | end | flex-start | flex-end | center | left | right | normal...)
> Distribution of spaces around **inline** (horizontal) elements.

> When grid columns are smaller than grid and that creates some free space.

#### `align-content` (start | end | flex-start | flex-end | center | left | right | normal...)
> Distribution of spaces around **block** (vertical) elements.

> When grid rows are smaller than grid and that creates some free space.

#### `grid-auto-rows`
> Size of implicit created grid row.

#### `grid-auto-columns`
> Size of implicit created grid columns.

#### `grid-auto-flow` (row | column | row dense)
> How auto-placed algorithm works.


### Grid Item

#### `grid-area`
> Shortcut for `grid-row` (`grid-row-start` and `grid-row-end`) and `grid-column` (`grid-column-start` and `grid-column-end`).

```scss
grid-area: 2 / 1 / 2 / 4;
```

> `grid-row-start`/`grid-column-start`/`grid-row-end`/`grid-column-end`.

> Calculates from **grid line**.

> `span` specs how many cells e.g. `grid-column-end: span 2` will be cross 2 cells.

#### `justify-self` (stretch | center | start | end)
> Placing of item in container. `justify` is for **inline** (horizontal) axis.

#### `align-self` (stretch | center | start | end)
> Placing of item in container. `align` is for **block** (vertical) axis.

#### `order`
> Order of item in grid.

#### Bonus
- `repeat`
> How many columns/rows should be repeated and what is their sizes. 

```scss
repeat(4, [col-start] 250px [col-end])
```
- `auto-fill`
> Creates columns and wraps them if the content is too large/small.

```scss
grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
```

- `auto-fit`
> Creates columns and wraps them if the content is too large/small. Fits the whole row/column (like fr).

- `minmax`
> Is a functional notation that defines a size range greater than or equal to min and less than or equal to max.

```scss
minmax(100px, max-content)
```

- min-content
> Minimum in `minmax` function of content (e.g. text length). 

```scss
grid-template-columns: minmax(min-content, 200px) 1fr 1fr;
```

- max-content
> Maximum in `minmax` function of content (e.g. text length). 

```scss
grid-template-columns: minmax(100px, max-content) 1fr 1fr;
```

- fit-content
> Function that creates size of column (column-size, max-size). Basically its combination of `auto` and `max-width`.

```scss
grid-template-columns: fit-content(200px) 1fr 1fr;
```

> Create column that fits its content but max size is 200px.

- subgrid
> Rather than being specified explicitly, the sizes of the grid rows/columns will be taken from the parent grid’s definition.

```scss
grid-template-columns: subgrid;
```

> **WARNING** Not very much supported. More info [here](https://caniuse.com/#feat=css-subgrid).


## Sources

[1]:[Flexbox container](https://www.vzhurudolu.cz/prirucka/css3-flexbox-kontejner)
[2]:[Basic Layout of Css grid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)
[3]:[MDN CSS Grid area](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-areas)
[4]:[MDN Grid template](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template)
[5]:[MDN Justify content](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content)
[6]:[autofill vs autofit](https://css-tricks.com/auto-sizing-columns-css-grid-auto-fill-vs-auto-fit/)
