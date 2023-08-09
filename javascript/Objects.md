<div align="center"><h1>Objects</h1></div>
<h3>
<ol>
<li>An object is a collection of related data and/or functionality.</li>
<li>An Object is represented as key:value pair</li>
</ol>
</h3>

## Access, Modify, Delete and Add Properties to an object

```js
const user = { name: "Mohammed Saif", age: 24 };

// Accessing
console.log(user.name);

// Modifying
user.name = "Akbar Ali";

// Deleting
delete user.age;

// Adding
user.profile = "Web Developer";

console.log(user); // { name: 'Akbar Ali', profile: 'Web Developer' }
```

<br/>
<br/>

# Interview Questions

<ol>
<li><h3>What will the output of the following code snippet?</h3>

```js
const func = (function (a) {
  delete a;
  return a;
})(5);

console.log(func);
```

<h4>Answer: 5</h4>
<p>delete a; is attempting to delete the property named a from the current context. However, it's important to understand that a here is a parameter of the IIFE, not an object property. The delete operator is used to delete properties from objects, not variables or function parameters.</p>
</li>
<li><h3>What if you want a multiword key in your object?</h3>
<h4>Answer: </h4>
<p>Write it in "double quotes".<br/>
"like the video": true
</p>
</li>
<li><h3>How can you access a multiword key of an object?</h3>
<h4>Answer: </h4>
<p>Use “square bracket notation”</p>

```js
let user = {};
user["like the video"] = true;
delete user["like the video"];
```

</li>

<li><h3>Computed Properties or Adding Dynaming Key:Value pairs</h3>
<h4>Answer: </h4>

```js
let property = "firstName";
let name = "Rahul Oberoi";
let person = { [property]: name };
```

**Square bracket notation can be used for unknown and complex key names and dot notation is used for known and simple keys.**

</li>
<li><h3>How to access keys in an object?</h3>
<h4>Answer: </h4>

```js
let user = { name: "Rahul", age: 24 };
for (let key in user) {
  alert(key); // name, age
  alert(user[key]); // Rahul, 24
}
```

</li>
<li><h3>What will the otuput of the following code snippet?</h3>

```js
const obj = { a: "one", b: "two", a: "three" };
console.log(obj);
```

<h4>Answer: </h4>

```js
{ a: "three", b: "two" }
```

The object will take the last specified value of the same property.

</li>
<li><h3>Create a function multiplyByTwo(obj) that multiplies all numeric property values of obj by 2.</h3>

```js
// Initial let nums = { a: 100, b: 200, title: "My nums" };

multiplyNumeric(nums);

//expected output nums = { a: 200, b: 400, title: "My nums" };
```

<h4>Answer: </h4>

```js
function multiplyByTwo(obj) {
  for (let key in obj) {
    if (typeof obj[key] == "number") {
      obj[key] *= 2;
    }
  }
}
```

</li>
<li><h3>Find the output of the following code snippet</h3>

```js
const a = {};
const b = { key: "b" };
const c = { key: "c" };

a[b] = 123;
a[c] = 456;

console.log(a[b]);
```

<h4>Answer: 456</h4>
<p>Object keys are automatically converted into strings. We are trying to set an object as a key to object `a`, with the value of `123`.

However, when we stringify an object, it becomes `"[object Object]"`. So what we are saying here, is that `a["[object Object]"] = 123`. Then, we can try to do the same again. `c` is another object that we are implicitly stringifying. So then, `a["[object Object]"] = 456`.

Then, we log `a[b]`, which is actually `a["[object Object]"]`. We just set that to `456`, so it returns `456`.

</p>
</li>
<li><h3>What is JSON.Stringify and JSON.parse ?</h3>
<h4>Answer: </h4>
<p>
JSON.stringify
<ul>
<li>
It's a method in JavaScript used to convert a JavaScript object or value into a JSON string.
</li><li>
Converts a JavaScript object into its JSON representation, which is a string format.</li><li>
Useful for sending data to a server or storing data in a text-based format.</li>
</ul><br/>
JSON.parse:<br/><br/>
<ul>
<li>
It's a method in JavaScript used to parse a JSON string and convert it into a JavaScript object.</li><li>
Converts a JSON string back into its JavaScript object form, allowing you to work with the data as objects.</li><li>
Useful for processing data received from a server or stored in a text-based format.</li>
</ul>
</p>

</li>

<li><h3>What's the output?</h3>

```js
const user = { name: "Lydia", age: 21 };
const admin = { admin: true, ...user };

console.log(admin);
```

<h4>Answer: </h4>

```js
{ admin: true, name: "Lydia", age: 21 }
```

</li>
<li><h3>What's the output of the following code snippet?</h3>

```js
const settings = { username: "lydiahallie", level: 19, health: 90 };

const data = JSON.stringify(settings, ["level", "health"]);
console.log(data);
```

<h4>Answer: {"level":19, "health":90}</h4>
<p>
The second argument of `JSON.stringify` is the *replacer*. The replacer can either be a function or an array, and lets you control what and how the values should be stringified.

If the replacer is an _array_, only the property names included in the array will be added to the JSON string. In this case, only the properties with the names `"level"` and `"health"` are included, `"username"` is excluded. `data` is now equal to `"{"level":19, "health":90}"`.

If the replacer is a _function_, this function gets called on every property in the object you're stringifying. The value returned from this function will be the value of the property when it's added to the JSON string. If the value is `undefined`, this property is excluded from the JSON string.

</p>
</li>

<li><h3>What is the output</h3>

```js
const shape = {
  radius: 10,
  diameter() {
    return this.radius * 2;
  },
  perimeter: () => 2 * Math.PI * this.radius,
};

console.log(shape.diameter());
console.log(shape.perimeter());
```

<h4>Answer: 20 and NaN</h4>
<p>Note that the value of `diameter` is a regular function, whereas the value of `perimeter` is an arrow function.

With arrow functions, the `this` keyword refers to its current surrounding scope, unlike regular functions! This means that when we call `perimeter`, it doesn't refer to the shape object, but to its surrounding scope (window for example).

There is no value `radius` on that object, which returns `NaN`.</p>

</li>
<li><h3>How to Destructure and Rename the property</h3>
<h4>Answer: </h4>

```js
let user = { name: "Rahul", age: 24 };

// Destructuring
const { name } = user;

console.log(name); // Rahul

// Renaming
const { name: myName } = { name: "Lydia" };

console.log(name); //undefined
```

<P>When we unpack the property `name` from the object on the right-hand side, we assign its value `"Lydia"` to a variable with the name `myName`.

With `{ name: myName }`, we tell JavaScript that we want to create a new variable called `myName` with the value of the `name` property on the right-hand side.

Since we try to log `name`, a variable that is not defined, `undefined` is returned on the left side assignment. Later, the value of `Lydia` is stored through the destructuring assignment

</P>
</li>
<li><h3>What's the output?</h3>

```js
function getItems(fruitList, ...args, favoriteFruit) {
    return [...fruitList, ...args, favoriteFruit]
    }

getItems(["banana", "apple"], "pear", "orange")
```

<h4>Answer: SyntaxError</h4>
<P>...args is a rest parameter. In this example, the rest parameter was the second parameter. This is not possible, and will throw a syntax error.
</P>

</li>
<li><h3>How will u make the above code snippet work?</h3>
<h4>Answer: </h4>
<p>The rest parameter's value is an array containing all remaining arguments, and can only be the last parameter! 
</p>

```js
function getItems(fruitList, favoriteFruit, ...args) {
  return [...fruitList, ...args, favoriteFruit];
}

getItems(["banana", "apple"], "pear", "orange");
```

Returns `['banana', 'apple', 'orange', 'pear']`

</li>

<h2>Referencing</h2>
<li><h3>What's the output of the following code snippet?</h3>

```js
let c = { greeting: "Hey!" };
let d;

d = c;
c.greeting = "Hello";
console.log(d.greeting);
```

<h4>Answer: Hello</h4>
<p>In JavaScript, all objects interact by reference when setting them equal to each other. When you change one object, you change all of them.</p>

</li>
<li><h3>What is the output of the following code snippet?</h3>

```js
console.log({ a: 1 } == { a: 1 });
console.log({ a: 1 } === { a: 1 });
```

<h4>Answer: false false</h4>
<p>In JavaScript, Objects are compared based on references.

In the above statement, we are comparing two different objects so their references will be different. Hence, we get the output as false for both of the statements.

</p>
</li>
<li><h3> What's the output of the following code snippet? ( Referencing is not always there )</h3>

```js
let person = { name: "Lydia" };
const members = [person];
person = null;

console.log(members);
```

<h4>Answer: </h4>

```js
[{ name: "Lydia" }];
```

<p>First, we declare a variable person with the value of an object that has a name property.

Then, we declare a variable called members. We set the first element of that array equal to the value of the person variable. Objects interact by reference when setting them equal to each other. When you assign a reference from one variable to another, you make a copy of that reference. (note that they don't have the same reference!)

Then, we set the variable person equal to null.

We are only modifying the value of the person variable, and not the first element in the array, since that element has a different (copied) reference to the object. The first element in members still holds its reference to the original object. When we log the members array, the first element still holds the value of the object, which gets logged.</p>

</li>
<li><h3>What's the output of the following code snippet?</h3>

```js
const value = { number: 10 };

const multiply = (x = { ...value }) => {
  console.log((x.number *= 2));
};

multiply();
multiply();
multiply(value);
multiply(value);
```

<h4>Answer: 20, 20, 20, 40</h4>
<p>In ES6, we can initialize parameters with a default value. The value of the parameter will be the default value, if no other value has been passed to the function, or if the value of the parameter is "undefined". In this case, we spread the properties of the value object into a new object, so x has the default value of { number: 10 }.

The default argument is evaluated at call time! Every time we call the function, a new object is created. We invoke the multiply function the first two times without passing a value: x has the default value of { number: 10 }. We then log the multiplied value of that number, which is 20.

The third time we invoke multiply, we do pass an argument: the object called value. The _= operator is actually shorthand for x.number = x.number _ 2: we modify the value of x.number, and log the multiplied value 20.

The fourth time, we pass the value object again. x.number was previously modified to 20, so x.number \*= 2logs 40.</p>

</li>
<li><h3>What is the output of the following code snippet?</h3>

```js
function changeAgeAndReference(person) {
  person.age = 25;
  person = {
    name: "John",
    age: 50,
  };

  return person;
}

const personObj1 = {
  name: "Alex",
  age: 30,
};

const personObj2 = changeAgeAndReference(personObj1);

console.log(personObj1); // -> ?
console.log(personObj2); // -> ?
```

<h4>Answer: </h4>

```js
{ name: 'Alex', age: 25 }
{ name: 'John', age: 50 }
```

<p>The function first changes the property age on the original object it was passed in. It then reassigns the variable to a brand new object and returns that object. Here’s what the two objects are logged out.</p>

</li>
<li><h3>Difference between shallow copy vs deep copy</h3>
<h4>Answer: </h4>
<h4>Shallow copy</h4>
<p>A shallow copy means that certain (sub-)values are still connected to the original variable.</p>

```js
const user = {
  name: "Jen",
  age: 26,
};

const copyOfUser = user;
console.log(user, "user"); //{ name: 'Jen', age: 26 } user

console.log("------------After Modification-----------");
copyOfUser.age = 24;
/*
Here you would expect user object wouldn't change, but copyOfUser
and user object both share same memory address
*/
console.log(user, "user");
// ------------After Modification-----------
// { name: 'Jen', age: 24 } user
```

<h4>Deep copy</h4>
<p>A deep copy means that all of the values of the new variable are copied and disconnected from the original variable</p>

```js
const user = {
  name: "Jen",
  age: 26,
};
console.log("=========Deep Copy========");
const copyOfUser = JSON.parse(JSON.stringify(user));
console.log("User=> ", user);
console.log("copyOfUser=> ", copyOfUser);
/*
=========Deep Copy========
User=>  { name: 'Jen', age: 26 }
copyOfUser=>  { name: 'Jen', age: 26 }
*/
console.log("---------After modification---------");
copyOfUser.name = "Rahul";
copyOfUser.age = 24;
/*
Here user object will not change
*/
console.log("User=> ", user);
console.log("copyOfUser=> ", copyOfUser);
/*
---------After modification---------
user=>  { name: 'Jen', age: 26 }
copyOfUser=>  { name: 'Rahul', age: 24 }
*/
```

</li>
<li><h3>How to clone an object without referencing its keys to original object?</h3>
<h4>Answer: There are 3 ways to clone an object</h4>

```js
const obj = { a: 1, b: 2 };
const objclone = Object.assign({}, obj);
const objclone = JSON.parse(JSON.stringify(employee));
const objclone = { ...obj };
```

</li>
</ol>
