# 📄 HTML Interview Essentials

> A structured, in-depth reference guide covering every HTML concept you need to ace frontend and full-stack developer interviews. From semantic markup to accessibility, forms, SEO, and performance — all in one place.

---

## 📌 Table of Contents

- [What is HTML?](#what-is-html)
- [HTML Document Structure](#html-document-structure)
- [Semantic HTML](#semantic-html)
- [Headings and Text Elements](#headings-and-text-elements)
- [Links and Navigation](#links-and-navigation)
- [Images and Media](#images-and-media)
- [Lists](#lists)
- [Tables](#tables)
- [Forms and Input](#forms-and-input)
- [HTML5 APIs](#html5-apis)
- [Accessibility (a11y)](#accessibility-a11y)
- [SEO Basics in HTML](#seo-basics-in-html)
- [Meta Tags](#meta-tags)
- [Block vs Inline Elements](#block-vs-inline-elements)
- [Void / Self-Closing Elements](#void--self-closing-elements)
- [Global Attributes](#global-attributes)
- [Data Attributes](#data-attributes)
- [HTML Entities](#html-entities)
- [iframe and Embedding](#iframe-and-embedding)
- [Script and Style Loading](#script-and-style-loading)
- [Performance Best Practices](#performance-best-practices)
- [Common Interview Questions](#common-interview-questions)

---

## What is HTML?

HTML stands for **HyperText Markup Language**. It is the standard language used to create and structure content on the web. It is not a programming language — it is a markup language that tells browsers how to display content.

- Current version: **HTML5**
- HTML files have `.html` or `.htm` extension
- Rendered by the browser's **rendering engine** (Blink, Gecko, WebKit)

---

## HTML Document Structure

Every HTML document follows a standard boilerplate:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Page Title</title>
  </head>
  <body>
    <!-- Visible content goes here -->
  </body>
</html>
```

| Part | Purpose |
|---|---|
| `<!DOCTYPE html>` | Tells the browser this is an HTML5 document |
| `<html lang="en">` | Root element; `lang` helps screen readers and SEO |
| `<head>` | Contains metadata, not visible on the page |
| `<body>` | Contains all visible page content |
| `<meta charset="UTF-8">` | Ensures proper character encoding |
| `<meta name="viewport">` | Makes the page responsive on mobile |

> **Interview Tip:** Always explain that `<!DOCTYPE html>` is a declaration, not a tag. It tells the browser to render the page in standards mode, avoiding quirks mode.

---

## Semantic HTML

Semantic HTML uses elements that convey meaning about the content inside them, rather than just defining how it looks.

### Why it matters
- Improves **accessibility** (screen readers understand the page structure)
- Helps **SEO** (search engines understand content hierarchy)
- Makes code **easier to read and maintain**

### Common Semantic Elements

```html
<header>   <!-- Top of a page or section -->
<nav>      <!-- Navigation links -->
<main>     <!-- Primary content of the page (only one per page) -->
<section>  <!-- Thematically grouped content -->
<article>  <!-- Standalone, self-contained content -->
<aside>    <!-- Sidebar or tangentially related content -->
<footer>   <!-- Bottom of a page or section -->
<figure>   <!-- Self-contained media content -->
<figcaption> <!-- Caption for a figure -->
<time>     <!-- Machine-readable date/time -->
<mark>     <!-- Highlighted text -->
<details>  <!-- Disclosure widget -->
<summary>  <!-- Visible heading for <details> -->
```

### Non-Semantic vs Semantic

```html
<!-- Non-Semantic -->
<div class="header">...</div>
<div class="nav">...</div>

<!-- Semantic -->
<header>...</header>
<nav>...</nav>
```

---

## Headings and Text Elements

```html
<h1>Main Heading (one per page)</h1>
<h2>Section Heading</h2>
<h3>Sub-section</h3>
<h4>Sub-sub-section</h4>
<h5>Rarely used</h5>
<h6>Rarely used</h6>

<p>Paragraph text</p>

<strong>Bold with importance</strong>  <!-- semantic -->
<b>Bold without importance</b>          <!-- presentational -->

<em>Italic with emphasis</em>           <!-- semantic -->
<i>Italic without emphasis</i>          <!-- presentational (icons, foreign terms) -->

<small>Fine print</small>
<del>Deleted text</del>
<ins>Inserted text</ins>
<sub>Subscript</sub>
<sup>Superscript</sup>

<blockquote cite="https://source.com">
  A quoted block of text.
</blockquote>

<q>Inline quote</q>
<abbr title="HyperText Markup Language">HTML</abbr>
<code>Inline code</code>
<pre><code>Block of preformatted code</code></pre>
<kbd>Ctrl</kbd> + <kbd>C</kbd>  <!-- Keyboard input -->
<br />   <!-- Line break -->
<hr />   <!-- Thematic break / horizontal rule -->
```

> **Interview Tip:** Know the difference between `<strong>` vs `<b>` and `<em>` vs `<i>`. Semantic versions carry meaning for assistive technologies.

---

## Links and Navigation

```html
<!-- Basic link -->
<a href="https://example.com">Visit Example</a>

<!-- Open in new tab (always add rel for security) -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">Open New Tab</a>

<!-- Relative link -->
<a href="/about">About Page</a>

<!-- Anchor link (same page) -->
<a href="#section-id">Jump to Section</a>

<!-- Email link -->
<a href="mailto:hello@example.com">Email Us</a>

<!-- Phone link -->
<a href="tel:+923001234567">Call Us</a>

<!-- Download link -->
<a href="/files/resume.pdf" download>Download Resume</a>
```

### Why `rel="noopener noreferrer"`?

When using `target="_blank"`, the opened page can access `window.opener` and potentially redirect your page. Adding `rel="noopener noreferrer"` prevents this security vulnerability.

---

## Images and Media

```html
<!-- Basic image -->
<img src="photo.jpg" alt="A description of the image" width="800" height="600" />

<!-- Responsive image with srcset -->
<img
  src="photo-800.jpg"
  srcset="photo-400.jpg 400w, photo-800.jpg 800w, photo-1200.jpg 1200w"
  sizes="(max-width: 600px) 400px, (max-width: 1000px) 800px, 1200px"
  alt="Responsive image example"
/>

<!-- Picture element for art direction -->
<picture>
  <source media="(max-width: 600px)" srcset="mobile.jpg" />
  <source media="(max-width: 1200px)" srcset="tablet.jpg" />
  <img src="desktop.jpg" alt="Hero image" />
</picture>

<!-- Lazy loading -->
<img src="photo.jpg" alt="Lazy loaded" loading="lazy" />

<!-- Video -->
<video controls width="720" poster="thumbnail.jpg">
  <source src="video.mp4" type="video/mp4" />
  <source src="video.webm" type="video/webm" />
  Your browser does not support the video tag.
</video>

<!-- Audio -->
<audio controls>
  <source src="audio.mp3" type="audio/mpeg" />
  Your browser does not support the audio element.
</audio>
```

> **Interview Tip:** The `alt` attribute is critical for accessibility and SEO. An empty `alt=""` tells screen readers to skip the image (use for decorative images). A missing `alt` is an accessibility failure.

---

## Lists

```html
<!-- Unordered list -->
<ul>
  <li>Item one</li>
  <li>Item two</li>
</ul>

<!-- Ordered list -->
<ol start="1" type="1">
  <li>First step</li>
  <li>Second step</li>
</ol>

<!-- type values for ol: "1", "A", "a", "I", "i" -->

<!-- Description list (key-value pairs) -->
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language</dd>
  <dt>CSS</dt>
  <dd>Cascading Style Sheets</dd>
</dl>

<!-- Nested lists -->
<ul>
  <li>Frontend
    <ul>
      <li>HTML</li>
      <li>CSS</li>
      <li>JavaScript</li>
    </ul>
  </li>
</ul>
```

---

## Tables

```html
<table>
  <caption>Monthly Sales Report</caption>
  <thead>
    <tr>
      <th scope="col">Month</th>
      <th scope="col">Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>January</td>
      <td>$10,000</td>
    </tr>
    <tr>
      <td>February</td>
      <td>$12,500</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>Total</td>
      <td>$22,500</td>
    </tr>
  </tfoot>
</table>
```

| Attribute | Purpose |
|---|---|
| `colspan` | Merges cells across columns |
| `rowspan` | Merges cells across rows |
| `scope="col/row"` | Accessibility hint for screen readers |
| `<caption>` | Describes the table for accessibility |

> **Interview Tip:** Tables are for **tabular data only**, not for layout. Using tables for layout is an old practice that harms accessibility.

---

## Forms and Input

Forms are one of the most interview-heavy topics in HTML.

```html
<form action="/submit" method="POST" enctype="multipart/form-data" novalidate>

  <!-- Text -->
  <label for="name">Full Name</label>
  <input type="text" id="name" name="name" placeholder="John Doe" required minlength="2" maxlength="50" />

  <!-- Email -->
  <input type="email" id="email" name="email" required />

  <!-- Password -->
  <input type="password" id="password" name="password" minlength="8" />

  <!-- Number -->
  <input type="number" name="age" min="18" max="100" step="1" />

  <!-- Date -->
  <input type="date" name="dob" />

  <!-- File upload -->
  <input type="file" name="avatar" accept="image/*" multiple />

  <!-- Checkbox -->
  <input type="checkbox" id="agree" name="agree" value="yes" checked />
  <label for="agree">I agree to the terms</label>

  <!-- Radio buttons -->
  <input type="radio" id="male" name="gender" value="male" />
  <label for="male">Male</label>
  <input type="radio" id="female" name="gender" value="female" />
  <label for="female">Female</label>

  <!-- Textarea -->
  <textarea name="message" rows="5" cols="40" placeholder="Your message..."></textarea>

  <!-- Select dropdown -->
  <select name="country">
    <option value="">Select a country</option>
    <optgroup label="Asia">
      <option value="pk">Pakistan</option>
      <option value="in">India</option>
    </optgroup>
  </select>

  <!-- Datalist (autocomplete suggestions) -->
  <input list="languages" name="language" />
  <datalist id="languages">
    <option value="JavaScript" />
    <option value="Python" />
    <option value="TypeScript" />
  </datalist>

  <!-- Hidden field -->
  <input type="hidden" name="csrf_token" value="abc123" />

  <!-- Range slider -->
  <input type="range" name="volume" min="0" max="100" value="50" />

  <!-- Color picker -->
  <input type="color" name="theme_color" />

  <!-- Submit -->
  <button type="submit">Submit</button>
  <button type="reset">Reset</button>
  <button type="button" onclick="doSomething()">Custom Action</button>

</form>
```

### Form Attributes

| Attribute | Meaning |
|---|---|
| `action` | Where to send form data |
| `method` | `GET` or `POST` |
| `enctype` | Encoding type; use `multipart/form-data` for file uploads |
| `novalidate` | Disables browser's built-in validation |
| `autocomplete` | `on` or `off` for autofill |

### Input Validation Attributes

| Attribute | Purpose |
|---|---|
| `required` | Field cannot be empty |
| `minlength` / `maxlength` | Text length constraints |
| `min` / `max` | Numeric/date range |
| `pattern` | Regex pattern validation |
| `step` | Increment for number/range |
| `type` | Built-in email, url, number validation |

---

## HTML5 APIs

HTML5 introduced several powerful browser APIs accessible via JavaScript:

| API | Description |
|---|---|
| **Geolocation API** | Get user's geographic location |
| **Web Storage API** | `localStorage` and `sessionStorage` for client-side storage |
| **Canvas API** | Draw 2D graphics via `<canvas>` |
| **Drag and Drop API** | Native drag-and-drop interaction |
| **History API** | Manipulate browser history (`pushState`, `replaceState`) |
| **Web Workers** | Run scripts in background threads |
| **Fetch API** | Make HTTP requests (modern replacement for XHR) |
| **Fullscreen API** | Make elements go fullscreen |
| **Notification API** | Show native browser notifications |
| **Service Worker API** | Enables offline support / PWAs |

```html
<!-- Canvas -->
<canvas id="myCanvas" width="500" height="300"></canvas>

<!-- Progress bar -->
<progress value="70" max="100"></progress>

<!-- Meter (range gauge) -->
<meter value="6" min="0" max="10" low="3" high="8" optimum="9">6 out of 10</meter>

<!-- Dialog element -->
<dialog id="myModal">
  <p>This is a native dialog!</p>
  <button onclick="document.getElementById('myModal').close()">Close</button>
</dialog>
```

---

## Accessibility (a11y)

Accessibility is always a discussion point in senior-level interviews.

```html
<!-- ARIA roles -->
<div role="alert">Error: Something went wrong.</div>
<nav role="navigation" aria-label="Main Navigation">...</nav>

<!-- ARIA labels for icon-only buttons -->
<button aria-label="Close dialog">
  <svg>...</svg>
</button>

<!-- ARIA described by -->
<input type="text" id="email" aria-describedby="email-hint" />
<span id="email-hint">We'll never share your email.</span>

<!-- Live regions for dynamic content -->
<div aria-live="polite" aria-atomic="true">
  Item added to cart!
</div>

<!-- Skip navigation link (keyboard users) -->
<a href="#main-content" class="skip-link">Skip to main content</a>

<!-- Hide from assistive tech -->
<span aria-hidden="true">🎉</span>

<!-- Tab index -->
<div tabindex="0">Focusable div</div>
<div tabindex="-1">Programmatically focusable only</div>
```

### Accessibility Checklist

- [ ] All images have meaningful `alt` text
- [ ] Form inputs have associated `<label>` elements
- [ ] Color contrast meets WCAG 2.1 AA (4.5:1 for text)
- [ ] Page has a single `<h1>` and a logical heading hierarchy
- [ ] Interactive elements are keyboard navigable
- [ ] Focus states are visible
- [ ] `lang` attribute is set on `<html>`
- [ ] Skip links are provided for keyboard users

---

## SEO Basics in HTML

```html
<head>
  <!-- Primary SEO tags -->
  <title>Buy Running Shoes Online | BrandName</title>
  <meta name="description" content="Shop the best running shoes for men and women. Free delivery on orders over $50." />
  <meta name="keywords" content="running shoes, sports shoes, buy shoes online" />
  <link rel="canonical" href="https://example.com/running-shoes" />

  <!-- Open Graph (Facebook, LinkedIn) -->
  <meta property="og:title" content="Buy Running Shoes Online" />
  <meta property="og:description" content="Shop the best running shoes." />
  <meta property="og:image" content="https://example.com/og-image.jpg" />
  <meta property="og:url" content="https://example.com/running-shoes" />
  <meta property="og:type" content="website" />

  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary_large_image" />
  <meta name="twitter:title" content="Buy Running Shoes Online" />
  <meta name="twitter:description" content="Shop the best running shoes." />
  <meta name="twitter:image" content="https://example.com/twitter-image.jpg" />

  <!-- Robots -->
  <meta name="robots" content="index, follow" />
</head>
```

> **Interview Tip:** The `<title>` is the single most important on-page SEO element. It should be unique per page and around 50-60 characters.

---

## Meta Tags

```html
<head>
  <!-- Character encoding -->
  <meta charset="UTF-8" />

  <!-- Responsive viewport -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- Theme color (browser UI) -->
  <meta name="theme-color" content="#1a1a2e" />

  <!-- Refresh/redirect -->
  <meta http-equiv="refresh" content="5; url=https://example.com" />

  <!-- Prevent caching -->
  <meta http-equiv="Cache-Control" content="no-cache" />

  <!-- Author -->
  <meta name="author" content="Haseeb Javed" />

  <!-- Favicon -->
  <link rel="icon" href="/favicon.ico" type="image/x-icon" />
  <link rel="apple-touch-icon" href="/apple-touch-icon.png" />

  <!-- Preconnect for performance -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="dns-prefetch" href="https://cdn.example.com" />
</head>
```

---

## Block vs Inline Elements

| Block Elements | Inline Elements |
|---|---|
| Start on a new line | Flow within text |
| Take full available width | Take only as much width as needed |
| `<div>`, `<p>`, `<h1>-<h6>` | `<span>`, `<a>`, `<strong>`, `<em>` |
| `<ul>`, `<ol>`, `<table>` | `<img>`, `<input>`, `<label>` |
| `<section>`, `<article>`, `<nav>` | `<button>`, `<code>`, `<abbr>` |

> **Note:** In CSS, the `display` property can override the default behavior of any element.

---

## Void / Self-Closing Elements

Void elements do not have closing tags and cannot have children:

```html
<br />
<hr />
<img />
<input />
<link />
<meta />
<area />
<base />
<col />
<embed />
<param />
<source />
<track />
<wbr />
```

> **Interview Tip:** In HTML5, the trailing slash (`/`) on void elements is optional but valid. In XHTML it was required. Most style guides keep it for clarity.

---

## Global Attributes

These attributes work on any HTML element:

| Attribute | Purpose |
|---|---|
| `id` | Unique identifier (one per page) |
| `class` | CSS class name(s) |
| `style` | Inline CSS styles |
| `title` | Tooltip text on hover |
| `lang` | Language of element content |
| `dir` | Text direction: `ltr`, `rtl`, `auto` |
| `hidden` | Hides element (like `display: none`) |
| `tabindex` | Controls keyboard focus order |
| `contenteditable` | Makes element editable in browser |
| `draggable` | Enables drag-and-drop |
| `spellcheck` | Enables/disables spell check |
| `data-*` | Custom data attributes |
| `aria-*` | Accessibility attributes |

---

## Data Attributes

Data attributes let you store custom data on any HTML element, accessible via JavaScript.

```html
<button data-user-id="42" data-role="admin" onclick="handleClick(this)">
  Click Me
</button>
```

```javascript
const btn = document.querySelector('button');

// Read
console.log(btn.dataset.userId); // "42"
console.log(btn.dataset.role);   // "admin"

// Write
btn.dataset.status = "active";

// Remove
delete btn.dataset.role;
```

> **Interview Tip:** Data attributes are great for passing data between HTML and JavaScript without using hidden inputs or global variables.

---

## HTML Entities

Used to display reserved or special characters:

| Character | Entity Name | Entity Number |
|---|---|---|
| `<` | `&lt;` | `&#60;` |
| `>` | `&gt;` | `&#62;` |
| `&` | `&amp;` | `&#38;` |
| `"` | `&quot;` | `&#34;` |
| `'` | `&apos;` | `&#39;` |
| ` ` (non-breaking space) | `&nbsp;` | `&#160;` |
| `©` | `&copy;` | `&#169;` |
| `®` | `&reg;` | `&#174;` |
| `™` | `&trade;` | `&#8482;` |
| `→` | `&rarr;` | `&#8594;` |
| `€` | `&euro;` | `&#8364;` |

---

## iframe and Embedding

```html
<!-- Basic iframe -->
<iframe
  src="https://example.com"
  width="800"
  height="600"
  title="Embedded Page"
  loading="lazy"
  sandbox="allow-scripts allow-same-origin"
></iframe>

<!-- Embed YouTube video -->
<iframe
  src="https://www.youtube.com/embed/VIDEO_ID"
  title="YouTube video"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope"
  allowfullscreen
  loading="lazy"
></iframe>

<!-- Google Maps -->
<iframe
  src="https://www.google.com/maps/embed?pb=..."
  title="Location Map"
  loading="lazy"
  allowfullscreen
></iframe>
```

### sandbox attribute values

| Value | What it allows |
|---|---|
| `allow-scripts` | JavaScript execution |
| `allow-same-origin` | Same-origin access |
| `allow-forms` | Form submission |
| `allow-popups` | Popups / new windows |
| `allow-top-navigation` | Can navigate top-level window |

> **Interview Tip:** iframes have security implications. Always use `sandbox` and set `title` for accessibility. Never embed untrusted content without `sandbox`.

---

## Script and Style Loading

```html
<!-- CSS in head (render-blocking, needed for initial paint) -->
<link rel="stylesheet" href="styles.css" />

<!-- Inline critical CSS -->
<style>
  body { margin: 0; font-family: sans-serif; }
</style>

<!-- Regular script (blocks parsing) -->
<script src="app.js"></script>

<!-- Defer: downloads in parallel, runs after HTML parsing -->
<script src="app.js" defer></script>

<!-- Async: downloads in parallel, runs as soon as ready (no order guarantee) -->
<script src="analytics.js" async></script>

<!-- Module script (deferred by default) -->
<script type="module" src="main.js"></script>

<!-- Inline script -->
<script>
  console.log("Hello from inline script");
</script>
```

### defer vs async

| | `defer` | `async` |
|---|---|---|
| Downloads | In parallel | In parallel |
| Execution | After HTML parsed | As soon as downloaded |
| Order | Maintained | Not guaranteed |
| Best for | App scripts with dependencies | Independent scripts (analytics, ads) |

---

## Performance Best Practices

- Put `<link>` stylesheets in `<head>` to avoid FOUC (Flash of Unstyled Content)
- Put `<script>` tags at the bottom of `<body>` or use `defer`
- Use `loading="lazy"` on images and iframes below the fold
- Use `<link rel="preload">` for critical resources like fonts
- Use `srcset` and `sizes` for responsive images
- Compress images (WebP format preferred)
- Minimize use of `<table>` for layout
- Avoid deeply nested DOM structures
- Use `async` for third-party scripts that don't depend on your app

```html
<!-- Preload critical font -->
<link rel="preload" href="/fonts/inter.woff2" as="font" type="font/woff2" crossorigin />

<!-- Preconnect to CDN -->
<link rel="preconnect" href="https://cdn.example.com" />
```

---

## Common Interview Questions

### Q1. What is the difference between `<section>` and `<div>`?
`<section>` is a semantic element that represents a thematically grouped block of content. It should ideally have a heading. `<div>` is a generic, non-semantic container used purely for styling or scripting purposes.

### Q2. What does `DOCTYPE` do?
It tells the browser which version of HTML to use for rendering. `<!DOCTYPE html>` triggers HTML5 standards mode and prevents quirks mode.

### Q3. What is the difference between `id` and `class`?
`id` must be unique within a page and is used for a single element. `class` can be reused on multiple elements. `id` has higher CSS specificity.

### Q4. What is the difference between `GET` and `POST` in forms?
`GET` appends form data to the URL as query parameters. It is bookmarkable but exposes data in the URL. `POST` sends data in the request body, suitable for sensitive or large data.

### Q5. What is an ARIA attribute?
ARIA (Accessible Rich Internet Applications) attributes like `aria-label`, `aria-hidden`, `aria-live` etc. are added to HTML elements to improve accessibility for screen readers and assistive technologies.

### Q6. What is the purpose of `<meta name="viewport">`?
It controls how the browser scales and sizes the page on mobile devices. Without it, mobile browsers zoom out and the page looks like a desktop view shrunken down.

### Q7. What is the difference between `async` and `defer` on scripts?
Both download the script without blocking HTML parsing. `async` executes the script as soon as it is downloaded (no order guarantee). `defer` waits until HTML parsing is complete and maintains script order.

### Q8. Why should you use semantic HTML instead of divs for everything?
Semantic HTML improves accessibility (screen readers understand the page structure), helps SEO (search engines better index the content), and makes code easier to read and maintain.

### Q9. What is the difference between `<strong>` and `<b>`?
`<strong>` marks text as having strong importance (semantic). `<b>` is just presentational bold with no semantic meaning. Screen readers may add emphasis when reading `<strong>` but not `<b>`.

### Q10. What happens if you omit the `alt` attribute on an image?
Some screen readers will read out the file name of the image, which is a bad user experience. It also fails WCAG accessibility guidelines. Always provide an `alt`, even if it is empty (`alt=""`) for decorative images.

### Q11. What is `tabindex`?
`tabindex` controls keyboard focus order. A value of `0` makes an element focusable in the natural document order. A value of `-1` makes it focusable only via JavaScript. Positive values like `1`, `2` create a manual tab order (generally avoid this).

### Q12. What is the `<template>` element?
`<template>` holds HTML content that is not rendered when the page loads. It is used as a blueprint for dynamically creating elements via JavaScript. Its content lives in a `DocumentFragment`.

```html
<template id="card-template">
  <div class="card">
    <h3 class="card-title"></h3>
    <p class="card-body"></p>
  </div>
</template>
```

---

## Contributing

Found an error or want to add more topics? Feel free to open a PR or issue. Contributions are always welcome.

---

## Author

**Haseeb Javed**
Full-Stack Developer | React, Django, FastAPI

- GitHub: [@haseebjaved4212](https://github.com/haseebjaved4212)
- Email: contactimhaseeb@gmail.com

---

## License

This project is open source and available under the [MIT License](LICENSE).