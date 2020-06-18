# Maps and Sets

## Map
Map is a collection of keyed data items, just like an Object. But the main difference is that Map allows keys of any type, unlike Objects that allow only `string` and `symbol`.
<br><br>
Methods and properties are:
- `new Map()` – creates the map.
- `map.set(key, value)` – stores the value by the key.
- `map.get(key)` – returns the value by the key, undefined if key doesn’t exist in map.
- `map.has(key)` – returns true if the key exists, false otherwise.
- `map.delete(key)` – removes the value by the key.
- `map.clear()` – removes everything from the map.
- `map.size` – returns the current element count.

```js
let map = new Map();

map.set('1', 'str1');   // a string key
map.set(1, 'num1');     // a numeric key
map.set(true, 'bool1'); // a boolean key

// remember the regular Object? it would convert keys to string
// Map keeps the type, so these two are different:
alert( map.get(1)   ); // 'num1'
alert( map.get('1') ); // 'str1'

alert( map.size ); // 3
```

**Avoid using map[propertyName] with Maps:** It will work but it is treating Map like a regular js Object which should be avoided. Use Map methods instead.

**Map can also use objects as keys.**

### Chaining
Every `map.set` call returns the map itself, so we can *"chain"* the calls:
```js
map.set('1', 'str1')
  .set(1, 'num1')
  .set(true, 'bool1');
```

### Iteration over Map
For looping over a map, there are 3 methods:

- `map.keys()` – returns an iterable for keys,
- `map.values()` – returns an iterable for values,
- `map.entries()` – returns an iterable for entries `[key, value]`, it’s used by default in `for..of`.

They're all insertion order unlike regular `Object`.

### Object.entries: Map from Object

Map insertion in array form: 

```js
// array of [key, value] pairs
let map = new Map([
  ['1',  'str1'],
  [1,    'num1'],
  [true, 'bool1']
]);

alert( map.get('1') ); // str1
```

Conversion from Object to Map: FIrst object gets converted to arrays using `Object.entries` and then map is created using `new`.

```js
let obj = {
  name: "John",
  age: 30
};

let map = new Map(Object.entries(obj));

alert( map.get('name') ); // John
```

### Object.fromEntries: Object from Map
Reverse of the above.
```js
let map = new Map();
map.set('banana', 1);
map.set('orange', 2);
map.set('meat', 4);

let obj = Object.fromEntries(map.entries()); // make a plain object (can write just "map" in param)

// done!
// obj = { banana: 1, orange: 2, meat: 4 }

alert(obj.orange); // 2
```

## Set
A Set is a special type collection – "set of values" (without keys), where each value may occur only once.

Its main methods are:
- `new Set(iterable)` – creates the set, and if an `iterable` object is provided (usually an array), copies values from it into the set.
- `set.add(value)` – adds a value, returns the set itself.
- `set.delete(value)` – removes the value, returns `true` if value existed at the moment of the call, otherwise `false`.
- `set.has(value)` – returns `true` if the value exists in the set, otherwise `false`.
- `set.clear()` – removes everything from the set.
- `set.size` – is the elements count.

```js
let set = new Set();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

// visits, some users come multiple times
set.add(john);
set.add(pete);
set.add(mary);
set.add(john);
set.add(mary);

// set keeps only unique values
alert( set.size ); // 3

for (let user of set) {
  alert(user.name); // John (then Pete and Mary)
}
```

### Iteration over Sets
We can loop over a set either with `for..of` or using `forEach`.
<br><br>
The same methods Map has for iterators are also supported:

- `set.keys()` – returns an iterable object for values,
- `set.values()` – same as `set.keys()`, for compatibility with Map,
- `set.entries()` – returns an iterable object for entries `[value, value]`, exists for compatibility with Map.