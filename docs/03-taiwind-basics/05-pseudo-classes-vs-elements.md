# Pseudo Classes Vs Pseudo Elements

## Pseudo classes
Pseudo classes are used to defined special states of an element. They are used style elements based on their state, such as hovered over, focused.

Some of the common pseudo classes are:
- `:hover` : Applies styles when user hovers over an element.
- `:focus` : Applies styles when an element is focused.
- `:active` : Applies styles when an elmenent is activated like a link is clicked.
- `:first-child` : Applies styles to the first child of a parent element.
- `:last-child` : Applies styles to the last child of a parent element.
- `:nth-child(n)` : Applies styles to the nth child of a parent element.
- `:disabled` : Applies styles when an element is disabled.
- `:enabled` : Applies styles when an element is enabled.
- `:checked` : Applies styles when an element is checked like checkboxes and radio-buttons

## Pseudo Elements
Psudo elements are used to style specific parts of an element. They are used
- to insert content before or after an element.
- to style first letter or line of an element.

Some of the common pseudo elements are:
- `::before` : Inserts content before the element.
- `::after` : Inserts content after the element.
- `::first-line` : Applies styles to the first line of an element.
- `::selection` : Applies styles to the portion of an element that is selected by the user.
- `::firt-letter` : Applies styles to the first letter of a block of text

### Example

```css
p::first-letter {
  font-size: 2em;
  font-weight: bold;
  color: #ff6347; /* Tomato Color */
}
```


## Equivalent Tailwind classes

Tailwind doesn't support pseudo elements directly. But there is a way to do it. I would suggest for plain css implementation.

Here are some of the tailwind pseudo classes
- `hover:` : example `<div class="hover:bg-blue-400">Hover me</div>`
- `focus:` : example `<input class="focus:outline-none focus:ring-2 focus:ring-cyan-500"/>`
- `active:` : example `<button class="active:bg-green-500">Click me</button>`
- `first:` : example `<div class="first:mt-0">First Child</div>`
- `last:` : example `<div class="last:mb-0">Last Child</div>`
- `checked:` : example `<input type="checkbox" class="checked:bg-green-500" />`
- `disabled:` : example `<button class="disabled:opacity-50" disabled>Disabled Button</button>`
