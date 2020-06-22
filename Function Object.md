# Global object, Function object, NFE, the "new Function" syntax

## Global Object
Every Javascript environment has a *"global"* object wich holds variables that should be available everywhere. In a **browser it is named `window`**, for **Node.js it is `global`**, for other environments it may have another name. Recently, `globalThis` was added to the language, as a **standardized name for a global object**, that should be supported across all environments.

- Any property can be directly accessed normally using either `.` or `[]` syntax.
- In a browser, global functions and variables declared with `var` (not `let`/`const`!) become the property of the global object:
```js
var gVar = 5;

alert(window.gVar); // 5 (became a property of the global object)
```

```js
let gLet = 5;

alert(window.gLet); // undefined (doesn't become a property of the global object)
```

- How do we make truly global variables then? Avoid global variables but, if a value is so important that you'd like to make it available globally, write it directly as a property:

```js
// make current user information global, to let all scripts access it
window.currentUser = {
  name: "John"
};

// somewhere else in code
alert(currentUser.name);  // John

// or, if we have a local variable with the name "currentUser"
// get it from window explicitly (safe!)
alert(window.currentUser.name); // John
```

### Using in Polyfills
We can check if a language feature is avalibale or not using a global object. [Example.](https://javascript.info/global-object#using-for-polyfills)

## Function object
- A function is an object in Javascript. 
- **Properties** (*can't access them from inside a function body using `this` or even function name*)
  - `name` - name of the function in `string` type, if name is not there like in function expressions, the first variable it's assigned to becomes its name.  
  - `length` - number of arguments
- There are cases when there’s no way to figure out the right name. In that case, the name property is empty string. Ex - `let arr = [function() {}];`.
- We can also add **custom properties** just like we would in an normal object.
- **A property is not a variable:** A property assigned to a function like `sayHi.counter = 0` does not define a local variable `counter` inside it. In other words, a property counter and a variable `let counter` are two unrelated things.

## Named Function Expression (NFE)
- We can have name of a function while defining a regular function expression:
```js
let sayHi = function func(who) {    // notice the 'func' addition here
  alert(`Hello, ${who}`);
};
```
This acts like a `this` for function objects. When we assign function to some other variable, inside its body it may be calling itself using old name. Using NFE will replace `func` with current name of the function.

```js
let sayHi = function(who) {
  if (who) {
    alert(`Hello, ${who}`);
  } else {
    sayHi("Guest"); // Error: sayHi is not a function
  }
};

let welcome = sayHi;
sayHi = null;

welcome(); // Error, the nested sayHi call doesn't work any more!
```

```js
let sayHi = function func(who) {
  if (who) {
    alert(`Hello, ${who}`);
  } else {
    func("Guest"); // Now all fine
  }
};

let welcome = sayHi;
sayHi = null;

welcome(); // Hello, Guest (nested call works)
```
- There's no such thing for Function Declaration.

## The "new Function" syntax
Another syntax to decalre a function: 

**Syntax:**
```js
let func = new Function ([arg1, arg2, ...argN], functionBody);
```

```js
let sum = new Function('a', 'b', 'return a + b');

alert( sum(1, 2) ); // 3

let sayHi = new Function('alert("Hello")');   // function without arguments

sayHi(); // Hello
```

- Functions created with new Function, have `[[Environment]]` referencing the *global Lexical Environment*, not the *outer* one. Hence, they cannot use outer variables.
```js
function getFunc() {
  let value = "test";

  let func = new Function('alert(value)');

  return func;
}

getFunc()(); // error: value is not defined
```
If it would've been normal behaviour, then `func` would've taken value from its *outer* environment `getFunc` and not *global* environment.
