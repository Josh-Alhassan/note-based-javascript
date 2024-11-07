# JavaScript: Language Basics

At the core of every language is a description of how it should work at the most basic level. This description typically defines syntax, operators, data types and built-in functionality upon which complex situations can be built.

## Syntax

ECMAScript syntax borrows heavily from C and other C-like oriented languages such as Java and Perl.

### Case Sensitivity

The first concept to understand is that everything in ECMAScript is case Sensitive: variables, function names, and operators are all case-sensitive, meaning that a variable name `test` is different from a variable named `Test`.

### Identifiers

An identifier is the name of a variable, function, property or function arguement. Identifiers maybe one or more characters in the following format:

> The first character must be a letter, an underscore(\_), or a dollar ($) sign.
> All other characters may be letters, underscores, dollar signs, or numbers.

By convension, ECMAScript identifiers use _camelCasing_ meaning that the first letter is lowercae and each additional word is offset by a capital letter, like this:

```
firstSecond
myCar
doSomethingImportant
```

This is not strictly enforced, it is considered a best practice to adhere to the built-in ECMAScript functions and objects that follow this format.

### Comments

ECMAScript uses c-language comments for both single-line and block comments. A single-line comment begins with two forward-slash characters, such as this:

`// single line comment`

A block comment begins with a forward slash and asterik (/_) and ends with the opposite (_/), as in this example:

```
/* This is a multi-line
comment */
```

### Strict Mode

ECMAScript 5 (ES5) introduced the concept of `strict mode`. Strict mode is a different parsing and execution model for JavaScript, where some of the erratic behaviour of ECMAScript 3 is addressed and errors are thrown for unsafe activities. To enable `strict mode` for an entire script, include the following at the top:

```
"use strict"
```

Although this may look like a string that isn't assigned to a variable, this is a _pragma_ that tells supporting JavaScript engines to change into `strict mode`. This syntax was chosen spefically so as not to break ECMAScript 3 syntax.

You may also specify just a function to execute on strict mode by including the _pragma_ at the top of the function body:

```
function doSomething() {
    "use strict"
    // function body
}
```

Strict mode changes many parts of how JavaScript is executed. All modern browsers support strict mode.
