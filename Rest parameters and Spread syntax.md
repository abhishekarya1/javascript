# Rest parameters and Spread syntax
Both are there to enable variable arguments in a function. Like:
- `Object.assign(dest, obj1, obj2, ..., objN) `
- `Math.max(arg1, arg2, ..., argN)`

## ...rest
- Works the same as in destructured assignments, **they create an array to store remaining arguments**
- Must be last in argument list otherwise error

```js
function sumAll(...args) { // args is the name for the array
  let sum = 0;

  for (let arg of args) sum += arg;   // can be used here as it is an iterable

  return sum;
}

alert( sumAll(1) ); // 1
alert( sumAll(1, 2) ); // 3
alert( sumAll(1, 2, 3) ); // 6
```

## arguments
- It is a special array-like object.
- **Arrow functions do not have "arguments".**
- It exists built-in in every function and stores number (`length` property) and every argument where it can be accessed as: `argument[n]`.
```js
function showName() {
  alert( arguments.length );
  alert( arguments[0] );
  alert( arguments[1] );

  // it's iterable
  // for(let arg of arguments) alert(arg);
}

// shows: 2, Julius, Caesar
showName("Julius", "Caesar");

// shows: 1, Abhishek, undefined (no second argument)
showName("Abhishek");
```

## Spread syntax (...arr)
- Does the *opposite* of `...rest`,  it "expands" an iterable object like an array into the list of arguments.
```js
let arr = [3, 5, 1];

alert( Math.max(...arr) ); // 5 (spread turns array into a list of arguments)
```

- We can use multiple arrays like this and even mix with normal values:
```js
let arr1 = [1, -2, 3, 4];
let arr2 = [8, 3, -8, 1];

alert( Math.max(1, ...arr1, 2, ...arr2, 25) ); // 25
```

- Can work with any *iterable*
```js
let str = "Hello";

alert( [...str] ); // H,e,l,l,o
```
### Copying arrays and objects using Spread syntax
```js
let arr = [1, 2, 3, 4, 5];

let arrCopy = [...arr];

// the references are different (arr & arrCopy) but contents will be exactly same
```

**Use ...obj instead of Object.assign():**
```js
let obj = { a: 1, b: 2, c: 3 };
let objCopy = { ...obj };

// the references are different (obj & objCopy) but contents will be exactly same
```
