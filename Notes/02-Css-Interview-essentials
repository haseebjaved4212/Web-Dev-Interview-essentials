# 🎨 CSS Interview Essentials

> A comprehensive, structured reference guide covering every CSS concept you need to ace frontend and full-stack developer interviews. From the box model and specificity to Flexbox, Grid, animations, and performance — all in one place.

---

## 📌 Table of Contents

- [What is CSS?](#what-is-css)
- [Ways to Add CSS](#ways-to-add-css)
- [Selectors](#selectors)
- [Specificity](#specificity)
- [Cascade and Inheritance](#cascade-and-inheritance)
- [The Box Model](#the-box-model)
- [Display Property](#display-property)
- [Positioning](#positioning)
- [Flexbox](#flexbox)
- [CSS Grid](#css-grid)
- [Units and Values](#units-and-values)
- [Colors](#colors)
- [Typography](#typography)
- [Backgrounds](#backgrounds)
- [Borders and Shadows](#borders-and-shadows)
- [Transitions](#transitions)
- [Animations](#animations)
- [Transforms](#transforms)
- [Pseudo-classes](#pseudo-classes)
- [Pseudo-elements](#pseudo-elements)
- [Variables (Custom Properties)](#variables-custom-properties)
- [Media Queries and Responsive Design](#media-queries-and-responsive-design)
- [Z-index and Stacking Context](#z-index-and-stacking-context)
- [Overflow](#overflow)
- [Clipping and Masking](#clipping-and-masking)
- [CSS Functions](#css-functions)
- [BEM Methodology](#bem-methodology)
- [Performance Best Practices](#performance-best-practices)
- [Common Interview Questions](#common-interview-questions)

---

## What is CSS?

CSS stands for **Cascading Style Sheets**. It is the language used to style and visually present HTML documents. It controls layout, colors, fonts, spacing, animations, and responsiveness.

- Current version: **CSS3** (modular, continuously updated)
- Applied to HTML via selectors
- Follows a **cascade** model where multiple rules can apply to the same element

---

## Ways to Add CSS

```html
<!-- 1. External Stylesheet (recommended) -->
<link rel="stylesheet" href="styles.css" />

<!-- 2. Internal / Embedded -->
<style>
  body {
    margin: 0;
    font-family: sans-serif;
  }
</style>

<!-- 3. Inline (lowest maintainability, highest specificity) -->
<p style="color: red; font-size: 16px;">Hello</p>
```

| Method | Specificity | Reusability | Best Use |
|---|---|---|---|
| External | Normal | High | All production styles |
| Internal | Normal | Low | Single page or email templates |
| Inline | Highest (overrides all) | None | Quick overrides, dynamic JS styles |

---

## Selectors

### Basic Selectors

```css
/* Universal */
* { box-sizing: border-box; }

/* Type / Element */
p { color: gray; }

/* Class */
.card { padding: 16px; }

/* ID */
#header { background: #000; }

/* Attribute */
input[type="text"] { border: 1px solid #ccc; }
a[href^="https"] { color: green; }    /* starts with */
a[href$=".pdf"] { color: red; }       /* ends with */
a[href*="example"] { color: blue; }   /* contains */
```

### Combinators

```css
/* Descendant (any level deep) */
.card p { font-size: 14px; }

/* Child (direct child only) */
.nav > li { display: inline-block; }

/* Adjacent sibling (immediately after) */
h2 + p { margin-top: 0; }

/* General sibling (all siblings after) */
h2 ~ p { color: gray; }
```

### Grouping

```css
h1, h2, h3 {
  font-family: 'Inter', sans-serif;
  font-weight: 700;
}
```

---

## Specificity

Specificity determines which CSS rule wins when multiple rules target the same element.

### Specificity Hierarchy (highest to lowest)

| Level | Source | Value |
|---|---|---|
| 1 | Inline styles | `1,0,0,0` |
| 2 | ID selectors | `0,1,0,0` |
| 3 | Classes, attributes, pseudo-classes | `0,0,1,0` |
| 4 | Elements, pseudo-elements | `0,0,0,1` |
| 5 | Universal `*` | `0,0,0,0` |

```css
/* Specificity: 0,0,0,1 */
p { color: black; }

/* Specificity: 0,0,1,0 */
.text { color: blue; }

/* Specificity: 0,1,0,0 */
#title { color: red; }

/* Specificity: 0,1,1,1 */
#title.text p { color: green; }
```

### !important

```css
p { color: red !important; }
```

`!important` overrides everything including inline styles. Avoid using it unless absolutely necessary (third-party overrides, utility classes). It breaks the natural cascade and makes debugging painful.

> **Interview Tip:** If two rules have the same specificity, the one that appears **later** in the stylesheet wins. This is the "C" in CSS — the Cascade.

---

## Cascade and Inheritance

### The Cascade

When multiple rules target the same element, the browser resolves conflicts using this priority order:

1. **Origin** — browser default < author styles < user styles < `!important`
2. **Specificity** — higher specificity wins
3. **Source Order** — later rule wins on a tie

### Inheritance

Some properties are inherited by default (text-related), others are not (box model related).

```css
/* Inherited by default */
color, font-family, font-size, font-weight,
line-height, letter-spacing, text-align,
visibility, cursor

/* NOT inherited by default */
margin, padding, border, background,
width, height, display, position,
top, left, z-index, overflow
```

### Controlling Inheritance

```css
.child {
  color: inherit;    /* Force inherit from parent */
  color: initial;   /* Reset to browser default */
  color: unset;     /* Inherit if inheritable, else initial */
  color: revert;    /* Revert to browser stylesheet value */
}
```

---

## The Box Model

Every element is a rectangular box made up of four layers:

```
┌─────────────────────────────────────┐
│              MARGIN                 │
│  ┌───────────────────────────────┐  │
│  │           BORDER              │  │
│  │  ┌─────────────────────────┐  │  │
│  │  │        PADDING          │  │  │
│  │  │  ┌───────────────────┐  │  │  │
│  │  │  │      CONTENT      │  │  │  │
│  │  │  └───────────────────┘  │  │  │
│  │  └─────────────────────────┘  │  │
│  └───────────────────────────────┘  │
└─────────────────────────────────────┘
```

### box-sizing

```css
/* Default: width = content only */
.default {
  box-sizing: content-box;
  width: 200px;
  padding: 20px;
  border: 2px solid;
  /* Total width = 200 + 40 + 4 = 244px */
}

/* Preferred: width includes padding + border */
.better {
  box-sizing: border-box;
  width: 200px;
  padding: 20px;
  border: 2px solid;
  /* Total width = 200px (padding and border are inside) */
}

/* Global reset (always use this) */
*, *::before, *::after {
  box-sizing: border-box;
}
```

### Margin Collapse

Vertical margins between block elements **collapse** into a single margin (the larger of the two). Horizontal margins never collapse.

```css
/* These two paragraphs have 30px between them, not 50px */
.p1 { margin-bottom: 30px; }
.p2 { margin-top: 20px; }
```

Margin collapse does NOT happen:
- On flex or grid children
- On absolutely positioned elements
- When padding or border separates the margins
- On inline elements

---

## Display Property

```css
/* Block: full width, new line */
display: block;

/* Inline: flows with text, no width/height */
display: inline;

/* Inline-block: flows with text, accepts width/height */
display: inline-block;

/* Removes element from layout entirely */
display: none;

/* Flex container */
display: flex;

/* Inline flex container */
display: inline-flex;

/* Grid container */
display: grid;

/* Inline grid container */
display: inline-grid;

/* Table display */
display: table;
display: table-row;
display: table-cell;

/* Contents: removes wrapper box, children become direct children of parent */
display: contents;
```

### `display: none` vs `visibility: hidden`

| | `display: none` | `visibility: hidden` |
|---|---|---|
| Space in layout | Removed | Preserved |
| Children visible? | No | No (unless overridden) |
| Accessible to screen readers? | No | No |
| Transition-able? | No | Yes |

---

## Positioning

```css
/* Default. Flows with document */
position: static;

/* Offset from its normal position */
position: relative;
top: 10px;
left: 20px;

/* Removed from flow. Positioned relative to nearest positioned ancestor */
position: absolute;
top: 0;
right: 0;

/* Like absolute but positioned relative to the viewport */
position: fixed;
bottom: 20px;
right: 20px;

/* Hybrid: relative until it hits a scroll threshold, then fixed */
position: sticky;
top: 0;
```

### Containing Block

An absolutely positioned element is positioned relative to the nearest ancestor that has `position` set to anything other than `static`. If none exists, it uses the `<html>` element (initial containing block).

```css
.parent {
  position: relative; /* Makes this the containing block */
}

.child {
  position: absolute;
  top: 0;
  left: 0; /* Positions relative to .parent, not the page */
}
```

---

## Flexbox

Flexbox is a **one-dimensional** layout system (row or column).

### Container Properties

```css
.container {
  display: flex;

  /* Direction */
  flex-direction: row;            /* default */
  flex-direction: row-reverse;
  flex-direction: column;
  flex-direction: column-reverse;

  /* Wrapping */
  flex-wrap: nowrap;              /* default */
  flex-wrap: wrap;
  flex-wrap: wrap-reverse;

  /* Shorthand for direction + wrap */
  flex-flow: row wrap;

  /* Alignment along main axis */
  justify-content: flex-start;   /* default */
  justify-content: flex-end;
  justify-content: center;
  justify-content: space-between;
  justify-content: space-around;
  justify-content: space-evenly;

  /* Alignment along cross axis */
  align-items: stretch;          /* default */
  align-items: flex-start;
  align-items: flex-end;
  align-items: center;
  align-items: baseline;

  /* Multi-line cross-axis alignment */
  align-content: flex-start;
  align-content: center;
  align-content: space-between;
  align-content: stretch;        /* default */

  /* Gap between items */
  gap: 16px;
  row-gap: 16px;
  column-gap: 24px;
}
```

### Item Properties

```css
.item {
  /* Grow factor (how much it grows relative to siblings) */
  flex-grow: 0;    /* default: does not grow */
  flex-grow: 1;    /* takes available space */

  /* Shrink factor */
  flex-shrink: 1;  /* default: can shrink */
  flex-shrink: 0;  /* does not shrink */

  /* Base size before grow/shrink */
  flex-basis: auto;   /* default */
  flex-basis: 200px;
  flex-basis: 50%;

  /* Shorthand: grow shrink basis */
  flex: 1;             /* 1 1 0% */
  flex: auto;          /* 1 1 auto */
  flex: none;          /* 0 0 auto */
  flex: 1 0 200px;

  /* Self alignment (overrides align-items for this item) */
  align-self: center;

  /* Reorder items visually (not in DOM) */
  order: 0;    /* default */
  order: -1;   /* moves to front */
  order: 1;    /* moves to back */
}
```

### Common Flexbox Patterns

```css
/* Perfect centering */
.center {
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Navbar: logo left, links right */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Equal width columns */
.cols > * {
  flex: 1;
}

/* Sticky footer */
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
main {
  flex: 1;
}
```

---

## CSS Grid

CSS Grid is a **two-dimensional** layout system (rows and columns).

### Container Properties

```css
.grid {
  display: grid;

  /* Define columns */
  grid-template-columns: 200px 1fr 1fr;
  grid-template-columns: repeat(3, 1fr);
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  grid-template-columns: minmax(100px, 300px) 1fr;

  /* Define rows */
  grid-template-rows: auto 1fr auto;
  grid-template-rows: repeat(3, 100px);

  /* Named areas */
  grid-template-areas:
    "header header"
    "sidebar main"
    "footer footer";

  /* Gaps */
  gap: 24px;
  row-gap: 16px;
  column-gap: 24px;

  /* Implicit rows/columns (auto-generated) */
  grid-auto-rows: minmax(100px, auto);
  grid-auto-columns: 1fr;
  grid-auto-flow: row;       /* default */
  grid-auto-flow: column;
  grid-auto-flow: row dense; /* fills gaps */

  /* Alignment */
  justify-items: stretch;    /* horizontal alignment of items */
  align-items: stretch;      /* vertical alignment of items */
  justify-content: start;    /* horizontal alignment of grid */
  align-content: start;      /* vertical alignment of grid */
}
```

### Item Properties

```css
.item {
  /* Placement by line numbers */
  grid-column: 1 / 3;        /* span from line 1 to line 3 */
  grid-column: 1 / span 2;   /* start at 1, span 2 columns */
  grid-row: 2 / 4;

  /* Named area placement */
  grid-area: header;

  /* Self alignment */
  justify-self: center;
  align-self: end;
}
```

### Named Areas Example

```css
.layout {
  display: grid;
  grid-template-columns: 250px 1fr;
  grid-template-rows: auto 1fr auto;
  grid-template-areas:
    "header  header"
    "sidebar main"
    "footer  footer";
  min-height: 100vh;
}

header  { grid-area: header; }
.sidebar { grid-area: sidebar; }
main    { grid-area: main; }
footer  { grid-area: footer; }
```

### Flexbox vs Grid

| | Flexbox | Grid |
|---|---|---|
| Dimensions | One-dimensional | Two-dimensional |
| Content-first vs layout-first | Content-first | Layout-first |
| Best for | Navigation, card rows, toolbars | Page layout, complex UI |
| Implicit sizing | Yes | Yes |
| Named areas | No | Yes |

> **Interview Tip:** Use Flexbox when you have a list of items and want them to flow. Use Grid when you have a defined layout with rows and columns that items need to slot into.

---

## Units and Values

### Absolute Units

| Unit | Description |
|---|---|
| `px` | Pixels (most common for screen) |
| `pt` | Points (print, 1pt = 1.33px) |
| `cm`, `mm`, `in` | Physical units (print) |

### Relative Units

| Unit | Relative To |
|---|---|
| `%` | Parent element's dimension |
| `em` | Current element's font-size |
| `rem` | Root element (`<html>`) font-size |
| `vw` | 1% of viewport width |
| `vh` | 1% of viewport height |
| `vmin` | 1% of the smaller viewport dimension |
| `vmax` | 1% of the larger viewport dimension |
| `ch` | Width of the `0` character |
| `ex` | Height of the `x` character |
| `fr` | Fraction of available space (Grid only) |
| `svh`, `dvh`, `lvh` | Small/dynamic/large viewport height (mobile) |

### em vs rem

```css
html { font-size: 16px; }

.parent {
  font-size: 20px;
}

.child {
  font-size: 1.5em;  /* = 30px (1.5 * 20px parent) */
  padding: 1em;      /* = 30px (relative to own font-size) */
  margin: 1rem;      /* = 16px (always relative to root) */
}
```

> **Interview Tip:** Use `rem` for font sizes to respect the user's browser font preferences. Use `em` for padding/margin within components so they scale with the component's font size.

---

## Colors

```css
/* Named */
color: red;
color: transparent;

/* Hex */
color: #ff0000;
color: #f00;          /* shorthand */
color: #ff000080;     /* with alpha (CSS4) */

/* RGB */
color: rgb(255, 0, 0);
color: rgba(255, 0, 0, 0.5);

/* HSL (Hue Saturation Lightness) */
color: hsl(0, 100%, 50%);
color: hsla(0, 100%, 50%, 0.5);

/* CSS4 Modern Syntax */
color: rgb(255 0 0);
color: rgb(255 0 0 / 50%);
color: hsl(0 100% 50% / 0.5);

/* oklch (perceptually uniform, CSS4) */
color: oklch(50% 0.2 30);

/* currentColor (inherits from color property) */
border-color: currentColor;
fill: currentColor;
```

---

## Typography

```css
/* Font family */
font-family: 'Inter', 'Helvetica Neue', Arial, sans-serif;

/* Font size */
font-size: 16px;
font-size: 1rem;
font-size: clamp(1rem, 2.5vw, 2rem); /* responsive fluid font */

/* Font weight */
font-weight: 400;    /* normal */
font-weight: 700;    /* bold */
font-weight: 100;    /* thin */
font-weight: 900;    /* black */

/* Font style */
font-style: normal;
font-style: italic;
font-style: oblique;

/* Line height */
line-height: 1.5;    /* unitless preferred */
line-height: 24px;
line-height: 150%;

/* Letter spacing */
letter-spacing: 0.05em;
letter-spacing: 2px;

/* Text alignment */
text-align: left;
text-align: center;
text-align: right;
text-align: justify;

/* Text decoration */
text-decoration: none;
text-decoration: underline;
text-decoration: underline dotted red;
text-decoration: line-through;

/* Text transform */
text-transform: uppercase;
text-transform: lowercase;
text-transform: capitalize;

/* Text overflow */
white-space: nowrap;
overflow: hidden;
text-overflow: ellipsis;

/* Multi-line ellipsis */
display: -webkit-box;
-webkit-line-clamp: 3;
-webkit-box-orient: vertical;
overflow: hidden;

/* Font shorthand */
font: italic bold 16px/1.5 'Inter', sans-serif;
/* style weight size/line-height family */

/* Web font loading */
@font-face {
  font-family: 'MyFont';
  src: url('/fonts/myfont.woff2') format('woff2'),
       url('/fonts/myfont.woff') format('woff');
  font-display: swap; /* Shows fallback font while loading */
}
```

---

## Backgrounds

```css
/* Color */
background-color: #f0f0f0;

/* Image */
background-image: url('/images/hero.jpg');

/* Gradient */
background-image: linear-gradient(to right, #667eea, #764ba2);
background-image: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
background-image: radial-gradient(circle at center, #fff, #000);
background-image: conic-gradient(from 0deg, red, yellow, green, red);

/* Multiple backgrounds */
background-image: url('overlay.png'), linear-gradient(to right, #000, #fff);

/* Repeat */
background-repeat: no-repeat;
background-repeat: repeat-x;
background-repeat: repeat-y;

/* Size */
background-size: cover;    /* covers entire area, may crop */
background-size: contain;  /* fits entirely, may leave gaps */
background-size: 100% 100%;
background-size: 300px 200px;

/* Position */
background-position: center;
background-position: top right;
background-position: 50% 50%;

/* Attachment */
background-attachment: fixed;    /* parallax effect */
background-attachment: scroll;   /* default */

/* Shorthand */
background: url('hero.jpg') center/cover no-repeat #1a1a2e;
```

---

## Borders and Shadows

```css
/* Border */
border: 2px solid #333;
border-top: 1px dashed red;
border-radius: 8px;
border-radius: 50%;                       /* circle */
border-radius: 10px 20px 30px 40px;      /* TL TR BR BL */
border-radius: 50% 0;                     /* pill on one side */

/* Outline (does not affect layout) */
outline: 2px solid blue;
outline-offset: 4px;

/* Box shadow */
box-shadow: 0 2px 4px rgba(0,0,0,0.1);
box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -2px rgba(0,0,0,0.1);
box-shadow: inset 0 2px 4px rgba(0,0,0,0.2);  /* inner shadow */

/* Text shadow */
text-shadow: 2px 2px 4px rgba(0,0,0,0.3);

/* Multiple shadows */
box-shadow:
  0 1px 3px rgba(0,0,0,0.12),
  0 1px 2px rgba(0,0,0,0.24);
```

---

## Transitions

Transitions animate a property change from one value to another.

```css
/* Shorthand: property duration timing-function delay */
transition: all 0.3s ease;
transition: background-color 0.3s ease, transform 0.2s ease-out;

/* Individual properties */
transition-property: background-color;
transition-duration: 300ms;
transition-timing-function: ease;
transition-delay: 100ms;

/* Timing functions */
transition-timing-function: ease;         /* default */
transition-timing-function: ease-in;
transition-timing-function: ease-out;
transition-timing-function: ease-in-out;
transition-timing-function: linear;
transition-timing-function: cubic-bezier(0.25, 0.1, 0.25, 1);
transition-timing-function: steps(4, end);
```

```css
/* Button hover example */
.btn {
  background: #667eea;
  color: white;
  padding: 12px 24px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  transition: background 0.2s ease, transform 0.1s ease, box-shadow 0.2s ease;
}

.btn:hover {
  background: #764ba2;
  transform: translateY(-2px);
  box-shadow: 0 8px 20px rgba(102, 126, 234, 0.4);
}

.btn:active {
  transform: translateY(0);
}
```

> **Interview Tip:** Prefer transitioning `transform` and `opacity` over properties like `width`, `height`, or `top/left`. Transform and opacity run on the compositor thread and do not trigger layout or paint, making them much smoother (GPU accelerated).

---

## Animations

CSS Animations allow you to define multi-step animated sequences using `@keyframes`.

```css
/* Define keyframes */
@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50%       { transform: scale(1.05); }
}

@keyframes spin {
  from { transform: rotate(0deg); }
  to   { transform: rotate(360deg); }
}

/* Apply animation */
.card {
  animation: fadeIn 0.5s ease-out both;
}

/* Shorthand: name duration timing-function delay iteration-count direction fill-mode */
animation: fadeIn 0.5s ease-out 0.1s 1 normal both;

/* Individual properties */
animation-name: fadeIn;
animation-duration: 500ms;
animation-timing-function: ease-out;
animation-delay: 100ms;
animation-iteration-count: 1;          /* or: infinite */
animation-direction: normal;           /* reverse, alternate, alternate-reverse */
animation-fill-mode: both;             /* none, forwards, backwards, both */
animation-play-state: running;         /* or: paused */

/* Multiple animations */
animation: spin 2s linear infinite, pulse 3s ease-in-out infinite;
```

### Transitions vs Animations

| | Transitions | Animations |
|---|---|---|
| Triggered by | State change (hover, focus) | Applied automatically |
| Steps | Start and end only | Multiple `@keyframes` steps |
| Looping | No | Yes (`infinite`) |
| Control | Limited | Full (pause, reverse, delay) |
| JS required? | No | No |

---

## Transforms

```css
/* 2D Transforms */
transform: translateX(50px);
transform: translateY(-20px);
transform: translate(50px, -20px);

transform: scaleX(1.5);
transform: scaleY(0.8);
transform: scale(1.5);
transform: scale(1.2, 0.8);

transform: rotate(45deg);
transform: rotate(-90deg);

transform: skewX(10deg);
transform: skewY(5deg);
transform: skew(10deg, 5deg);

/* Chain multiple transforms */
transform: translateY(-10px) scale(1.05) rotate(5deg);

/* 3D Transforms */
transform: translateZ(100px);
transform: translate3d(50px, 20px, 100px);
transform: rotateX(45deg);
transform: rotateY(180deg);
transform: rotateZ(45deg);
transform: perspective(500px) rotateY(30deg);

/* Transform origin (point of transformation) */
transform-origin: center;         /* default */
transform-origin: top left;
transform-origin: 50% 100%;
transform-origin: 0 0;

/* 3D perspective on parent */
.parent {
  perspective: 1000px;
  perspective-origin: center;
}
.child {
  transform: rotateY(45deg);
  transform-style: preserve-3d;
}

/* Backface visibility (for card flips) */
.card-front,
.card-back {
  backface-visibility: hidden;
}
```

---

## Pseudo-classes

Pseudo-classes target elements based on state or structural position.

```css
/* User action states */
a:hover    { color: blue; }
a:focus    { outline: 2px solid blue; }
a:active   { color: darkblue; }
a:visited  { color: purple; }

/* Form states */
input:focus          { border-color: blue; }
input:disabled       { opacity: 0.5; cursor: not-allowed; }
input:enabled        { }
input:checked        { }
input:required       { border-color: red; }
input:optional       { }
input:valid          { border-color: green; }
input:invalid        { border-color: red; }
input:placeholder-shown { }
input:focus-visible  { }   /* keyboard focus only */

/* Structural */
li:first-child       { font-weight: bold; }
li:last-child        { border-bottom: none; }
li:nth-child(2)      { }
li:nth-child(even)   { background: #f9f9f9; }
li:nth-child(odd)    { background: #fff; }
li:nth-child(3n+1)   { color: red; }   /* every 3rd starting at 1 */
li:nth-last-child(2) { }
p:first-of-type      { }
p:last-of-type       { }
p:only-child         { }
p:only-of-type       { }
:root                { }               /* html element */
.card:empty          { display: none; }
li:not(.disabled)    { cursor: pointer; }
li:not(:last-child)  { border-bottom: 1px solid #eee; }

/* Link */
:any-link { }

/* Focus within parent */
.form:focus-within { box-shadow: 0 0 0 3px rgba(66,153,225,0.5); }
```

---

## Pseudo-elements

Pseudo-elements create virtual sub-elements without adding HTML.

```css
/* First letter */
p::first-letter {
  font-size: 3em;
  float: left;
  line-height: 1;
}

/* First line */
p::first-line {
  font-weight: bold;
}

/* Before and After (content must be set) */
.badge::before {
  content: "🔥 ";
}

.external-link::after {
  content: " ↗";
  font-size: 0.75em;
}

/* Decorative line using pseudo-element */
.heading::after {
  content: "";
  display: block;
  width: 60px;
  height: 4px;
  background: #667eea;
  margin-top: 8px;
  border-radius: 2px;
}

/* Placeholder styling */
input::placeholder {
  color: #aaa;
  font-style: italic;
}

/* Selection styling */
::selection {
  background: #667eea;
  color: white;
}

/* Scrollbar (webkit) */
::-webkit-scrollbar        { width: 8px; }
::-webkit-scrollbar-track  { background: #f1f1f1; }
::-webkit-scrollbar-thumb  { background: #888; border-radius: 4px; }
```

---

## Variables (Custom Properties)

```css
/* Define variables on :root (global scope) */
:root {
  --color-primary: #667eea;
  --color-secondary: #764ba2;
  --color-text: #1a1a2e;
  --color-bg: #ffffff;

  --font-size-base: 16px;
  --font-family: 'Inter', sans-serif;

  --spacing-sm: 8px;
  --spacing-md: 16px;
  --spacing-lg: 32px;

  --border-radius: 8px;
  --shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Use variables */
.button {
  background: var(--color-primary);
  padding: var(--spacing-sm) var(--spacing-md);
  border-radius: var(--border-radius);
  font-family: var(--font-family);
  font-size: var(--font-size-base);
}

/* Fallback value */
color: var(--color-accent, #ff6b6b);

/* Scoped variable (override within component) */
.card {
  --border-radius: 12px;
  border-radius: var(--border-radius);
}

/* Dark mode with variables */
@media (prefers-color-scheme: dark) {
  :root {
    --color-text: #f0f0f0;
    --color-bg: #1a1a2e;
  }
}

/* Manipulate with JavaScript */
/* document.documentElement.style.setProperty('--color-primary', '#ff0000'); */
```

---

## Media Queries and Responsive Design

### Breakpoints

```css
/* Mobile first (min-width) */
/* Base styles: mobile */

@media (min-width: 640px)  { /* sm: small tablets */ }
@media (min-width: 768px)  { /* md: tablets */ }
@media (min-width: 1024px) { /* lg: desktops */ }
@media (min-width: 1280px) { /* xl: wide screens */ }
@media (min-width: 1536px) { /* 2xl: ultra wide */ }

/* Desktop first (max-width) */
@media (max-width: 1279px) { /* below xl */ }
@media (max-width: 1023px) { /* below lg */ }
@media (max-width: 767px)  { /* below md (mobile) */ }
```

### Media Query Features

```css
/* Orientation */
@media (orientation: landscape) { }
@media (orientation: portrait)  { }

/* Dark mode */
@media (prefers-color-scheme: dark)  { }
@media (prefers-color-scheme: light) { }

/* Reduced motion (accessibility) */
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}

/* High DPI / Retina screens */
@media (-webkit-min-device-pixel-ratio: 2), (min-resolution: 192dpi) {
  .logo { background-image: url('logo@2x.png'); }
}

/* Hover support (touch vs mouse) */
@media (hover: hover) {
  .btn:hover { background: darkblue; }
}

/* Print styles */
@media print {
  .no-print { display: none; }
  body { font-size: 12pt; }
}

/* Range syntax (CSS4) */
@media (768px <= width <= 1024px) { }
```

### Responsive Patterns

```css
/* Fluid typography */
h1 {
  font-size: clamp(1.75rem, 4vw, 3rem);
}

/* Responsive container */
.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 clamp(1rem, 5%, 2rem);
}

/* Auto-responsive grid without media queries */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 24px;
}
```

---

## Z-index and Stacking Context

`z-index` controls which elements appear on top of others along the Z axis.

```css
.modal-backdrop { z-index: 100; }
.modal          { z-index: 200; }
.tooltip        { z-index: 300; }
.notification   { z-index: 400; }
```

### What Creates a Stacking Context?

A new stacking context is created when an element has:
- `position` other than static + `z-index` other than auto
- `opacity` less than 1
- `transform`, `filter`, `perspective`, `clip-path`
- `isolation: isolate`
- `will-change: transform` or `will-change: opacity`
- `mix-blend-mode` other than normal
- `contain: layout` or `contain: paint`

```css
/* Isolation: isolate prevents z-index "bleed" from parent context */
.card {
  isolation: isolate;
}
```

> **Interview Tip:** A `z-index` of `9999` does not always win. If an element is inside a stacking context with a lower `z-index` than a sibling context, it will always be below elements in that sibling context regardless of its own `z-index`.

---

## Overflow

```css
/* Default: content spills out */
overflow: visible;

/* Clips content, no scrollbar */
overflow: hidden;

/* Always shows scrollbar */
overflow: scroll;

/* Only shows scrollbar when needed */
overflow: auto;

/* Clip without creating a block formatting context */
overflow: clip;

/* Axis control */
overflow-x: hidden;
overflow-y: auto;

/* Scroll behavior */
scroll-behavior: smooth;

/* Overflow anchor */
overflow-anchor: none;

/* Overscroll behavior */
overscroll-behavior: contain;   /* prevents scroll chaining */
overscroll-behavior-y: none;    /* prevents pull-to-refresh */
```

---

## Clipping and Masking

```css
/* clip-path */
.circle  { clip-path: circle(50%); }
.ellipse { clip-path: ellipse(60% 40%); }
.polygon { clip-path: polygon(50% 0%, 100% 100%, 0% 100%); }
.inset   { clip-path: inset(10px 20px 30px 40px round 8px); }

/* Animated clip-path */
.reveal {
  clip-path: inset(0 100% 0 0);
  transition: clip-path 0.6s ease;
}
.reveal.visible {
  clip-path: inset(0 0% 0 0);
}

/* mask */
.masked {
  mask-image: linear-gradient(to bottom, black 70%, transparent);
  -webkit-mask-image: linear-gradient(to bottom, black 70%, transparent);
}
```

---

## CSS Functions

```css
/* calc() - mathematical expressions */
width: calc(100% - 64px);
padding: calc(var(--spacing-md) * 2);
font-size: calc(1rem + 0.5vw);

/* clamp(min, preferred, max) */
font-size: clamp(1rem, 2.5vw, 2rem);
width: clamp(280px, 50%, 600px);

/* min() and max() */
width: min(100%, 600px);         /* smaller of the two */
width: max(300px, 50%);          /* larger of the two */

/* var() */
color: var(--color-primary, #667eea);

/* env() - environment variables */
padding-top: env(safe-area-inset-top);    /* notch/safe area on iOS */

/* url() */
background-image: url('/images/hero.jpg');

/* rgb(), hsl(), oklch() */
color: rgb(102 126 234 / 80%);

/* attr() */
.tooltip::after {
  content: attr(data-tooltip);
}

/* counter() */
ol { counter-reset: section; }
li::before {
  counter-increment: section;
  content: counter(section) ". ";
}

/* repeat(), minmax(), fit-content() */
grid-template-columns: repeat(3, minmax(0, 1fr));
grid-template-columns: fit-content(200px) 1fr;
```

---

## BEM Methodology

BEM stands for **Block, Element, Modifier**. It is a CSS naming convention that makes styles more readable and maintainable.

```
Block:    .card
Element:  .card__title
Modifier: .card--featured
          .card__title--large
```

```html
<article class="card card--featured">
  <img class="card__image" src="..." alt="..." />
  <div class="card__body">
    <h2 class="card__title card__title--large">Title</h2>
    <p class="card__description">Description text</p>
    <a class="card__link" href="#">Read more</a>
  </div>
</article>
```

```css
/* Block */
.card {
  border-radius: 8px;
  overflow: hidden;
  box-shadow: var(--shadow);
}

/* Modifier on block */
.card--featured {
  border: 2px solid var(--color-primary);
}

/* Element */
.card__image {
  width: 100%;
  aspect-ratio: 16 / 9;
  object-fit: cover;
}

.card__title {
  font-size: 1.25rem;
  font-weight: 700;
}

/* Modifier on element */
.card__title--large {
  font-size: 1.75rem;
}
```

### Why BEM?

- Avoids specificity wars (almost everything is a single class)
- Self-documenting class names
- Prevents style bleeding across components
- Works great with component-based frameworks

---

## Performance Best Practices

- Avoid `*` universal selector in complex selectors
- Use `transform` and `opacity` for animations (GPU accelerated, no reflow)
- Avoid `@import` inside CSS files (blocks parallel downloads)
- Minimize use of expensive properties in animations: `box-shadow`, `border-radius`, `filter` on large areas
- Use `will-change: transform` sparingly only on elements that will animate
- Use `contain: layout paint` on isolated components to limit repaint areas
- Use `font-display: swap` to prevent invisible text while fonts load
- Minify and gzip CSS in production
- Remove unused CSS (tools: PurgeCSS, UnCSS)
- Use `@layer` for predictable cascade ordering
- Prefer logical properties for internationalization: `margin-inline-start` over `margin-left`

```css
/* will-change: hint the browser to prepare for GPU layer */
.animated-element {
  will-change: transform;
}
/* Remove after animation is done */
.animated-element.done {
  will-change: auto;
}

/* CSS Layers (predictable cascade) */
@layer reset, base, components, utilities;

@layer base {
  h1 { font-size: 2rem; }
}
@layer components {
  .card { padding: 16px; }
}
@layer utilities {
  .mt-4 { margin-top: 16px; }
}

/* Logical properties */
.text {
  margin-inline: auto;      /* margin-left + margin-right */
  padding-block: 16px;      /* padding-top + padding-bottom */
  border-inline-start: 4px solid blue; /* left border in LTR, right in RTL */
}
```

---

## Common Interview Questions

### Q1. What is the CSS Box Model?
Every element is made up of four layers: content, padding, border, and margin. By default, `width` and `height` only apply to the content area (`content-box`). Using `box-sizing: border-box` includes padding and border in the width calculation, which is almost always what you want.

### Q2. What is CSS Specificity and how is it calculated?
Specificity determines which CSS rule takes effect when multiple rules apply to the same element. It is calculated as a four-part value: inline styles (1,0,0,0), IDs (0,1,0,0), classes/attributes/pseudo-classes (0,0,1,0), and elements/pseudo-elements (0,0,0,1). The rule with the higher specificity wins. If specificity is equal, the rule appearing later in the source wins.

### Q3. What is the difference between `position: relative`, `absolute`, `fixed`, and `sticky`?
`relative` offsets the element from its normal position without removing it from the flow. `absolute` removes it from the flow and positions it relative to the nearest non-static ancestor. `fixed` positions it relative to the viewport and it stays in place during scroll. `sticky` behaves like `relative` until it reaches a scroll threshold, then acts like `fixed` within its parent container.

### Q4. What is the difference between Flexbox and CSS Grid?
Flexbox is one-dimensional, working either in rows or columns. It is content-first, meaning it sizes based on the content. Grid is two-dimensional, handling both rows and columns simultaneously. It is layout-first, meaning you define the grid structure and slot items into it.

### Q5. What does `z-index` do and when does it not work?
`z-index` controls the stacking order of positioned elements. It only works on elements with a `position` value other than `static`. It can also appear not to work when the element is inside a stacking context with a lower effective `z-index` than its sibling context, no matter how high you set the child's `z-index`.

### Q6. What is the difference between `em` and `rem`?
`em` is relative to the font size of the element itself (or parent for font-size). `rem` is always relative to the root `<html>` element's font size. `rem` is more predictable for font sizing because it is not affected by nested elements.

### Q7. What is a CSS custom property (variable)?
Custom properties are variables defined with `--` prefix (e.g. `--color-primary`) and used with `var()`. They cascade and inherit like regular CSS properties, can be scoped, changed dynamically via JavaScript, and make theming much easier.

### Q8. How do you create a CSS animation?
You define keyframes with `@keyframes` and apply them using the `animation` property. You can control duration, timing function, delay, iteration count, direction, and fill mode. For simple state-change animations, transitions are usually sufficient.

### Q9. What is `will-change` and when should you use it?
`will-change` is a hint to the browser that an element will be animated, allowing the browser to promote it to its own compositor layer in advance. Use it sparingly, only on elements about to animate, and remove it after the animation is done. Overusing it wastes memory and can actually degrade performance.

### Q10. What is the difference between `display: none` and `visibility: hidden`?
`display: none` removes the element from the layout entirely so it takes up no space. `visibility: hidden` hides the element visually but it still occupies space in the layout. Only `visibility` can be transitioned.

### Q11. What is a stacking context?
A stacking context is a three-dimensional conceptual layer formed by an element and its descendants. Elements within the same stacking context are ordered by `z-index`. Common triggers include `transform`, `opacity < 1`, `position + z-index`, and `isolation: isolate`. Understanding stacking contexts is essential for debugging z-index issues.

### Q12. What is the difference between `transition` and `animation`?
Transitions animate between two states and are triggered by a change (like `:hover`). They only have a start and end state. Animations use `@keyframes` to define multiple steps, run automatically, can loop, reverse, and pause. Animations give you much more control.

### Q13. What is BEM and why is it useful?
BEM (Block Element Modifier) is a naming convention for CSS classes. It structures class names as `.block__element--modifier`. It avoids specificity problems, makes code self-documenting, and prevents styles from leaking between components. It pairs well with component-based frameworks.

### Q14. How does `flex: 1` work?
`flex: 1` is shorthand for `flex-grow: 1; flex-shrink: 1; flex-basis: 0%`. It tells the element to grow and shrink equally to fill available space, starting from a base size of zero. It is the most common way to create equal-width columns in a flex container.

### Q15. What is the difference between `margin: auto` and `text-align: center`?
`margin: auto` centers a block-level element horizontally within its parent by distributing available space equally on both sides. It requires a defined `width`. `text-align: center` centers inline content (text, inline elements) within a block container.

---

## Contributing

Found a gap or want to add a topic? Open a PR or raise an issue. All contributions are welcome.

---

## Author

**Haseeb Javed**
Full-Stack Developer | React, Django, FastAPI

- GitHub: [@haseebjaved4212](https://github.com/haseebjaved4212)
- Email: contactimhaseeb@gmail.com

---

## License

This project is open source and available under the [MIT License](LICENSE).