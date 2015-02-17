# CSS

We don't stick to any hard and fast rules when it comes to CSS. We don't use BEM, SMACSS or whatever the latest cool CSS architecture is. __BUT__, we do have some general principles that keep things easier to understand and easier to maintain.

## Overview :eyeglasses:

1. Keep specificity low.
2. Give most things a class.
3. That's it.

Keeping specificity low allows you to write great reusable code _and_ easily override things, if needs be.

Giving most things a class means that, most of the time, your styling concerns are separated from your HTML structure. Classes are also more performant than generic tag elements, but that probably doesn't matter too much these days.

Imagine the following HTML module:

```html
<div class="module">
  <header>
    <h2>Module Title</h2>
    <p>Some cool strapline</p>
  </header>
  <div class="module-inner">
    <!-- Module content  -->
  </div>
</div>
```

If you want to style the strapline, you might do this:

```css
.module header p {
  color: red;
}
```

This styling is closely linked to the structure of the HTML and if we wanted to move the strapline out of the header or add another ```<p>``` element, the CSS would break. If we'd given the strapline a class, like this:

```html
<p class="module-strapline">Some cool strapline</p>
```

then your CSS could simply be:

```css
.module-strapline {
  color: red;
}
```

This selector has lower specificity __and__ it's independent from the HTML structure! If another developer comes along and moves the strapline in the HTML, the CSS should work the same. If another developer wants to update the style, it's also __much__ easier to find in the stylesheet.

Yes, it's longer to type and it's not as 'pure' but it wins every time for both easiness to understand and maintain.

## Tooling :wrench:

- We use SCSS because it's awesome :v:
- We generally use grunt to compile CSS, which allows us to:
  - Use autoprefixer so we don't have to worry about prefixes.
  - Smush the CSS to reduce file size.
  - Add a cache-busting hash.

## Style :ok_woman:

Try to stick to these rules:

- Indent properties and nest styles with 2 spaces
- Always include a space after a selector and before the opening curly brace.
- If styling multiple selectors, keep one selector per line.
- Keep one declaration per line.
- Include a space after the colon.
- Always include a semi-colon at the end of a declaration.
- Include leading zeros, e.g. ```0.5px``` not ```.5px```
- Zero values shouldn't include a unit
- Have the closing curly brace on its own line, at the same indent as the selector.
- Leave a blank line between rules.
- Leave a blank line before nested selectors.
- If a selector only has one rule, consider keeping it all on one line.
- Write descriptive comments, e.g. explain the content and/or purpose of a rule.
- Avoid CSS ```@import```
- ```@import``` in SCSS is great and it's use is encouraged.

Example:

```css
// This is good!
.chart-header,
.table-header {
  display: block;
  width: 100%;
  background: grey;
}
```

Things not to worry too much about:

- Order of property declarations. Life's too short.
  - Maybe put important ones like ```display: none``` at the top!

## Class names :speech_balloon:

- Lowercase names with-hyphens, not camelCase or under_scores.
- Use meaningful names that are purposeful or structural – not presentational.
- Prefix classes based on closest parent.
- If a class is for behaviour, prefix it with ```js-``` and keep it out of the stylesheets.

## Nesting in Sass :hatching_chick:

Don't unnecessarily nest in Sass. If you're giving most things a class, it's not necessary to nest selectors – this just creates more specific style rules that aren't as reusable. As a rough guide, try not to go beyond 3 levels deep.

Leave a blank line before your nested selector, it makes it easier to spot!

Nesting _is_ really useful for element states and pseudo elements, for example:

```css
.sign-up-link {
  background: pink;
  font-weight: bold;

  &:hover {
    text-decoration: underline;
  }
}
```

## Media queries :iphone:

Using SCSS allows us to nest media queries inside a selector. This is great because it means everything related to that selector is in one place so it's easy to find.

Generally, we style elements in a mobile-first manner. This means mobile styles get applied first and styles are overridden for larger screens.

Set variables for your breakpoints so they're easy to adjust if needs be. Then use Sass's string interpolation to define your media query inside a selector, like in the following example:

```css
$tablet: "(min-width: 750px)";

.grid-item {
  width: 100%;

  @media #{$tablet} {
    width: 50%;
  }
}
```

## Organisation :file_folder:

Using SCSS allows us to keep our styles nicely modular and organised. The ```main.scss``` is essentially a table of contents that pulls in everything in the right order.

```css
// DEPENDENCIES
@import "bourbon";
@import "neat";

// BASE STYLES
@import "base/normalize";
@import "base/variables";
@import "base/typography";
@import "base/lists";
@import "base/tables";
@import "base/forms";
@import "base/layout";

// PLUGINS
@import "plugins/carousel";

// COMPONENTS
@import "components/buttons.scss";
@import "components/icons.scss";

// PATTERNS
@import "patterns/header";
@import "patterns/footer";
@import "patterns/grid";
@import "patterns/video-player";

// SECTIONS
@import "sections/home";
@import "sections/about";
```
