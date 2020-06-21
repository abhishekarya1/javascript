# JSON
The JSON (**JavaScript Object Notation**) is a general format to represent values and objects. It is described as in RFC 4627 standard. Initially it was made for JavaScript, but many other languages have libraries to handle it as well. So it's easy to use JSON for data exchange when the client uses JavaScript and the server is written on Ruby/PHP/Java/Whatever.

JavaScript provides methods:
- `JSON.stringify` to convert objects into JSON.
- `JSON.parse` to convert JSON back into an object.

## JSON.stringify
The method `JSON.stringify(student)` takes the object and converts it into a string.

The resulting json string is called a *JSON-encoded* or *serialized* or *stringified* or *marshalled* object. We are ready to send it over the wire or put into a plain data store.

Please note that a JSON-encoded object has several important differences from the object literal:
- **Strings use double quotes**. No single quotes or backticks in JSON. So `'John'` becomes `"John"`.
- Object **property names are double-quoted** also. That’s obligatory. So `age:30` becomes `"age":30`.

**Usage:**
```js
let student = {
  name: 'John',
  age: 30,
  isAdmin: false,
  courses: ['html', 'css', 'js'],
  wife: null
};

let json = JSON.stringify(student);

alert(typeof json); // we've got a string!

alert(json);
/* JSON-encoded object:
{
  "name": "John",
  "age": 30,
  "isAdmin": false,
  "courses": ["html", "css", "js"],
  "wife": null
}
*/
```
JSON does not support comments. Adding a comment to JSON makes it invalid.

JSON can be applied to primitives as well:
- Objects `{ ... }`
- Arrays `[ ... ]`
- Primitives:
  - `strings`
  - `numbers`
  - `boolean`
  - `null`
  
```js
  // a number in JSON is just a number
alert( JSON.stringify(1) ) // "1"

// a string in JSON is still a string, but double-quoted
alert( JSON.stringify('test') ) // "test"

alert( JSON.stringify(true) ); // "true"

alert(JSON.stringify(null) );  // "null"

alert( JSON.stringify([1, 2, 3]) ); // [1,2,3]
```
  
JSON is data-only language-independent specification, so some JavaScript-specific object properties are skipped by `JSON.stringify`.

Namely:
- Function properties (**Methods**).
- Symbolic properties (**Symbols**).
- Properties that store `undefined`.

```js
let user = {
  sayHi() { // ignored
    alert("Hello");
  },
  [Symbol("id")]: 123, // ignored
  something: undefined // ignored
};

alert( JSON.stringify(user) ); // {} (empty object)
```
**Nested objects are automatically converted**

**Avoid circular references**

###  Custom "toJSON"
`JSON.stringify` automatically calls it if available. Some objects like `Date` already have it built-in, and sometimes we can define it in out object.

## JSON.parse
To decode a JSON-string.
Example -
```js
// stringified array
let numbers = "[0, 1, 2, 3]";

numbers = JSON.parse(numbers);

alert( numbers[1] ); // 1
```
