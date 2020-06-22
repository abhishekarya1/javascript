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
