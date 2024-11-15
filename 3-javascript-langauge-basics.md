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

### Global Declarations

Unlike the `var` keyboard, when declaring variables using `let` in the global context, variables will not attach to the `window` object as they do with `var`.

```
var name = "Joshua";
console.log(window.name); // "Joshua"

let age = 26;
console.log(window.age); // undefined
```

### Let Declaration in Loops

Prior to the advent of `let`, `for` loop defination involved using an iterator variable whose defination would bleed outside of the loop body:

```
for (var i = 0; i < 5; ++i) {
    // do loop things
}

console.log(i); // 5
```

This is no longer a problem when switching to `let` declarations, as the iterator variable will be scoped only to the `for` loop block:

```
for (let i = 0; i < 5; ++i) {
    // do loop things
}

console.log(i); // ReferenceError: i is not defined
```

### `const` Declaration

`const` behaves identically to that of `let` but with one important difference - It must be initialised with a value, and that value cannot be redefined after declaration. Attempting to modify a `const` variable will not result in a run time error.

```
const age = 26;
age = 36; // TypeError: assigned to a constant
```

`const` disallows redundant declaration.

```
const name = "Joshua";
const name = "Alhassan"; // syntax error
```

`const` is still scoped in blocks

```
const name = "Joshua";

if (true) {
    const name = "Alhassan"
}

console.log(name); // Joshua
```

The `const` declaration is only enforced with respect to the reference to the variable that it points to. If a `const` variable references an object,it does not violate the `const` constraints to modify properties inside that object.

```
const person = {};
person.name = "Joshua"; // Ok
```

Even though the JavaScript engine is creating new instances of `let` iterator variables in for loops, and even though `const` variables behave similarly to `let` variables, you cannot use `const` to declare for loop iterators.

```
for (const i = 0; i < 10; ++1) {}
// TypeError: assignment to constraint variable
```

However, if you were to declare a for loop variable that is not modified,`const` is allowed - precisely becuase a new variables is declared for each iteration. This is especially relevant in the case of `for-of` and `for-in` loops.

```
let i = 0;
for (const j = 7; i < 5; ++i) {
    console.log(j);
}

// 7,7,7,7,7

for (const key in {a:1, b:2}) {
    console.log(key);
}

// a, b

for (const value of [1,2,3,4,5]) {
    console.log(value)
}

// 1,2,3,4,5
```

## Declaration Styles and Best Practices

The introduction of `let` and `const` in ECMAScript 6 bring objectively better tooling to the language in the form of increased precision of declaration scope and semantics. It is no secret that the bizarre behaviour of `var` declarations caused the JavaScript community to pull its collective hair our for years as a result of all the problems it caused. In the wake of introduction of these new keywords, there are some increasingly common patterns emerging that can improve code quality.

### Don't use `var`

With `let` and `const`, most developers willfind that they no longer need to use `var` in their codebase anywhere. The patterns that emerge from restricting variable declaration to only `let` and `const` will serve to enforce higher codebase quality thanks to careful management of variable scope, declaration locality, and const correctness.

### Prefer `const` over `let`

Using `const` declarations allows the browser runtime to enforce constant variables, as well as for static code analysis tools to foresee illegal re-assignment operations. Therefore, many developers feel it is to their advantage to, by default, declare variables as `const` unless they know they will need to re-assign its value at some point. This allows for developers to more concretely reason about values that they know will never change, and also for quick detection of unexpected behaviour in cases where the code execution attempts to perform an unaticipated value re-assignment.

# DATA TYPES

There are six simple data types (also called _primitive_ types) in ECMAScript: undefined, Null, Boolean, Number, String, and Symbol. Symbol was newly introduced in ECMAScript 6. There's also one complex data type called object, which is an un-ordered list of name-value pairs. Because there's noway to define your own data type in ECMAScript, all values can be represented as one of these seven. Having only seven data types may seem like too few to fully represent data: However, ECMAScript's data types have dynamic aspects that make each single data type behave like several.

## The `typeof` Operator

Because ECMAScript is loosely typed, they need to be a way to determine the data type of a given variable. The `typeof` operator provides that information. Using the `typeof` operator on a value returns one of the following strings:

> "undefined" if the value is undefined
> "boolean" if the value is a Boolean
> "string" if the value is string
> "number" if the value is a number
> "Object" if the value is an object (other than function or null)
> "function" if the value is a function
> "Symbol" if the value is a symbol

The `typeof` operator is called like this:

```
let message = "some string";
console.log(typeof message); // "string"

let number = 95;
console.log(typeof number); // "number"
```

Note that `typeof` is an operator and not a function, no paranthesis are required (although they can be used).

Be aware that there are a few cases where `typeof` seemingly returns a confusing but technically correct value. Calling `typeof null` returns a value of "object", as the special value `null` is considered to be an empty object reference.

## The Undefined Type

The undefined type has only one value, which is the special value `undefined`. When a variable is declared using `var` or `let` but not initialised, it is assigned to the value of "undefined" as follows:

```
let message;
console.log(message == undefined); // true
```

In the code above, the variable `message` is declared without initializing it. When compared with the literal value of `undefined` the two are equal.

```
let message = undefined;
console.log(message == undefined); // true
```

The above code is unneccessary because, by default any uninitialized variables gets the value `undefined`

Note that a variable containing the value of `undefined` is different from a variable that hasn't been defined at all.

```
let message; // This variable is declared but has a value undefined.

// let age

console.log(message); // "undefined"
console.log(age); // Causes an error
```

Only one useful operation can be performed on an undeclared variable: You can call `typeof` on it (calling `delete` on an undeclared variable won't cause an error. But this isn't very useful and in fact throws an error in strict mode).

The `typeof` operator returns "undefined" when called on an uninitialized variable but it also returns "undefined" when called on an undeclared variable, which can be a bit confusing.

```
let message; // This variable is declared but has no value of undefined

// let age - This variable isn't declared

console.log(typeof message); // "undefined"
console.log(typeof age); // "undefined"
```

In both cases, calling typeof on the variable returns the string "undefined". Logically, this makes sense because no real operations can be performed with either variables even though they are technically very different.

Note: _Even though uninitialized variables are automatically assigned a value of `undefined`, it is advisable to always initialise variables. Thatway, when `typeof` returns `undefined`, you will know that it's because a given variable hasn't been declared rather than was simply not initialised._

The value `undefined` is falsy: therefore, you are able to more succinctly check for it wherever you might need to. Beaer in mind, however, that many other possible values are also falsy, so be careful in scenarios where you need totest for an exact value of `undefined` rather than just a falsy value:

```
let message; // this variable is declared but has a value of undefined.
// 'age' is not defined

if (message) {
    // This block will not execute
}

if (!message) {
    // This block will execute
}

if (age) {
    // This will throw an error
}
```
