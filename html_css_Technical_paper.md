# Technical Paper: HTML and CSS Concepts

# 1. The CSS Box Model

Every HTML element is treated as a rectangular box. The CSS Box Model explains how the size and spacing of an element are calculated.

The Box Model has four main parts:
```
Content
   |
Padding
   |
Border
   |
Margin
```

- **Content** is the actual text, image, or information inside an element.

- **Padding** is the space between the content and the border.


- **Border** surrounds the content and padding.


- **Margin** creates space outside an element.


---

# 2. Inline Versus Block Elements


## Block Elements

Block elements normally start on a new line and take up the available width.

Examples:
```div, p, section, header, footer, h1 to h6```



## Inline Elements

Inline elements stay within the same line and only take up the space they need.

Examples:
```span, a, strong, em```

## Inline-Block

`inline-block` allows elements to stay on the same line while still accepting width and height.

`display: inline-block;`

---

# 3. CSS Positioning: Relative and Absolute

CSS positioning helps control where elements appear on a webpage.

## Position: Relative

An element with `position: relative` remains in its normal position but can be moved.
The original space of the element is still reserved.

## Position: Absolute

An element with `position: absolute` is removed from the normal document flow. It is positioned relative to its nearest positioned parent.


# 4. Common CSS Structural Classes

- Structural classes are used to organize the layout of a webpage.

- **Examples:**
```.container, .wrapper, .header, .main, .sidebar, .content, .footer, .row, .column```

- These names are conventions and do not have special behavior until CSS is applied.

---

# 5. Common CSS Styling Classes

- Styling classes are used to change the appearance of elements.

- Examples:
`.primary`,`.secondary`,`.active`,`.hidden`,`.visible`,`.large`,`.small`,`.rounded`, `.shadow`,`.text-center`

- Reusable classes can reduce repeated CSS code.

---

# 6. CSS Specificity

CSS Specificity determines which style is applied when multiple CSS rules target the same element.

Highest specificity to lowest:
```
!important
   ↓
Inline Style
   ↓
ID
   ↓
Class / Attribute / Pseudo-class
   ↓
Element / Pseudo-element
   ↓
Universal Selector
```
# 7. CSS Responsive Queries
Responsive design means creating websites that work on mobile phones, tablets, laptops, and desktop screens.
Media queries allow CSS to apply different styles based on screen size.

```css
@media (min-width: 768px) {
  .container {
    width: 80%;
  }
}
```
---
# 8. Flexbox

Flexbox is a CSS layout system used to arrange elements in rows or columns.

Example:
```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
}
```
Flexbox is useful for navigation bars, cards, buttons, and simple layouts.

---

# 9. CSS Grid

CSS Grid is a layout system that allows developers to control both rows and columns.

Example:
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}
```

## Flexbox vs Grid

- **Flexbox** is useful for one-dimensional layouts, such as a single row or column.

- **Grid** is useful for two-dimensional layouts where rows and columns need to be controlled together.

---

# 10. Common Header Meta Tags

The `<head>` section contains important information about the webpage.

- **Charset** allows characters to display correctly.

- **Viewport** is important for responsive websites and mobile devices.

- **Description** provides a short description of the webpage.

- **Title** appears in the browser tab.

---

# 11. Semantic HTML

Semantic HTML means using elements based on their meaning. It makes code easier to read and improves accessibility.

- Example:
`<header>`,`<nav>`,`<main>`,`<section>`,`<article>`,`<aside>`,`<footer>`
---

# 12. CSS Reset

Different browsers apply different default styles. A CSS reset helps create a consistent starting point.

A simple reset:

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  line-height: 1.5;
}
```
---
# References

1. MDN Web Docs. CSS Basics: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics

2. MDN Web Docs. CSS Layout:
   https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout

3. MDN Web Docs. Responsive Desig:
   https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Responsive_Design

4. W3Schools. CSS:
   https://www.w3schools.com/css/



