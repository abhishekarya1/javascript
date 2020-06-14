# Code Quality

## Debugging in Chrome
### Sources
To see `.js` file and code inside of it

### Console
To run our own js code in terminal fashion

### Breakpoints
Clicking the line number in sources allow us to create points at which code execution pauses. While the code is paused, we can examine current variables, execute commands in the console etc. In other words, we can debug it.
<br><br>
**Conditional Breakpoints:** Right click on the line number allows to create a *conditional breakpoint*. It only triggers when the given expression is *truthy*.

### Debugger command
Write `debugger;` anywhere inside code to stop execution at that point.

### Tracing
Various kinds of [steps](https://javascript.info/debugging-chrome#tracing-the-execution). 

### Logging
Anything output using `console.log()` can be seen **only** in Console panel.

## Coding Style
[Style Guides](https://javascript.info/coding-style#style-guides) and [Linters](https://javascript.info/coding-style#automated-linters)

## Comments
There's a special syntax [JSDoc](https://en.wikipedia.org/wiki/JSDoc) to document a function: usage, parameters, returned value. Most editors like Jetbrains Webstorm can understand them as well and use them to provide autocomplete and some automatic code-checking. Also, there are tools like JSDoc 3 that can generate HTML-documentation from the comments.

## Automated testing with Mocha
- Why tho?
  - writes some code,
  - tests it with a few test cases,
  - adds some more code,
  - tests it again, but forgets to test exactly like before (skipping some tests, etc...)

### Behavior Driven Development (BDD)
- Agile development process that encourages collaboration among developers, QA and non-technical or business participants in a software project. **BDD is three things in one: tests** AND **documentation** AND **examples**.
- The process:
  - write *specification* aka *spec* which includes tests
  - implementation/coding 
  - use a framework like Mocha to test spec on implementation
  - add more spec, and then implement them, and test again
  - repeat till the functionality is ready
- The development is **iterative** in BDD.

### Usage
- Demo with Mocha (`describe`, `it`), Chai (`assert`ions) [here](https://plnkr.co/edit/8OgvvBpZI90lA1If?p=preview).

## Babel and Polyfills
[Babel](https://babeljs.io/) is a transpiler. It rewrites modern JavaScript code into the previous standard. It has two parts:
  1. Direct Transpiler - rewrites the code. The developer runs it on their own computer. It rewrites the code into the older standard. And then the code is delivered to the website for users.
  2. Polyfill - sometimes the modern code cannot be directly transpiled to the older one because of limitations in availability of language constructs. A script that updates/adds new functions is called 'polyfill'. It "fills in" the gap and adds missing implementations/constructs. 
