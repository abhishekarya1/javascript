# Objects (Basic)

## Objects
- stores key-value pairs
- key is a property and value is its value

**Syntax:** Creating Objects
```js
let user = new Object(); // "object constructor" syntax
let user = {};  // "object literal" syntax
```

**Example:** 
```js
let user = {     // an object
  name: "John",  // by key "name" store value "John"
  age: 30,        // by key "age" store value 30, COMMA IS OPTIONAL IN THE LAST K-V PAIR
};
```

### Access using Dot Notation
```js
alert( user.name ); // John
alert( user.age ); // 30
```

**Adding Values:** 
```js
user.isAdmin = true;
```

**Deleting Value:** 
```js
delete user.isAdmin;
```

**Multiword property names:**
```js
let user = {
  name: "John",
  age: 30,
  "likes birds": true  // multiword property name must be quoted
};
```
### Object declared as const
It may be modified but `const` makes the object variable constant i.e we cannot put another object into this `const` object.
```
const student = {
name : "Abhishek",
batch : 1
};

student.batch = 5;  // no error

student = { name : "Foo", batch: 4};  // error

let intern = {};
student = intern; // error
```
