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
