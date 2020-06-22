# Variable Scope
- Variables declared inside a code block `{}` are visible only inside it.
- Re-declaration of variables is an error.
- Nested functions can access all the *"outer"* variables of the parent function it is declared inside of.

## Lexical Environments
- Imaginary `object` that keeps record of variables and functions in the current scope and also has a reference to the outer scope/lexical env.
- Every variable is in a **"dead zone"** from the start of the code block till it the point is declared using `let`. It is there in lexical environment of that block (as a key) but it's value is `undefined` till it is declared. 
- This is not the case with **functions**, they become available to use as soon as the code block is entered, even if they're declared later in the same code block. (Just like in C/C++ but there functions can only be in global lexical environment/scope).
- Returning a function makes the function being returned have reference to the outer lexical environment of the lex. env. it was **created** in and **not the one it was called in**.

[Illustrations](https://javascript.info/closure#lexical-environment)
<br><br>
[Important Example: Returning a function](https://javascript.info/closure#which-variables-are-available)
<br><br>
[Important Example: Different calls make different lexical environments](https://javascript.info/closure#are-counters-independent)
<br><br>
[Important Example: "non-existing" vs. "unitialized" variables](https://javascript.info/closure#is-variable-visible)

# var
- Old and obsolete
  1. It has **no code block scope, it has either *function* or *global* scopes**. i.e. if any variable declared using `var` can be accessed beyond any loops, `if-else`, or `{}` block. This is because a long time ago in JavaScript blocks had no *Lexical Environments*. And var is a remnant of that.
  ```js
  if (true) {
  var test = true; // use "var" instead of "let"
  }

  alert(test); // true, the variable lives after if
  ```
  
  2. We can **redeclare a variable any number of times.** 
  ```js
  var user = "Pete";

  var user = "John"; // this "var" does nothing (already declared)
  // ...it doesn't trigger an error

  alert(user); // John
  ```
  
  3. **Hoisting:** **"var" variables can be declared below their use.** `var` variables are defined from the beginning of the function, no matter where the definition is (assuming that the definition is not in the nested function, if it's in another code block then they're ignored and we **can** use the variable). This behaviour is just like functions in new js.
  ```js
  var name;
  
  alert(name);  // will alert 'Abhishek' without any error
  
  name = 'Abhishek';
  ```
 We call it hoisting because variables are *"raised"* to the top of the function this way with `var`.
 
  - **Declarations are hoisted, but assignments are not.**
   ```js
  alert(phrase);

  var phrase = "Hello"; // alerts undefined 
   ```
   In the above example `phrase` declaration was hoisted and thus no error, but the assignment to `"Hello"` was not hoisted and thus, `undefined` was alerted.
 
 ### IIFE
 - **Immediately-invoked function expressions:** They emulate a code block by using function syntax. Since `var` variables can only follow scpope rules in a function. We create a function and immediately exectute it to emulate code block. No need of them with `let` in newer js.
 
 ```js
// Different Ways to create IIFE

(function() {
  alert("Parentheses around the function");
})();

(function() {
  alert("Parentheses around the whole thing");
}());

!function() {
  alert("Bitwise NOT operator starts the expression");
}();

+function() {
  alert("Unary plus starts the expression");
}();
 ```
