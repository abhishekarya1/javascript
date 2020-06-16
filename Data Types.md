# Data Types

## Methods of primitives
How can there be a method of a primitive? eg. `str.toUpperCase()` or `str.length()`.
<br>
**Ans:** *Primitives are not objects.* Still js provides special methods for them. But, primitives can't have methods so an object is created temporarily, it returns the result, and gets destroyed.
<br><br>
The JavaScript engine highly optimizes this process. It may even skip the creation of the extra object at all. But it must still adhere to the specification and behave as if it creates one.

**`null` and `undefined` don't have any such object methods. They're truly primitive.**

 Some languages like Java allow us to explicitly create "wrapper objects" for primitives using a syntax like `new Number(1)` or `new Boolean(false)`.

In JavaScript, that's also possible for historical reasons, but highly unrecommended. Things will go crazy in several places.

For instance:
```js
alert( typeof 0 ); // "number"

alert( typeof new Number(0) ); // "object"!
```

Objects are always *truthy* in if, so here the alert will show up:

```js
let zero = new Number(0);

if (zero) { // zero is true, because it's an object
  alert( "zero is truthy!?!" );
}
```
On the other hand, using the same functions `String`/`Number`/`Boolean` without `new` is a totally sane and useful thing. They convert a value to the corresponding type: to a `string`, a `number`, or a `boolean` (primitive) as they return primitives instead of object (`this`).

For example, this is entirely valid:
```js
let num = Number("123"); // convert a string to number
```

## Numbers
1. 64-bit format IEEE-754, also known as "double precision floating point numbers",
2. BigInt

### e
```js
let billion = 1000000000;
let billion1 = 1e9;   // billion == billion1 is true

let billion2 = 7.3e9; // 7.3 billion
```
e multiplies the number before it with (1 followed by the number of zeroes equal to the number after e)
```js
1e3 = 1 * 1000
1.23e6 = 1.23 * 1000000
```
**Small numbers:**
```js
let ms = 1e-6; // 0.000001
1.23e-6 = 1.23 / 1000000 (=0.00000123)
```

### Hex, binary and octal numbers
1. Hex - prefix is `0x`
2. Octal - prefix is `0o`
2. Binary - prefix is `0b`

```js
let h = 0xff; // or 0xFF
let a = 0b11111111; // binary form of 255
let b = 0o377; // octal form of 255

alert( a == b ); // true, the same number 255 at both sides
```

### toString(base)
The method `num.toString(base)` returns a string representation of num in the numeral system with the given base.
For example:
```js
let num = 255;

alert( num.toString(16) );  // ff
alert( num.toString(2) );   // 11111111
```
The base can vary from 2 to 36 (digits can be [0-9A-Z]). By default it's 10.

**Calling a method on a number:** If we want to call a method directly on a number, then we need to place two dots `..` after it.
```js
alert( 123456..toString(36) ); // 2n9c
```

### Math functions
- M`ath.floor(num)`
- `Math.ceil(num)`
- `Math.round(num)`
- `Math.trunc(num)`
- `Math.random()`: Returns a random number from 0 to 1 (not including 1)
- `Math.max(a, b, c...)` & `Math.min(a, b, c...)`
- `Math.pow(n, power)`
- `num.toFixed(n)`: Rounds the number to `n` digits after the point and returns a `string` representation of the result.

### Tests: isFinite and isNaN
`isNaN(value)` converts the value to a numeric type and then checks if it's `NaN`. We can't use `NaN === value`? No. **The value NaN is unique in that it does not equal anything, including itself!**
```js
alert(NaN === NaN); // false
```
- `isFinite(value)` converts its argument to a number and returns `true` if it's a regular number, not `NaN`/`Infinity`/`-Infinity`. **It can be used to validate whether a string value is a regular number.** Note that an empty or a space-only string is treated as `0` in all numeric functions including `isFinite`.

### Object.is(a, b) 
It is the same as `a === b`. `a` and `b` are primitives.
```js
Object.is(NaN, NaN) // true
Object.is(0, -0) // false, technically that's true, because internally the number has a sign bit that may be different even if all other bits are zeroes
```
### parseInt and parseFloat
Used to read number from alphanumric strings like `'123px'`, ``12.5rs``. It starts from left to right and stops if number couldn't be read, then it returns the *read portion only*.

```js
alert( parseInt('100px') ); // 100
alert( parseFloat('12.5em') ); // 12.5

alert( parseInt('12.3') ); // 12, only the integer part is returned
alert( parseFloat('12.3.4') ); // 12.3, the second point stops the reading
```

There are situations when `parseInt`/`parseFloat` will return `NaN`. It happens when no digits could be read:
```js
alert( parseInt('a123') ); // NaN, the first symbol stops the process
```

### The second argument of parseInt(str, radix)
The `parseInt()` function has an optional second parameter. It specifies the base of the numeral system, so `parseInt` can also parse strings of hex numbers, binary numbers and so on:
```js
alert( parseInt('0xff', 16) ); // 255
alert( parseInt('ff', 16) ); // 255, without 0x also works

alert( parseInt('2n9c', 36) ); // 123456
```

## Strings

### Backticks
1. Can evluate expresssions inside them using `&{...}`.
2. Can span multiple lines.
```js
let str = `Abhishek  // newline added here; totally valid
Arya`;
```
### Templpate Functions/Tagged Templates
- func`string`: `func` is an existing function and this syntax passes the `string` to that function.

### Escape Characters
`\n`, `\t`, `\b`, `\f`, `\v`, `\r`, `\\`, `\'`, `\"`

### String properties and methods
- `.length`: It is a property and not a function.
- `.toLowerCase()` 
- `.toUpperCase()`
- `.indexOf(substr, pos)`: It looks for the substr in `str`, starting from the given position `pos`, and returns the position where the match was found or `-1` if nothing can be found. `pos` is *optional*, skipping it means seach starting from `0`. This returns the first occurance index of `str`. 
- `.lastIndexOf(substr, pos)`: Same as above but it start searchhing from the end and returns last index of the substring if found.

**NOTE:** Be careful of `str.indexOf(substr, pos)` inside `if`, because if substring is found at index `0` then if treats `0` as `false`.

### The bitwise NOT trick
`if ( ~str.indexOf("...") )`: This is `true` only if there is a match. Why? for 32-bit integers `~n` equals `-(n+1)`, `~n` is zero only if `n == -1` (or no substring match).

- `.includes(substr, pos)`
- `.startsWith(str)`
- `.endsWith(str)`

### Extracting a substring
| method|selects…	|negatives|
|---|---|---|
|slice(start, end)|	from start to end (not including end)|	allows negatives|
|substring(start, end)|	between start and end|	negative values mean 0|
|substr(start, length)|	from start get length characters	|allows negative start|

### Getting a characher
```js
let str = 'Abhishek';

alert(str[0]); // A
alert(str[3]); // i
alert(str[7]); // k
```

This can return `undefined` if string is empty. Use `str.charAt(0)` to make sure that empty string (`""`) is returned on empty string.

**Strings are immutable:** We cannot change a single character in a string by using `string_name[index]`.
```js
let str = 'Abhishek';

str[0] = 'T'; // error
```

### Unicode compatibility in strings 
- [In string comparison](https://javascript.info/string#comparing-strings)
- [Internals, Unicode](https://javascript.info/string#internals-unicode)
