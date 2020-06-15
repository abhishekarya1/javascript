# Objects (Basic)

## Objects
- stores key-value pairs
- key is a property and value is its value

**Syntax:** Creating Objects
```js
let user = new Object(); // "object constructor" syntax
let user = {};  // "object literal" syntax
```

**Adding values to empty object:**
```js
let user = {};  // empty object

user.name = 'Abhishek';   // will create name key automatically
user.age = 22;    //will create age key automatically
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
It may be modified but `const` makes the object variable constant i.e we cannot change it as a whole (`{...}`).
```
const student = {
name : "Abhishek",
batch : 1
};

student.batch = 5;  // no error

student = { name : "Foo", batch: 4};  // error
```

### Square brackets
1. Only way to refer to multiword keys:
```js
user.likes birds = false;  // won't work

user["likes birds"] = false;  // correct, IF KEY IS QUOTED IN OBJECT, IT MUST BE QUOTED INSIDE [] EVEN IF SINGLE WORD 
```

2. We can get key during runtime for access, unlike dot notation (`.`):
```js
let user = {
  name: "John",
  age: 30
};

let key = prompt("What do you want to know about the user?", "name");

// access by variable
alert( user[key] ); // output: John ; (if entered "name")
```

### Computed properties
3. We can use `[]` to insert runtime values for key:
```js
let fruit = prompt("Which fruit to buy?", "apple");

let bag = {
  [fruit]: 5, // the name of the property is taken from the variable fruit, if a visitor enters "apple", bag will become {apple: 5}
};

alert( bag.apple ); // 5 if fruit="apple"
```

- We can use more complex expressions inside square brackets:
```js
let fruit = 'apple';
let bag = {
  [fruit + 'Computers']: 5 // bag.appleComputers = 5
};
```

### Property value shorthand
```js
let name = 'Abhishek';
let age = 22;

let student = {
name : name,
age : age
};

alert(student.age); // output: 22
```

**Shorthand:**
```js
let name = 'Abhishek';
let age = 22;

let student = {
name, // same as name:name
age   // same as age:age
};
```

### Object name
- There are no limitations on property names. They can be any reserved words or any strings or symbols.
- Other types are automatically converted to strings. For instance, a number `0` becomes a string `"0"` when used as a property key:
```js
let obj = {
  0: "test" // same as "0": "test"
};

// both alerts access the same property (the number 0 is converted to string "0")
alert( obj["0"] ); // test
alert( obj[0] ); // test (same property)
```

### Property existence test, "in" operator
- When we access a property which does not exist, it returns `undefined`.
- `in` operator returns a boolean value.
```js
let user = { name: "John", age: 30 };

alert( "age" in user ); // true, user.age exists
alert( "blabla" in user ); // false, user.blabla doesn't exist
```

### for...in loop
```js
let user = {
  name: "John",
  age: 30,
  isAdmin: true
};

for (let key in user) {
  // keys
  alert( key );  // name, age, isAdmin
  // values for the keys
  alert( user[key] ); // John, 30, true
}
```

**What's the ordering in an object which for...in loop traverses?**
<br>
**Ans:** Integer properties are sorted, others appear in creation order. If a number is defined as a `string` in the object, convert it to `number` using `+` operator.

## Object copying, references
When an object is copied to another variable, only the reference (address) to the original object is stored in the new variable i.e. a shallow copy. Changes to new variable affect the original as well. This behaviour is unlike the other 7 primitives.
```js
let user = { name: "John" };

let admin = user; // copy the reference
```

### Comparison by reference
- `==` and `===` work the same for objects. Two variables will only be equal if they refer to the same object.
- Two exacly same objects will not be equal either.
```js
let a = {};
let b = {}; // two independent objects

alert( a == b ); // false
```

## Deep copying objects (Object.assign())
```js
let user = { name: "John" };

let permissions1 = { canView: true };
let permissions2 = { canEdit: true };

// copies all properties from permissions1 and permissions2 into user
Object.assign(user, permissions1, permissions2);

// now user = { name: "John", canView: true, canEdit: true }
```
- If the copied property name already exists, it gets overwritten.
