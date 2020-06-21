# Destructuring assignment
Destructuring assignment is a special syntax that allows us to "unpack" arrays or objects into a bunch of variables.

## Array destructuring

```js
let arr = [1, 2, 3];

let [a, b, c] = arr;

// sets a = arr[0], b = arr[1], c = arr[2]
```

- Array remains unmodified throughout.
- Ignore elements using commas: Leave empty those vars for which we don't want assignment to happen.

```js
let arr = [1, 2, 3];

let [a, , c] = arr;

// sets a = arr[0], b = undefined, c = arr[2]
```

- Works with any iterable on the right-side.
```js
let [a, b, c] = "abc"; // ["a", "b", "c"]
let [one, two, three] = new Set([1, 2, 3]);
```
- Assign to anything "assignable" on the left-side
```js
let user = {};
[user.name, user.surname] = "Abhishek Arya".split(' ');

alert(user.name); // Abhishek
```
- Looping with `.entries()`
```js
let user = {
  name: "John",
  age: 30
};

// loop over keys-and-values
for (let [key, value] of Object.entries(user)) {
  alert(`${key}:${value}`); // name:John, then age:30
}
```

For Map:
```js
let user = new Map();
user.set("name", "John");
user.set("age", "30");

for (let [key, value] of user) {
  alert(`${key}:${value}`); // name:John, then age:30
}
```

- Swap variables trick
```js
let guest = "Jane";
let admin = "Pete";

// Swap values: make guest=Pete, admin=Jane
[guest, admin] = [admin, guest];

alert(`${guest} ${admin}`); // Pete Jane (successfully swapped!)
```

### ...rest
If we want not just to get first values, but also to gather all that follows. We can use any variable name in place of `rest`. It is an **array of remaining elements** (i.e. it starts after the last explicit destructuring variable).
```js
let [name1, name2, ...rest] = ["Julius", "Caesar", "Consul", "of the Roman Republic"];

alert(name1); // Julius
alert(name2); // Caesar

// Note that type of `rest` is Array.
alert(rest[0]); // Consul
alert(rest[1]); // of the Roman Republic
alert(rest.length); // 2
```

### Default values
Absent values are assigned `undefined`. Provide default values with `=`.

```js
let arr = [9, 8, 7];

let [a = 1, b = 2, c = 3] = arr;

// a = 9, b = 8, c = 7

let arr1 = [];

let [a = 1, b = 2, c = 3] = arr1;

// a = 1, b = 2, c = 3
```

## Object destructuring
**New variables with the same name as property/key are created and assigned the corresponding property**. Syntax - `let {var1, var2} = {var1, var2, ...}`.

```js
let options = {
  title: "Menu",
  width: 100,
  height: 200
};

let {title, width, height} = options;

alert(title);  // Menu
alert(width);  // 100
alert(height); // 200
```
Properties `options.title`, `options.width` and `options.height` are assigned to the *corresponding* variables.

### Colon (:)
If we want to assign a property to a variable with another name, for instance, `options.width` to go into the variable named `w`, then we can set it using a colon:
```js
let options = {
  title: "Menu",
  width: 100,
  height: 200
};

// { sourceProperty: targetVariable }
let {width: w, height: h, title} = options;

// width -> w
// height -> h
// title -> title

alert(title);  // Menu
alert(w);      // 100
alert(h);      // 200
```
The colon shows **"what : goes where"**. In the example above the property `width` goes to `w`, property `height` goes to `h`, and `title` is assigned to the same name.

- Default assignments can be done with `=` the same way as in Arrays.
- We can combine `=` and `:`.
- `...rest` works too, the remaining part of the object here is made another objecct with the name `rest`.
Example -
```js
let options = {
  title: "Menu",
  height: 200,
  width: 100
};

// title = property named title
// rest = object with the rest of properties
let {title, ...rest} = options;

// now title="Menu", rest={height: 200, width: 100}
alert(rest.height);  // 200
alert(rest.width);   // 100
```

### Gotcha if there's no let
This won't work:
```js
let title, width, height;

// error in this line
{title, width, height} = {title: "Menu", width: 200, height: 100};
```

`{}` is treated as a normal code block only. To make it mean destructuring assignment, add `()` around it.

```js
let title, width, height;

// okay now
({title, width, height} = {title: "Menu", width: 200, height: 100});

alert( title ); // Menu
```

### Nested and Complex Destructuring
[Link](https://javascript.info/destructuring-assignment#nested-destructuring)
