JavaScript CodeStyle
====================
  - [Overview](#overview)
    - [Scope](#scope)
    - [Goal](#goal)
  - [General](#general)
  - [Naming](#naming)
  - [Strictness](#strictness)
  - [Variable declaration](#variable-declaration)
  - [Literals](#literals)
    - [Objects](#objects)
    - [Arrays](#arrays)
    - [Strings](#strings)
  - [Semicolons](#semicolons)
  - [Keywords](#keywords)
  - [Block Statements](#block-statements)
  - [Conditional Statements](#conditional-statements)
    - [if](#if)
    - [switch](#switch)
  - [Loops](#loops)
    - [for](#for)
    - [for (var i in obj)](#for-var-i-in-obj)
  - [Operators and keywords](#operators-and-keywords)
    - ['const' keyword](#const-keyword)
    - ['with' operator](#with-operator)
    - [Comparison Operators](#comparison-operators)
    - [Ternary Operator](#ternary-operator)
    - [Unary Operators](#unary-operators)
  - [eval](#eval)
  - [undefined](#undefined)
  - [Parentheses](#parentheses)
  - [Exceptions](#exceptions)
  - [Type Casting](#type-casting)
  - [Parsing](#parsing)
  - [Multi-Line Statements](#multi-line-statements)
  - [Method Chaining](#method-chaining)
  - [String concatenation](#string-concatenation)
  - [Empty Lines](#empty-lines)
  - [Function Context](#function-context)
  - [Comments](#comments)
  - [Classes](#classes)
  - [node.js](#nodejs)
    - [Importing Modules](#importing-modules)
  - [Linting](#linting)
    - [JSHint](#jshint)
    - [JSCS](#jscs)

##Overview

###Scope

This document provides the coding standards and guidelines for developers and teams working for or with VaffelNinja. The subjects covered are:

 - Javascript file formatting
 - Naming conventions
 - Coding style
 - Inline documentation
 - Errors and exceptions

###Goals

Good coding standards are important in any development project, particularly when multiple developers are working on the same project. Having coding standards helps to ensure that the code is of high quality, has fewer bugs, and is easily maintained.

##General

  * Files should be encoded in UTF-8 without [BOM](http://en.wikipedia.org/wiki/Byte-order_mark).
  * The line-break character must be LF - `\n`.
  * Files should end with a LF character.
  * One level of indentation is achieved with 4 space characters.
  * Lines should be no longer than 120 characters.
  * Trailing whitespace at the end of lines should be removed.

##Naming
  * All files, functions, variables, parameters, classes etc should be in English, and use generic terms. Exceptions are allowed where the name is intended to reflect very specific Norwegian names or concepts, e.g. "skattelister", "rampelys" etc.
  * `variableNamesLikeThis`
  * `functionNamesLikeThis`
  * `ClassNamesLikeThis`
  * `methodNamesLikeThis`
  * `CONSTANTS_LIKE_THIS`
  * `namespacesLikeThis`
  * `events-like-this`
  * `private` or `protected` properties and methods should be prefixed with a single `_` character
  * Shortened and abbreviated names should be avoided.
  * Common abbreviations, such as `JSON` and `XML` are written in `CamelCase`. For example: `Json`, `Xml`.
  * Filenames should not be camelCased and spaces are prohibited. Use the `-` character instead.
  * Most functions should be named. This is especially important when working with asyncronous processes like timers and callbacks. This helps greatly when debugging:

**Bad:**

```javascript
setTimeout(function() {
    doThatThing();
}, 1000);
```

**Good:**

```javascript
setTimeout(function someDescriptiveTitle() {
    doThatThing();
}, 1000);
```

##Strictness

Always start the top level block with `'use strict;'`. If writing CommonJS modules, assume a scope is present and place the pragma at the top of the file. If writing AMD or standalone Javascript, ensure your file has a separate scope and apply the pragma as early as possible:

**CommonJS:**

```javascript
'use strict';
var fs = require('fs');
/**
 * ... more code
 *
 * module will (implicitly) be wrapped with:
 * (function (exports, require, module, __filename, __dirname) {
 *     // your code here
 * })(module.exports, require, module, 'your-file.js', '/directory/to/file');
 */
```

**AMD/standalone:**

```javascript
(function() {
    'use strict';
    var foo = 'bar';
    // ... more code
});
```

##Variable declaration
  * Each variable should be declared:
    * using a `var` statement;
    * only once in the current scope;
    * on a new line;
    * as close as possible to the place where it's first used.

**Good:**

```javascript
var keys = ['foo', 'bar'];
var values = [23, 42];

var object = {}, key;
while (items.length) {
    key = keys.pop();
    object[key] = values.pop();
}
```

**Bad:**

```javascript
var keys = ['foo', 'bar'], values = [23, 42];
var object = {};

while (items.length) {
    var key = keys.pop();
    object[key] = values.pop();
}
```

##Literals

###Objects
  * There should be no whitespace characters before the colon:

```javascript
var obj = {
    prop: 0
};
```
  * Only property names should be aligned within object literals:

**Good:**

```javascript
var obj = {
    a: 0,
    b: 1,
    lengthyName: 2
};
```
**Bad:**

```javascript
var obj = {
    a          : 0,
    b          : 1,
    lengthyName: 2
};
```
  * Quotes around property names should be typed only if needed:

**Good:**

```javascript
var obj = {
    key: 0,
    'key-key': 1
};
```

**Bad:**

```javascript
var obj = {
    'key': 0,
    'key-key': 1
};
```
  * There should be no trailing commas after the last value of the object, as this breaks older IEs and certain Javascript parsers:

**Bad:**

```javascript
var myObject = {
    key: 'value',
    key2: 'value', // <-- BAD
};
```
  * Reserved words must be quoted if using them as properties:

**Good:**

```javascript
var obj = {
    'default': 'someValue',
    'super': 'someSuper'
};
```

**Bad:**

```javascript
var obj = {
    default: 'someValue',
    super: 'someSuper'
};
```

###Arrays
  * When enumerating elements in an array literal, spaces should be typed after the comma only:

```javascript
var fellowship = ['foo', 'bar', 'baz'];
```

###Strings
  * String literals should use single quotes:

```javascript
var lyrics = 'Never gonna give you up. Never gonna let you down. Never gonna turn around and desert you.';
```
  * If a string contains a single quote character, it should be escaped:

```javascript
var test = 'It shouldn\'t fail';
```

##Semicolons
Statements should always end with a semicolon.

##Keywords
  * Keywords are always followed by a single space character, except after anonymous functions:

```javascript
if (test) {
    // ...
}

function foo() {
    // ...
}

var bar = function() {
    // ...
};
```
  * If the keyword is followed by a semicolon, there should be no space between them:

```javascript
return;
```

##Block Statements
  * The opening curly brace should be on the same line and separated with one space character:

```javascript
if (test) {
    // ...
}

function foo() {
    // ...
}
```
  * Branching and looping statements should always be surrounded with curly braces:

**Good:**

```javascript
if (test) {
    return;
}
```
**Bad:**

```javascript
if (test)
    return;

if (test) return;

if (test) { return; }
```

##Conditional Statements
###if
  * The `else` keyword should be on the same line as the closing brace of the if-part of the statement:

```javascript
if (test) {
    // ...
} else {
    // ...
}
```
  * Condition statements should not contain assignment operations:

**Good:**

```javascript
var foo = bar();
if (foo > 0) {
    // ...
}
```

**Bad:**
```javascript
var foo;
if ((foo = bar()) > 0) {
    // ...
}
```
  * Logical operators should not be used for conditional branching:

**Good:**

```javascript
if (condition) {
    actionIfTrue();
} else {
    actionIfFalse();
}
```

**Bad:**
```javascript
condition && actionIfTrue() || actionIfFalse();
```
  * Conditions longer than the [maximum line length](#general) should be divided as in the example:

```javascript
if (longCondition ||
    anotherLongCondition &&
    yetAnotherLongCondition
) {
    // ...
}
```

 * [Yoda conditions](http://en.wikipedia.org/wiki/Yoda_conditions) should not be used:

**Good:**
```javascript
if (getType() === 'driving') {

}
```

**Bad:**
```javascript
if ('driving' === getType()) {

}
```

###switch
The switch statement should be written as in the example:

```javascript
switch (value) {
    case 1:
        // ...
        break;

    case 2:
        // ...
        break;

    default:
        // ...
        // no break keyword on the last case
}
```

##Loops
###for
Functional constructs (map, reduce etc) are prefered where applicable. [Array.prototype.forEach](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) is prefered over the `for` loop.

```javascript
[1, 2, 3].forEach(function (value) {
    console.log(value);
});
```
Performance-critical parts of the code can use a `for` statement, as well as cases where the loop can be broken out of before iteration has completed.

###for (var i in obj)
When using the `for-in` loop, authors should be aware of the pitfalls of enumerable properties on prototypes and know when to use [hasOwnProperty()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty).

##Operators and keywords
###'const' keyword

Never use the [const](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Statements/const) keyword.

###'with' operator

The `with` operator should not be used.

###Comparison Operators
If there is no need for type casting, the strict equality operator `===` (or strict inequality `!==`) should be used.

###Ternary Operator
The ternary operator should be written as in the examples:

```javascript
var x = a ? b : c;

var y = a ?
    longButSimpleOperandB : longButSimpleOperandC;

var z = a ?
    moreComplicatedB :
    moreComplicatedC;
```

###Unary Operators
Unary operators should be typed without whitespace between them and their operands:
```javascript
var foo = !bar;
```
Exceptions from this rule are the unary [special JS operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators#Special_operators)).

##eval
The `eval` function should be avoided.
`json` serialized data should be parsed with [JSON.parse](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/JSON/parse).

##undefined
Checking for `undefined` values should be done using the strict equality operator.

**Good:**
```javascript
x === undefined;
```

**Bad:**
```javascript
typeof x === 'undefined'

x === void 0
```

##Parentheses
  * Should be used only if it is required of the expression's syntax or semantics.
  * Should not be used with the unary operators `delete`, `typeof` and `void`, or with the keywords `return`, `throw` and `new`.

##Exceptions
`throw` should be used with `new Error` or an object of a class derived from `Error`:

**Good:**
```javascript
throw new Error('msg');
```
**Bad:**
```javascript
throw 'msg';
```

##Type Casting
Type casting should be done explicitly (note the difference between [parsing](#parsing) and type casting):

**Good:**
```javascript
Boolean(foo)
Number(bar)
String(baz)
[].indexOf(qux) === -1 or [].indexOf(qux) < 0
```
**Bad:**
```javascript
!!foo
+bar
baz + ''
~[].indexOf(qux)
```

##Parsing
  * When parsing strings to integers or floats, a radix MUST be specified.

**Good:**
```javascript
var width = parseInt('20px', 10);
var someNum = parseInt('0x10', 16);
```

**Bad:**
```javascript
var width = parseInt('20px');
var someNum = parseInt('0x10');
```

##Multi-Line Statements
  * If a statement is longer than the maximum [line length](#general), it is split into several lines and properly indented.
  * Lines of the statement should be split after an operator:

```javascript
var debt = this.calculateBaseDebt() + this.calculateSharedDebt() + this.calculateDebtPayments() +
    this.calculateDebtFine();
```
  * Closing parentheses should be on a new line with the indentation of the current block statement:

**Good:**
```javascript
DoSomethingThatRequiresALongFunctionName(
    very_long_argument1,
    argument2,
    argument3,
    argument4
);
anotherStatement;
```
**Bad:**
```javascript
DoSomethingThatRequiresALongFunctionName(
    very_long_argument1,
    argument2,
    argument3,
    argument4);
anotherStatement;
```

##Method Chaining
When a method is called on a new line, it should:
  * Be one indentation level deeper than the target object.
  * Begin with the property access operator `.`.

**Good**:

```js
someObject
    .operation()
    .operationWithCallback(function (obj) {
        obj.processed = true;
    })
   .end();
```

**Bad**:

```js
someObject.
   start().
   end();

someObject
.start()
.end();
```

##String concatenation
  * Strings should be concatenated with the `+` operator.
  * The `[].join('')` should be avoided.
  * Escaping newline literals inside strings should be avoided.

**Good:**
```javascript
var foo = 'A rather long string of English text, an error message ' +
    'actually that just keeps going and going -- an error ' +
    'message to make the Energizer bunny blush (right through ' +
    'those Schwarzenegger shades)! Where was I? Oh yes, ' +
    'you\'ve got an error and all the extraneous whitespace is ' +
    'just gravy.  Have a nice day.';
```
**Bad:**
```javascript
var foo = 'A rather long string of English text, an error message \
          actually that just keeps going and going -- an error \
          message to make the Energizer bunny blush (right through \
          those Schwarzenegger shades)! Where was I? Oh yes, \
          you\'ve got an error and all the extraneous whitespace is \
          just gravy.  Have a nice day.';
```

##Empty Lines
A single empty line can be used as a separator for grouping the code into logical blocks:

```javascript
doSomethingTo(x);
doSomethingElseTo(x);
andThen(x);

nowDoSomethingWith(y);

andNowWith(z);
```

##Function Context
* Binding the context variable for function calls should be done using [Function.prototype.bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind). If targeting IE8 or below, a [polyfill or abstraction](https://lodash.com/docs#bind) should be used:

```javascript
doAsync(function () {
    this.fn();
}.bind(this));
```

* Preferably, the context argument should be used (if available):

**Good:**

```javascript
[1, 2, 3].forEach(function (n) {
    this.fn(n);
}, this);
```

**Bad:**

```javascript
[1, 2, 3].forEach(function (n) {
    this.fn(n);
}.bind(this));
```

* If assigning the current context to a variable (generally avoided), the variable should be named `_this`:

```javascript
var _this = this;
doAsync(function () {
    _this.fn();
});
```

##Comments
  * In-line comments should start with `//`. Between the `//` and the text of the comment should be one space character.
  * Comments for functions, classes, etc. should be written according to the [jsdoc](http://usejsdoc.org/) documentation syntax.

##Classes
  * "Symmetrical" methods should be declared one after the other. For example:

```javascript
var FooClass = inherit({
    __constructor: function () {},

    // destructors are placed right after the constructor
    destruct: function () {},

    someMethod: function () {}
});
```

##node.js

###Importing Modules
  * Modules should be imported in the beginning of the file, after the description of the module (if present):

**Good:**

```javascript
var http = require('http');
var fs = require('fs');

// code here
```
**Bad:**

```javascript
var http = require('http');

// code here

var fs = require('fs');

// code here
```

This rule does not apply to modules that are imported "on demand".

  * Module import calls should be grouped according to the following order:

1. Standard node.js modules (i.e. fs, util, etc.).
2. External lib modules.
3. Modules of the current application.

## Linting

###JSHint

Please use [JSHint](https://github.com/jshint/jshint/) with the `.jshintrc` config found in this
repository.

###JSCS

Please use [JSCS](http://jscs.info/) with the `.jscsrc` config found in this repository.
