# Objects (Basic)

## Objects
- stores key-value pairs
- key is a propertyName and value is its propertyValue

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

**Returning an object:**
```js
function hi(){
	return {      // object to be returned
		name : 'Abhishek'
	};
}

let greet = hi();
alert(greet. name);
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
- Property can only be `string` or `symbols`. Other types are automatically converted to strings. For instance, a number `0` becomes a string `"0"` when used as a property key:
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

## Garbage collection
- Concept of *reachability*.
- ["Mark-and-Sweep" algorithm](https://javascript.info/garbage-collection#internal-algorithms)
- Collection optimizations - **Genreational**, **Incremental**, and **Idle-time** collections.

## Object methods and "this"
- functions in objects are called *methods*.
```js
function sayHello() // function definition
{ 
  alert("Hello");
}

let user = {};  // empty object

user.sayHello = SayHello; // adding key
user.sayHello();  // call
```
**Using function expression:**
```js
let user = {};

user.sayHello = function(){ alert("Hello"); };
```

**Shorthand:**
```js
let user = {
  name : 'Abhishek',
  
  sayHello() { alert("Hello"); }  // same as "sayHi: function(){...}"
};
```

### "this" keyword
- To access the object, a method can use the `this` keyword. This is a good way to make objects "portable" i.e. we can copy an object into multiple objects and do not need to change the code inside, which references current object everytime.
- ["this" is not *bound*](https://javascript.info/object-methods#this-is-not-bound): `this` can occur inside any function outside the object, an will refer to any object the function is added to and will change according to the context during *runtime*.
- If `this` is in a function only and that function is not in any object, then we get `undefined`. [Important Example](https://javascript.info/object-methods#using-this-in-object-literal)
- Arrow funcitons can't have their own `this`, we need to declare another function as a wrapper for arrow function to use `this`.

## Constructor Functions
Constructor functions technically are regular functions. There are two conventions though:
1. They are named with capital letter first.
2. They should be executed only with "new" operator.
```js
function User(name) {   // constructor function
  this.name = name;
  this.isAdmin = false;
}

let user = new User("Jack");

alert(user.name); // Jack
alert(user.isAdmin); // false
```

### new
When a function is executed with new, it does the following steps:
1. A new empty object is created and assigned to this.
2. The function body executes. Usually it modifies `this`, adds new properties to it.
3. The value of `this` is returned.

### return with Constructors
Usually, constructors do not have a `return` statement. Their task is to write all necessary stuff into `this`, and it automatically becomes the result.
<br><br>
But if there is a `return` statement, then the rule is simple:
  - If `return` is called with an object, then the object is returned instead of `this`.
  - If `return` is called with a primitive, it's ignored.

### Omitting Parentheses
```js
let user = new User; // <-- no parentheses
// same as
let user = new User();
```

### Funtion calling with new
- Funtions can be called using *new* and if they return an object, then that object will be returned instead of `this`. [Example](https://javascript.info/constructor-new#two-functions--one-object).

## Optional chaining (?.)
The `?.` syntax has three forms:

1. `obj?.prop` – returns `obj.prop` if obj exists, otherwise `undefined`.
2. `obj?.[prop]` – returns `obj[prop]` if obj exists, otherwise `undefined`.
3. `obj?.method()` – calls `obj.method()` if obj exists, otherwise returns `undefined`.
As we can see, all of them are straightforward and simple to use. The ?. checks the left part for null/undefined and allows the evaluation to proceed if it's not so.

A chain of `?.` allows to safely access nested properties.

Still, we should apply `?.` carefully, only where it's ok that the left part doesn't exist.

So that it won't hide programming errors from us, if they occur.

## Symbols
A "symbol" represents a unique identifier.

**Syntax:**
```js
let symbol_name = Symbol("symbol_desc");  // description is just a label 
```

```js
let id1 = Symbol("id");
let id2 = Symbol("id");

alert(id1 == id2); // false
```
- **Symbols can't automatically convert to string.** Use `.toString(symbol_name)` for that.
- Use `symbol.description` to show the description only:
```js
let id = Symbol("id");
alert(id.description); // id
```

### "Hidden" properties
- Third party code (maybe from another js library) can make same name/description symbols after forking our code and they won't clash with symbols that we already have with the same name (as name/desc doesn't matter) in our code, they even get skipped in `for...in` loop iteration.
- `Object.keys(user)` also ignores them. That's a part of the general "hiding symbolic properties" principle. If another script or a library loops over our object, it won't unexpectedly access a symbolic property.
- In contrast, `Object.assign` copies both string and symbol properties.

### Using Symbol in an object as keyname ([...]) 
```js
let id = Symbol("id");

let user = {
  name: "John",
  [id]: 123 // not "id: 123"
};
```
That's because we need the value from the variable `id` as the key, not the string `"id"`.

### Global symbols and Global symbol registry (GSR)
There is an internal "global symbol registry" maintained by the js engine, we can add to it using `Symbol.for(name)`. For same name/desc, it stores only one key and return it i.e. for the same name/desc, only one symbol is made, stored, and returned everytime.
```js
let foo = Symbol.for("foo1");	// creates symbol with name foo1 in GSR

let foobar = Symbol.for("foo1"); // same symbol's as above reference is returned and stored in foobar 
```

### Symbol.keyFor
`Symbol.keyFor` returns name/desc for a given symbol key which is of type `string`. It *only* uses GSR internally.
```js
let foo = Symbol("name");

alert( Symbol.keyFor(foo) );
```

### System symbols
There exist many "system" symbols that JavaScript uses internally, and we can use them to fine-tune various aspects of our objects. For example: `Symbol.toPrimitive` allows us to describe object to primitive conversion.

## Object to primitive conversion
- All objects are `true` in a boolean context. There are only numeric and string conversions.
- The `numeric` conversion happens when we subtract objects or apply mathematical functions. For instance, Date objects (to be covered in the chapter Date and time) can be subtracted, and the result of `date1 - date2` is the time difference between two dates.
- As for the` string` conversion – it usually happens when we output an object like `alert(obj)` and in similar contexts.

### Hints
Three variants of type conversion, so-called **"hints"**. 
1. `string`
2. `number`
3. `default`: When js is not sure of which is the context. eg. `+` can be concatenate or arithmetic addition.

The greater and less comparison operators, such as `< >`, can work with both strings and numbers too. Still, they use the "number" hint, not "default". That's for historical reasons.
<br>
<br>
All built-in objects except for one case (`Date` object, we'll learn it later) implement "default" conversion the same way as "number". So no need to remember all three.

### Conversion
To do the conversion, JavaScript tries to find and call three object methods:
1. Call `obj[Symbol.toPrimitive](hint)` – the method with the symbolic key `Symbol.toPrimitive (system symbol)`, if such method exists,
2. Otherwise if hint is `"string"`
try `obj.toString()` and `obj.valueOf()`, whatever exists.
3. Otherwise if hint is `"number"` or `"default"`
try `obj.valueOf()` and `obj.toString()`, whatever exists.
