# JavaScript

If in doubt, refer to the [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript). To be honest, you should probably just read it anyway. The following guide will mostly summarise Airbnb's and add some more context for our workflow.

## Overview :eyeglasses:

- Always use feature detection over browser detection.
  - [Modernizr](http://modernizr.com/) is our choice for feature detection.
  - Try to use [grunt-modernizr](https://github.com/Modernizr/grunt-modernizr) if possible to create a smaller customised build.
  - Only use browser detection is there is no hope left.
- Keep functions as small as you can.
  - If they do more than one thing, consider breaking them up into multiple functions.
- Include JavaScript at the end of the HTML document, just before the closing ```</body>``` tag.
  - Apart from Modernizr, which is included just before the closing ```</head>``` tag.

## Organisation :file_folder:

Currently, we use the [Revealing Module Pattern](http://addyosmani.com/resources/essentialjsdesignpatterns/book/#revealingmodulepatternjavascript) to keep things nice and organised. This might change in the near future as we test out an AMD approach.

## Style :ok_woman:

- Try to write variables and function names that make sense!
  - camelCase for variables and functions.
  - PascalCase for classes.
  - CAPS for constants.
- Indent with two spaces.
- Use lots of spaces:
  - 1 before the leading brace
  - Spaces inbetween operators
  - Leave a blank line after blocks and before the next statement
- Don't use leading commas, it's a bit weird
- Always use ```var``` to declare variables and use one per variable
- Assign variables at the top of their scope, usually the module.
- Use single quotes for strings.
- Use ```===``` and ```!==``` instead of ```==``` and ```!=```

Example:

```js
// This is horrible
  c = 1;
  var iC = function(){
    return c = c+1;
  }

// This is better
var counter = 1;

var increaseCounter = function {
  return counter++;
}
```

## Tooling :wrench:

- Using Grunt, we lint, concatenate and smush our JS.
