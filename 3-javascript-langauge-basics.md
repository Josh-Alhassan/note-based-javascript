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

### Statements

Statements in ECMAScript are terminated by a semicolon. Omitting the semicolon makes the parser determine where the end of the statement occurs.

```
let sum = a + b // valid - not recommended
let diff = a - b; // valid - preferred
```

Even though a semicolon is not required at the end of statements, you should always include one. Including semicolons helps prevent errors of omission, such as not finishing what you were typing, and allows developers to compress ECMAScript code by retrieving extra white space. Including semicolons also improves performance in certain situations because parsers try to correct syntax errors by inserting semicolons where they appear to belond.

Multiple satements can be combined into a code block by using c-style syntax, beginning with a left curly brace `({)` and ending with a right curly brace `(})`:

```
if (test) {
    test = false;
    console.log(false);
}
```

Control statements, such as `if`, require code blocks only when executing multiple statements. However, is is considered a best practice to always use code blocks with control statements, even if there's only one statement to be executed.

```
// Valid - but error prone and should be avoided

if (test)
console.log(test);

// Preferred
if (test) {
    console.log(test);
}
```

## Keywords & Reserved Words

By rule, keywords are reserved and cannot be used as identifiers or property names.

```
break       do          in              typeof
case        else        instanceof      var
catch       export      new             void
class       extends     return          while
const       etc
```

## Variables

ECMAScript variables are loosely typed, meaning that a variable can hold any type of data. Every variable is simply a named placeholder for a value. There are three keywords that can be used to declare a variable: `var`, `const`, and `let`.

### The `var` Keywords

To define a variable, use the `var` operator followed by the variable name (an identifier) like this:

`var message;`

This code defines a variable named `message` that can be used to hold any value. (Without initialization, it holds the special value `undefined`). ECMAScript implements variable initialization, so it's possible to define the variable and set its value at the same time, as in this example:

`var message = "Hello World";`

`message` is defined to hold a string value of "Hello World". Doing this initialization doesn't mark the variable as being a string type: It is simply the assignment of a value in the variable.

It is still possible to not only change the value stored in the variable but also change the type of value such as this:

```
var message = "hello world";
message = 100; // Legal, but not recommended
```

It is not recommended to switch the data type that a variable contains, but it is completely valid in ECMAScript.

### Var Declaration Scope

It's important to note that using `var` operator to define a variable makes it local to the function scope in which it was defined. For example, defining a variable inside of a function using `var` means that the variable is destroyed as soon as the function exits.

```
function test() {
    var message = "Hello Function"; // local variable
}

test();
console.log(message); // error!

```

the `message` variable is defined within a function using `var`. The function is called `test()`, which creates the variable and assigns its value. Immediately after that, the variable is destroyed so that the last line in the example causes an error. It is however possible to define a variable globally by simply omitting the `var` operator as follows:

```
function test() {
    message = "Hello Function"; // globally variable
}

test();
console.log(message); // "Hello Function"
```

By removing the `var` operator, the `message` variable becomes global.

**Note**: _Although it's possible to define global variables by omitting the `var` operator, this approach is not recommended. Global variables defined locally are hard to maintain and cause confusion because it's not Immediately apparent if the omission of `var` was intentional. Strict mode throws a `ReferenceError` when an undeclared variable is assigned a value._

If you need to define more than one variable, you can do so using a single statement, seperating each variable with a comma like this:

```
var message = "hi",
    found = false,
    age = 29
```

Here, these variables are defined and initialized. Because ECMAScript is loosely typed, variable initializations using different data types may be combined into a single statement. Inserting line breaks and indenting the variables is to help improve readability.

### Var Declaration Hoisting

When using `var` the following is possible becuase variables declared using that keyword are hoisted to the top of the function

```
function foo () {
    console.log(age);
    var age = 26;
}

function(); // undefined
```

The above doesn't throw an error because the ECMAScript runtime technically treats it like this:

```
function foo () {
    var age;
    console.log(age);
    age = 26;
}

foo() // underfined
```

This is "hoisting," where the interpreter pulls all variable declarations to the top of it's scope. It also allows you to use redundant `var` declarations without penalty.

```
function foo() {
    var age = 16;
    var age = 26;
    var age = 36;
    console.log(age);
}

foo(); // 36
```

### `let` Declarations

`let` operators is nearly the same way as `var`, but with some important difference. Most notable is that `let` is block scoped. But `var` is function scoped.

```
if (true) {
    var name = "Joshua";
    console.log(name); // Joshua
}

console.log(name); // Joshua

if (true) {
    let age = 26;
    console.log(age); // 26
}

console.log(age); // ReferenceError: age is not defined
```

Here, the age variable cannot be referenced outside the `if` block because its scope does not extend outside the block. Block scope is strictly a subset of function scope, so any scope limitations that apply to `var` declarations will also apply to `var` declarations.

`let` declarations also does not allow for any redundant declarations within a block scope. Doing so will result in an error:

```
let age;
let age; // SyntaxError; identifier `age` has already been declared.
```

**Note**: The different keywords do not declare different types of variables - They just specify how the variables exist inside the relevant scope.

### Temporal Dead Zone

Another important difference between `var` and `let` is that `let` declarations cannot be used in a way that assumes hoisting:

```
// name is hoisted
console.log(name); // undefined
var name = "Joshua";
```

The segment of execution that occurs before the declaration is referred to as the "Temporal Dead Zone," and any attempted references to those variables will throw a `ReferenceError`.

TDZ is a concept that refers to the period between the declaration of a `let` or `const` variable and its initialization. During this time, the variable exists but cannot be accessed, and any attempt to access it will throw a `ReferenceError`.
