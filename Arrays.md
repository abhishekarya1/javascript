# Arrays
An array can store elements of any type, even mixed.
<br>
Last element in an array, just like an object, may end with a comma.
## Creating and accessing
```js
let arr = new Array();    // constructor funtion way (array as an object)
let arr = [];   // popular and easy
```
Example:
```js
let fruits = ["Apple", "Orange", "Plum"];

alert( fruits[0] ); // Apple
alert( fruits[1] ); // Orange
alert( fruits[2] ); // Plum
```

Replace or add an element:
```js
fruits[2] = 'Pear'; // now ["Apple", "Orange", "Pear"]

fruits[3] = 'Lemon'; // now ["Apple", "Orange", "Pear", "Lemon"]
```

Length:
```js
alert(fruits.length); // 4
```

Print whole array:
```js
alert( fruits ); // Apple,Orange,Plum
```

### Array Methods
- `.pop()` - remove the last element and return it
- `.push()` - add element at the end 
- `.shift()` - remove the first element and return it
- `.unshift()` - add element at the start

We can add multiple elements at once with `push` and `unshift`:
```js
let fruits = ["Apple"];

fruits.push("Orange", "Peach");
fruits.unshift("Pineapple", "Lemon");

alert( fruits );  // ["Pineapple", "Lemon", "Apple", "Orange", "Peach"]
```

### Arrays are objects
- They are objects in which values are stored in contiguous locations in memory and the following operations are valid but never do them:
```js
let fruits = []; // make an array

fruits[99999] = 5; // assign a property with the index far greater than its length

fruits.age = 25; // create a property with an arbitrary name
```
- They are copied by reference just like Objects.

### Performance
`pop` and `push` are faster than `shift` and `unshift` because of element movement overhead.

### Loop for arrays (for...of)
```js
let fruits = ["Apple", "Orange", "Plum"];

// iterates over array elements
for (let fruit of fruits) {
  alert( fruit );
}
```

`for..in` can be used but don't use it as it's not optimized for arrays and is 10-100 times slower.

### A word about "length"
The length property automatically updates when we modify the array. To be precise, **it is actually not the count of values in the array, but the greatest numeric index plus one.**

For instance, a single element with a large index gives a big length:
```js
let fruits = [];
fruits[123] = "Apple";

alert( fruits.length ); // 124
```

Also, **it is editable** since it is a property. We can truncate the array by changing the value of `length` to a smaller value.


### new Array()
```js
let arr = new Array("Apple", "Pear", "etc");  // it is lengthy and obsolete
```

### Arrays as Strings
Arrays can only be converted to `string`.

```js
let arr = [1, 2, 3];

alert( arr ); // 1,2,3
alert( String(arr) === '1,2,3' ); // true


alert( [] ); // ""
alert( [1] + 1 ); // "11"
alert( [1,2] ); // "1,2"
alert( [1,2] + 1 ); // "1,21"
```

## More array methods
- [Link](https://javascript.info/array-methods)

## Iterables
How does js know to iterate over elements of objects and array like structures like `string`?
Ans: It does so with iterables. **Objects that can be used in `for..of` are called *iterable*.**
<br><br>
Technically, iterables must implement the method named `Symbol.iterator`. The result of `obj[Symbol.iterator]` is called an *iterator*. It handles the further iteration process.
- An iterator must have the method named `next()` that returns an object `{done: Boolean, value: any}`, here `done:true` denotes the end of the iteration process, otherwise the `value` is the next value.
- The `Symbol.iterator` method is called automatically by `for..of`, but we also can do it directly.
- Built-in iterables like strings or arrays, also implement `Symbol.iterator`.
<br><br>
[Example](https://javascript.info/iterable#symbol-iterator)

### Array.from
There's a universal method `Array.from` that takes an *iterable* or *array-like* value and makes a "real" Array from it. Then we can call array methods on it.
```js
let arrayLike = {
  0: "Hello",
  1: "World",
  length: 2
};

let arr = Array.from(arrayLike); // (*)
alert(arr.pop()); // World (method works)
```
