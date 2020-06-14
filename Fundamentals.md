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
- Only `[a-zA-Z0-9\_$]` are allowed, first character should not be a digit.

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
| true/false | 1/0 |  
| string | Whitespaces from the start and end are removed. If the remaining string is empty, the result is 0. Otherwise, the number is "read" from the string. An alphanumeric mixed string gives NaN. |

#### Boolean Conversion
The conversion rule:
- Values that are intuitively "empty", like 0, an empty string (`""`), `null`, `undefined`, and `NaN`, become `false`.
- Other values become `true`.

**NOTE**: `"0"` is not an empty string and hence it's boolean value is `true`.

### Basic operators & maths
Arithmetic operaors - `+`, `-`, `*`, `/`, `%`, and `**`

### + is a very special operator
- Arithmetic addition (on numeric and boolean).
- String concatenation
  - **only** the `+` operator converts any other type to `string` if one of the operands is a `string`. **All** other basic operators convert string to numeric if one of the operands is a `string`.
  ```js
  let a = 2 + '3'; // 2 will be converted to string and the result will be "23"
  let b = 2 + 2 + '1'; // "41" and not "221", because of associativity
  let c = '1' + 2 + 2; // "122"
  ```
- Convert to Numeric type (shorthand for `Number(value)`), no effect on numbers. 

- **Exercise:**
```js
"" + 1 + 0  // "10"
"" - 1 + 0  // "-1"
true + false  // 1
true + true // 2
6 / "3" // 2
"2" * "3" // 6
4 + 5 + "px"  // 9px
"$" + 4 + 5 // $45
"4" - 2 // 2
"4px" - 2 // NaN
7 / 0 // Infinity
"  -9  " + 5  // " -9 5"
"  -9  " - 5  // -14
null + 1  // 1
undefined + 1 // NaN
" \t \n" - 2  // -2, as the string is an empty string (only having whitespace chars) i.e. "0" after numeric conversion
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

## Comparisons
- All comparison operators return a boolean value.
- 8 comparison operators: `<`, `>`, `<=`, `>=`, `==`, `!=`, `===`, and `!==`.
- **String Comparison:** Strings are compared lexicographically (unicode) character-by-character.
```js
alert( 'Z' > 'A' ); // true
alert( 'Glow' > 'Glee' ); // true
alert( 'Bee' > 'Be' ); // true
```
- **Strict equality operator (===):** Returns `false` if the operands are of different types.
```js
alert(0 == false); // true
alert(0 === false); // false
```
### Comparisons with null and undefined
```js
alert(null === undefined);  // false
alert(null == undefined);  // true, they both are same for == operator
```
- `==` is defined separately than other comparison operators:
  - every comparison operator converts operands to number first. `null` converts to `0` and `undefined` to `NaN`.
  - `==` is defined such that `null` and `undefined` are **only** equal to one another and **not anything else**. No such conversion takes place with `null` and `undefined` with `==`. This can lead to non-intuitive results like [this](https://javascript.info/comparison#strange-result-null-vs-0).
  
  ```js
  alert(null == 0); // false, null to number is 0 but no such conversion for == and above rule is followed
  ```

### Conditional operators
`if-else`, `else if`, `switch`, and `?:`.
- **Switch:**
  - No ranges are allowed unlike C/C++.
  - The case matching is **strict**. 
  - Both `switch` and `case` allow arbitrary expressions.
```js
switch(a+b){
  case '1':  // 1 won't match with this
  
  case (b+1):
  
  case 3:   // '3' won't match with this
}
```

### Logical operators
- Operands get converted to `boolean` type before operation.
- Operands are evaluated from left to right.
- **There is a return type, it is not always `boolean`.**
<br><br>
- **OR (||):** finds the first *truthy* value (short-circuited) and returns that value, if all `false` then return value of last operand.
- **AND (&&):** finds the first *falsy* value (short-circuited) and returns that value, if all `true` then return value of last operand.
- **NOT(!):** returns `true`/`false`. Convert operand to `boolean` type, inverse the value and return it. `!!` can be used in place of `Boolean(value)`.

**Must do Exercises:** [here](https://javascript.info/logical-operators#tasks).

### Nullish coalescing operator '??'
- It performs a check for `null` and `undefined` values.
- The result of `a ?? b` is: `a` if it's not `null` or `undefined`, otherwise `b`.
- `??` returns the first *defined* value.
- It's forbidden to use it with `||` or `&&` without explicit parentheses.

### Loops
`for`, `while`, and `do...while`
- any part of the `for` loop can be skipped
- inline declaration is allowed in `for` loop
```js
for(let i=0; i<10; i++){}
```
- `break` and `continue` - call is only possible from inside a loop.
- To jump in code, use labels with break as:
```js
for(let i=0; i<10; i++)
{
  if(i == 5)
    break foo;
}

foo: alert("You just jumped here!")
```
**NOTE:** The label must be somewhere **above** its usage (`break label;`), unlike C/C++.

### Functions
- Scope rules (*global* and *local*) and variables are *pass-by-value* as in C/C++.
```js
function message(){
let m = "Hello World!";   // local variable 
alert(m);
}

message();  // call
```
- If params are not passed or insufficient params are provided during the call, then such params are assigned `undefined`, unless a default param is provided in the function definition.
- A function with an empty return or without it returns `undefined`.
- Functions can be declared anywhere in a program, even inside `if`/`else` blocks, but they'll be accessible only inside that block.
- Functions can be used above the code declaring them just like in C/C++, but not with function expressions. 

### Function Expression
- Functions can be assigned to variables as:
```js
let sayHi = function() {
  alert( "Hello" );
};  
```
- This print the source code of the function:
```js
function sayHi() {
  alert( "Hello" );
}
alert( sayHi ); // shows the function code, does not call it
```
  - We can copy a function to another variable as:
  ```js
  let funcNew = sayHi;
  ```
  
  #### Callback functions
  A function can be used in a function declaration and later passed as argument. Those functions are called "Callbacks".
  ```js
  function ask(question, yes, no) { // used here as normal vars
  if (confirm(question)) yes();
  else no();
} 

function showOk() {
  alert( "You agreed." );
}

function showCancel() {
  alert( "You canceled the execution." );
}

// usage: functions showOk, showCancel are passed as arguments to ask
ask("Do you agree?", showOk, showCancel);
  ```
- We can also declare functions inside `ask(...)` call as:
```js
function ask(question, yes, no) {
  if (confirm(question)) yes()
  else no();
}

ask(
  "Do you agree?",
  function() { alert("You agreed."); },   // anonymous function
  function() { alert("You canceled the execution."); }  // anonymous function
);
```

### Arrow functions
- `let func = (arg1, arg2, ...argN) => expression`
```js
`let sum = (a, b) => a + b;
alert( sum(1, 2)
```
- Empty arrow function:
```js
let sayHi = () => alert("Hello!");

sayHi();
```

- Multiline arrow function:
```js
let sum = (a, b) => {  // the curly brace opens a multiline function
  let result = a + b;
  return result; // if we use curly braces, then we need an explicit "return"
};

alert( sum(1, 2) ); // 3
```
