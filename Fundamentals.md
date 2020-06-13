# Introduction

## Javascript History
- initially called **Livescript** as it was initially created to "make web pages alive" as it ran in the browser.
- named so becuase Java was very popular at that time and Javascript creators wanted to market it as a "younger" brother to Java.
-  to standardize JavaScript for multiple independent implementations **ECMAScipt** or **ES** specification was standardized by Ecma International. Javascript is the most popular implementation of ECMAScript.
- Javascript can execute not only in the browser, but also on the server, or actually on any device that has a special program called the **JavaScript engine**. The browser has an embedded engine sometimes called a **JavaScript virtual machine**. Most popular engines being **V8 in Chrome and Opera** and **SpiderMonkey in Firefox**.
- These engines use **JIT Compilers**, which means they first compile the code, run it, and then analyze and run optimizations during runtime of the compiled code to make it even more efficient.
- In-browser JS is used to customize webpages, but out-browser JS can be used to design entire backends/software.
- Reasons for JS popularity:
  - Simple
  - Full integration with HTML/CSS
  - JS engine is present and enabled by default on browser
- Many new languages are **transpiled** (converted)  to Javascript before they run in the browser. Ex - CoffeeScript, TypeScript (Microsoft), Flow (Facebook), Dart (Google).

### Developer Console
- In Chrome:
  - Press `F12`
  - Goto `Console`
  - You can type single line js and press `Enter` to run it
  - To type multiple lines, just hit `Shift+Enter` to continue typing into the next line
  
## JS Fundamentals

### <script> tag
- JS code on an HTML page can be written inside it as 
```js
  <script> ...js code goes here... </script>
```  
- We can use external scripts as 
```js
  <script src="my.js">
  ...cannot use js code here, when using external script...
  </script>
```
- we can have multiple `<script>` tags anywhere on a webpage
- The `type` and `language` attributes are not required anymore
  
### Semicolons
- they are automatically added in most cases, only where Javascript feels like
- just as a good programming practice, always use semicolons

### Comments
- Single line
```js
// This will be ignored
```
- Multi-line 
```js
/* All this
will be 
ignored*/
```
- Nesting of comments is not allowed

### 'use strict'
- written as a string
```js
"use strict"; // either this way
'use strict'; //or this way
```
- used to specify that older language features must not be included
- it can placed **only at the top of the script (only comments can come before it)**, or at the **start of the function body (in this case it only affects that function)**

### Variables
- new way: `let`
- old way: `var`
- constant: `const`
```js
const Birthday = "25/02/1998";
```

### Data types
- 8 basic types: 
  - `number` -  limited by ±2<sup>53</sup> (`123`)
  - `bigint` - numbers larger than ±2<sup>53</sup> (`123n`)
  - `string` - `""` or `''` or `backticks` (extended functionality quotes to enable usage of `${...}`)
  - `null` - nothing, empty or value unknown
  - `undefined` - default initial value for unassigned things
  - `boolean` - `true`/`false`
  - `object` - more complex data structures
  - `symbol` - unique identifier for object
- 3 special numeric values which also belong to `number` data type
  - `Infinity` - +∞
  - `-Infinity` - -∞
  - `NaN` - Not-a-Number (often a result of mathematical operation other than `+` on unequal data types)
- `typeof` operator
  - `typeof x` or `typeof(x)`
  - it returns a string (name of type detected)
  - `typeof(null)` is `object` and it is a language error
  - `typeof(function_name)` reutrns `function`. Ex - `typeof alert`

### Interaction: alert, prompt, confirm
- all three opens a *"modal window"* i.e. the script and the page pauses until this window is closed either by interacting or pressing `Esc`
- we can't control location and look of this modal window

- **alert:** returns nothing
```js
alert("FBI! OPEN UP!!");
```
- **prompt:** returns the input, if `Esc` then `null`
```js
let name = prompt("Enter your name:", Abhishek); //Second param is always optional
```
- **confirm:** returns `true` on OK, otherwise `false` (even on `Esc`)
```js
let permission = confirm("Close this window?");
```

### Type Conversions
#### String Conversion
Every other datatype can be converted to `string` type using `String(value_to_convert)` as:
- `null` becomes `"null"`
- `undefined` becomes `"undefined"`
- `true`/`false` becomes `"true"`/`"false"`
- `12345` becomes `"12345"`

#### Number Conversion
Implicit conversion happens in mathematical functions and expressions automatically. Use `Number(value_to_convert)` to explicitly convert.
| Value    |   Becomes...  | 
|----------|-------------|
| undefined |  NaN | 
| null |    0   | 
| true/false | 0/1 |  
| string | Whitespaces from the start and end are removed. If the remaining string is empty, the result is 0. Otherwise, the number is "read" from the string. An error gives NaN. |

#### Boolean Conversion
The conversion rule:
- Values that are intuitively "empty", like 0, an empty string (`""`), `null`, `undefined`, and `NaN`, become `false`.
- Other values become `true`.

**NOTE**: `"0"` is not an empty string and hence it's boolean value is `true`.

### Basic operators & maths
Arithmetic operaors - `+`, `-`, `*`, `/`, `%`, and `**`

### + is a very special operator
- Arithmetic addition
- String concatenation
  - **only** the `+` operator converts any other type to `string` if one of the operands is a `string`.
  ```js
  let a = 2 + '3'; // 2 will be converted to string and the result will be "23"
  let b = 2 + 2 + '1'; // "41" and not "221", because of associativity
  let c = '1' + 2 + 2; // "122"
  ```
- Convert to Numeric type (shorthand for `Number(value)`), no effect on numbers 

```js
"" + 1 + 0
"" - 1 + 0
true + false
6 / "3"
"2" * "3"
4 + 5 + "px"
"$" + 4 + 5
"4" - 2
"4px" - 2
7 / 0
"  -9  " + 5
"  -9  " - 5
null + 1
undefined + 1
" \t \n" - 2
```

### Assignment (=)
Returns assigned value
```js
let b;
let a = (b=5);
alert("a = " + a);   

// Output: a = 5
```

#### Chained Assignments
```js
a = b = c = 4; // All a,b, and c get value as 4
```

### Compound Operators
Exist for all arithmetical and bitwise operators. Ex - `+=`, `|=`, etc...

### Unary Increment/Decrement
Postfix and prefix: `++` and `--`

### Bitwise operators
AND (`&`), OR (`|`), XOR (`^`), NOT (`~`), LEFT SHIFT (`<<`), RIGHT SHIFT (`>>`), and ZERO-FILL RIGHT SHIFT ('>>>')

### Comma operator
Same as in C. Very low precedence.