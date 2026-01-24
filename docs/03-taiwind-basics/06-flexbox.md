# Flexbox

Flexbox is a powerfull layout module in css. \
It allows us to design flexible and responsive layout structures without using float or positioning. \

## Basic Concepts

1. Container: The parent element that will hold the flex items.
2. Items: The child elements of the flex container.
3. Properties: Various properties to control the layout, alignment and distribution of flex items.


## Key Properties
- `display: flex` : defines a flex container.
- `flex-direction` : difines the direction of the flex items.
    - Possible values are `row, row-reverese, column, column-reverse`
- `justify-content` : aligns flex items along the main axis.
    - Possible values are `flex-start, flex-end, center, space-between, space-around, space-evenly`

- `align-items` : aligns flex items along the cross axis
    - Possible values are `flex-star, flext-end, center, baseline, stretch`
- `flex-wrap` : controls whether flex items should wrap onto multiple lines.
    - Possible values are `nowrap, wrap, wrap-reverse`
- `align-content`: aligns flex lines when there is extra space in the cross-axis
    - Possible values are `flex-start, flex-end, center, space-between, space-around, stretch`


## Equivalent Classess in Tailwind

### Basic Classes
- `flex` eq `display: flex;`
- `flex-row` eq `flex-direction: row;`
- `flex-row-reverse` eq `flex-direction: row-reverse;`
- `flex-col` eq `flex-direction: column;`
- `flex-col-reverse` eq `flex-direction: column-reverse;`

### Flex Wrap Classes
- `flex-nowrap` eq `flex-wrap: nowrap;`
- `flex-wrap` eq `flex-wrap: wrap;`
- `flex-wrap-reverse` eq `flex-wrap: wrap-reverse;`

### Justify Content
- `justify-start` eq `justify-content: flext-start;`
- `justify-end` eq `justify-content: flex-end;`
- `justify-center` eq `justify-content: center;`
- `justify-between` eq `justify-content: space-between;`
- `justify-around` eq `justify-content: space-around;`
- `justify-evenly` eq `justify-content: space-evenly;`


### Align Item Classes
- `items-start` eq `align-items: flex-start;`
- `items-end` eq `align-items: flex-end;`
- `items-center` eq `align-items: center;`
- `items-baseline` eq `align-items: baseline;`
- `items-stretch` eq `align-items: stretch;`
