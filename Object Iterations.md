# Object Iterations
- `Object.keys(obj)` – returns an array of keys.
- `Object.values(obj)` – returns an array of values.
- `Object.entries(obj)` – returns an array of `[key, value]` pairs.

- They all ignore `Symbols` in an object.

- The first difference is that we have to call `Object.keys(obj)`, and not `obj.keys()`.
  1.  The main reason is flexibility. Remember, objects are a base of all complex structures in JavaScript. So we may have an object of our own like data that implements its own `data.values()` method. And we still can call `Object.values(data)` on it.
  2. The second difference is that `Object.*` methods return "real" array objects, not just an iterable. That's mainly for historical reasons.

Example:
```js
let user = {
  name: "John",
  age: 30
};

// Object.keys(user) = ["name", "age"]
// Object.values(user) = ["John", 30]
// Object.entries(user) = [ ["name","John"], ["age",30] ]
```

## Summary
Use `Object.*(obj)` functions to get arrays for Object keys, values, or both. We can't use `obj.*()` without explicitly creating them first unlike Map and Set where they're predefined automatically.
