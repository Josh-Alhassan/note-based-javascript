# What is JavaScript

## JavaScript Implementation

- Though JavaScript and ECMAScript are often used synonymousely, JavaScript is much more than just what is defined in ECMA-262.
- JavaScript implementation is made up of the following 3 distinct parts.

Diagram Below

- The Core (ECMAScript)
- The Document Object Model (DOM)
- The Browser Object Model (BOM)

1. The Core (ECMAScript)

- ECMAScript is the language defined in ECMA-262. It isn't tied to the browser. Infact, the language has no methods for input or output whatsoever.

- ECMA-262 defines "ECMAScript" language as a base upon which more robust scripting language maybe built.

- "Web Browswers" are just one host environment in which ECMAScript langauge implementation may exist.

- A "host environment" provides the base implmentation of ECMAScript (as a language) and implmentation extensions designed to interface with the environment itself. Example of "extensions" includes the "Document Object Model" which uses ECMAScript's core type and syntax to provide additional functionality that's more specific to the environment. Other host environment include Nodejs, a server-side JavaScript platform.

- ECMA-262 doesn't reference web browsers. On a very basic level, it describes the following parts of the language:

  > Syntax
  > Types
  > Statements
  > Keywords
  > Reserved words
  > Operators
  > Global Objects

- ECMAScript is simply a description of a language implementing all of the facets described in the ECMAScript specificiation. JavaScript implements ECMAScript.

### ECMAScript Editions

- The different versions of ECMAScript are defined as _editions_

#### First Edition

- The first edition of ECMASCript (ECMA-262) was essentially the same as _Netscape's JavaScript 1.1_ but with all references to browser-specific code removed and a few minor changes like, ECMA-262 required support for the unicode standard (to support multiple langauges) and that object be platform independent (Netscape JavaScript 1.1 actually had different implmentations of Objects, such as the `Date` object, depending on the platform). This was a major reason why JavaScript 1.1 and 1.2 did not conform to the first editions of ECMA-262.

#### Second Edition

- This edition of ECMA-262 was largely editorial. The standard was updated to get into strict agreement with ISO/IEC - 16262 and didn't feature any addition, changes or omissions. ECMAScript implmentations typically don't use the second edition as a measure of conformance.

#### Third Edition

This edition marked the arrival of ECMAScript as a true programming language. This edition was the first real update to the standard. It also added support for the regular expressions, new control statements, `try - catch` exception handling and small changes to better prepare for the internationalization.

#### The Fourth Edition

In response to the popularity of JavaScript on the web, developers began revising ECMAScript to meet the growing demands of web development around the world. The fourth edition includes strongly typed variables, new statements and data structures, true classes and classical inheritance and new ways to interact with data.

Note: _Subcommittee of TC39 developed a smaller evolution of the ECMAScript language, because they believed the fourth edition was too big of a jump of the language. So, the fourth edition of ECMAScript was abandoned before officially being published._

#### The Fifth Edition

This edition introduced additional functionality which includes a native `JSON` object for parsing and serializing `JSON` data, methods for inheritance and advanced property defination, and the inclusion of a new strict mode.

#### The Sixth Edition

The sixth edition of ECMA-262 - colloquially reffered to as ES6, ES2015, or ES Harmony - was published in June 2015, and contains arguably the most important collection of ehancements to the specification since its inception. ES6 adds formal support for classes, modules, iterators, generators, arrow functions, promises, reflection, proxies, and a host of new data types.

#### The Seventh Edition

The seventh edition of ECMA-262, dubbed ES7 or ES2016, was published in June of 2016. The revision included only a handlful of syntactical additions such as `Array.Prototype.includes` and the exponentiation operator.

#### The Eight Edition

The eight edition of ECMA-262, called ES8 or ES2017, was finalized in January of 2017. This revision included asynchrounous iteration, rest and spread properties, a collection of new regular expression features, a
`Promise Finally()` catchall handler, and template literal revisions.

#### Ninth Edition

The ninth edition of ECMA-262 is still being finalized, but it already has a large number of features in _stage 3_. Its most significant addition will likely be **dynamic importing of ES6 modules**

### What Does ECMAScript conformance Mean?

ECMA-262 lays out the defination of ECMASCript conformance. To be considered an implementation of ECMASCript, an implementation must do the following:

- Support all "types, values, objects, properties, functions, and program syntax and semantics" as they are described in ECMA-262.

- Support the unicode character standard.

These criteria give implmentation developers a great amount of power and flexiblity for developing new langauages based on ECMASCript, which partly accoints for it's popularity.

### The Document Object Model (DOM)

The Document Object Model (DOM) is an application programming interface (API) for XML that was extended for use in HTML. The DOM maps out an entire page as a hierachy of nodes. Each parts of an HTML or XML page is a type of node containing difference kinds of data. Consider the following HTML pages.

```
<html>
  <head>
    <title> Sample Page </title>
  </head>
  <body>
    <p> Hello World! </p>
  </body>
</html>
```

This code can be diagrammed into a hierachy of nodes using the DOM by creating a tree to represent a document, the DOM allows developers an unprecedented level of control over its content and structure.

Nodes can be removed, added, replaed, and modified easily by using the DOM API.

### The Browser Object Model (BOM)

Using the BOM, developers can interact with the browser outside of the context of its displayed page. What mae the BOM truely unique, and often problematic, was that it was the only part of JavaScirpt implmentation that had no related standard. But, this changed with the intoduction of HTML5, which sought to codify much of the BOM as part of a formal specification.

Primarily, the BOM deals with the browser window and frames, but generally any browser-sepcific extension to JavaScript is considered to be a part of the BOM. The following ae some such extensions:

- The capability to pop up new browser windows.
- The capability to move, resize, and close browser windows.
- The `navigator` object, which gives detailed information about the browser.
- The `screen` object, which gives deetailed information about the user's screen resolution
- The `location` object, which gives detailed information about the page loaded in the browser.
- The `performance` object, which gives detailed information about the browser's memory consumption, navigational behaviour, and timing statistics.
- Support for cookies
- Custom Objects such as XMLHttpRequest and Internet Explorer's ActiveXObjecct.

Because no standard existed for the BOM for a long time, each browser has its own implementation. There are some _de facto_ standards, such as having a `window` object and a `navigator` object, but each browser defines its own properties and methods for these and other objects.
