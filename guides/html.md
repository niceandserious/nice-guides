# HTML

> Strive to maintain HTML standards and semantics, but not at the expense of practicality. Use the least amount of markup with the fewest intricacies whenever possible.
> – [@mdo](http://mdo.github.io/code-guide/#html-practicality)

## Style :ok_woman:

- Indent nested elements once, with 2 spaces.
- Always use double quotes for attributes.
  - Even though the HTML5 spec doesn't require quotes for attributes, it's safer and more consistent to use them.
- Don't include the trailing slash in self-closing elements. In HTML5, they're not required.
  - E.g. ```<img src="my-image.jpg">``` not ```<img src="my-image.jpg"/>```
- Do include optional closing tags like ```</li>```. It's just nicer.
- Lowercase! We're not in the 90s. ```<LOL>```

## Doctype

- Always use the HTML5 doctype: ```<!DOCTYPE html>```
- This enforces standards mode and more consistent rendering in most browsers.

## Character encoding

Set the document's character encoding to UTF-8 using the the meta tag:

```
<meta charset="utf-8">
```

The character encoding should also be set in the HTTP header.

## Language

Try to include the ```lang``` attribute when possible. As we're based in :uk: it'll generally be:

```
<html lang="en-gb">
  <!-- fun stuff -->
</html>
```

Use [other language codes](http://reference.sitepoint.com/html/lang-codes) where appropriate.

## Link types

- HTML5 doesn't require you to specify a ```type``` when including JavaScript and CSS files.
  - So there's no need for ```text/css``` or ```text/javascript```.

## Classes & IDs

- Classes are reusable! So always prefer classes to IDs.
- IDs should be used sparingly, they are mainly for:
  - In-page anchor links
  - JavaScript hooks
- Don't use the same class/ID for both style and behaviour.
  - If a class/ID is used for behaviour, prefix it with ```js-```, e.g. ```js-toggle-menu```
- Separate state-related styles from default styles.
  - Prefix state-related styles with ```is-```, e.g. ```is-active```

## Fallbacks

Make sure to include fallbacks for multimedia content:
- Always include ```alt``` text on ```<img>``` elements that explains what the image shows.
  - Unless an image is purely decorative and you can't use CSS, in which case use ```alt=""```
- If possible, provide video captions or audio transcripts.
