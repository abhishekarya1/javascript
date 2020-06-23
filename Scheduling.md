# Scheduling: setTimeout and setInterval
There are two methods for it:
  - `setTimeout` allows us to run a function once after the interval of time.
  ```js
  let timerId = setTimeout(func|code, [delay], [arg1], [arg2], ...)
  ```
  ```js
  clearTimeout(timerId);
  ```
  - `setInterval` allows us to run a function repeatedly, starting after the interval of time, then repeating continuously at that interval.
  ```js
  let timerId = setInterval(func|code, [delay], [arg1], [arg2], ...)
  ```
  ```js
  clearInterval(timerId);
  ```

### Differences
`setInterval` does not take into account the delay caused by function execution, `setTimout` taked it into account and has precisely the amount of time specified between function calls.

### Similarities
Nested `setTimeout` can be used inplace of `setInterval`.

## Garbage collection and setInterval/setTimeout callback
When a function is passed in setInterval/setTimeout, an internal reference is created to it and saved in the scheduler. It prevents the function from being garbage collected, even if there are no other references to it.
```js
// the function stays in memory until the scheduler calls it
setTimeout(function() {...}, 100);
```
For `setInterval` the function stays in memory until `clearInterval` is called.

## Zero delay setTimeout
There's a special use case: `setTimeout(func, 0)`, or just `setTimeout(func)`.

This schedules the execution of `func` as soon as possible. But **the scheduler will invoke it only after the currently executing script is complete.((

So the function is scheduled to run "right after" the current script.

For instance, this outputs "Hello", then immediately "World":

```js
setTimeout(() => alert("World"));

alert("Hello");
```

The first line "puts the call into calendar after 0ms". But the scheduler will only "check the calendar" after the current script is complete, so "Hello" is first, and "World" – after it.
