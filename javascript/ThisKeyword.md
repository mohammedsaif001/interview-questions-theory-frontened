<div align="center"><h1>'this' Keyword</h1></div>
The value of this is determined by how a function is called (runtime binding). So, there are two types of binding when it comes to object binding in JS, one is implicit and other is explicit.

## Implicit Binding

Implicit Binding is applied when you invoke a function in an Object using the dot notation. this in such scenarios will point to the object using which the function was invoked. Or simply the object on the left side of the dot.

## Explicit Binding

In Explicit Binding, you can force a function to use a certain object as its this. Explicit Binding can be applied using call(), apply(), and bind().
<br/>
<br/>

# What is 'this' keyword in javascript?

<ul>
<li>In javascript, the 'this' keyword refers to an object</li>
<li>Which object depends on how this is being invoked(used or called)</li>
<li>The 'this' keyword refers to different objects dependung on how it is used</li>
</ul>

<ol>
<li>In an object method, this refers to the object</li>
<li>Alone, 'yhis' refers to the global object</li>
<li>In a function, this refers to the global object</li>
<li>In a function in strict mode, 'this' is undefined</li>
<li>In an event, this refers to the element that recieved the event</li>
<li>Methods like call(),bind(),apply() can refer 'this' to any object</li>
</ol>

### Global

```js
let a = 5;
console.log(this); // window obj
console.log(this.a); // undefined
```

### 'this' inside a Function

Generally it targets the window object
<br/>
Inside a function, this points to the owner of the function call, I repeat, THE FUNCTION CALL, and NOT the function itself. The same function can have different owners in different scenarios.

```js
function myFunction() {
  console.log(this);
}
myFunction(); // window object
```

### Method inside an object

```js
let user = {
  name: "Mohammed",
  age: 24,
  getDetails() {
    console.log(this.name); //Mohammed
  },
};
```

<h4>What happens when we have functions inside a nested object key?</h4>

```js
let user = {
  name: "Mohammed",
  age: 24,
  childObj: {
    newName: "Roadside Coder",
    getDetails() {
      console.log(this.newName, "and", this.name);
    },
  },
};

user.childObj.getDetails(); // Roadside Coder and undefined
```

### 'this' inside an arrow function

It takes it's this from the outer “normal” function

```js
const myFun = () => {
  console.log(this);
};
myFun(); // window object
```

<h4>What if arrow functions are inside the object?</h4>

```js
let user = {
  name: "Mohammed",
  age: 24,
  getDetails: () => {
    console.log(this.name);
    // undefined because arrow functions points to the window object unless it's the child of a normal function
  },
};
```

```js
let user = {
  name: "Mohammed",
  age: 24,
  getDetails() {
    const nestedArrow = () => console.log(this.name); //Mohammed
    nestedArrow();
  },
};

//  gives "Mohammed" as the output since it points to the parent's context i.e. the user object.
```

### Class / Constructor

'this' inside a constructor will point to everything inside of a constructor

```js
class user {
  constructor(n) {
    this.name = n;
  }
  getName() {
    console.log(this.name);
  }
}

const User = new user("Mohammed"); // => This will generate a user object from the above class
User.getName();
```

# Interview Questions

<ol>
<li><h3>Give the output of the following snippet.</h3>

```js
const user = {
  firstName: "Mohammed!",
  getName() {
    const firstName = "Jen!";
    return this.firstName;
  },
};
console.log(user.getName()); // What is logged?
```

<h4>Answer: </h4><p>Mohammed! is logged to the console. user.getName() is a method invocation, that's why this inside the method equals object.
<br/>
There's also a variable declaration const firstName = 'Jen!' inside the method. The variable doesn't influence anyhow the value of this.firstName.</p>
</li>

<li><h3>What is the result of accessing its ref? Why?</h3>

```js
function makeUser() {
  return {
    name: "John",
    ref: this,
  };
}

let user = makeUser();

alert(user.ref.name); // What's the result?
```

<h4>Answer: An Error</h4>
<p>That’s because rules that set 'this' do not look at object definition. Only the moment of call matters.

Here the value of this inside makeUser() is undefined, because it is called as a function, not as a method with “dot” syntax.

The value of this is one for the whole function, code blocks and object literals do not affect it.

So ref: this actually takes current this of the function.

We can rewrite the function and return the same this with undefined value:</p>

</li>

<li><h3>How do u make the above question work?</h3>

```js
function makeUser() {
  return {
    name: "Mohammed Saif",
    ref() {
      return this;
    },
  };
}

let user = makeUser();

alert(user.ref().name); // Mohammed Saif
```

You make ref a method and then there will be no error. You will get the output as Mohammed Saif.

 </li>

<li><h3>What logs to console the following code snippet?</h3>

```js
const user = {
  name: "Mohammed Saif!",
  logMessage() {
    console.log(this.name); // What is logged?
  },
};
setTimeout(user.logMessage, 1000);
```

<h4>Answer: </h4>
<p>After a delay of 1 second, `undefined` is logged to console.

While `setTimeout()` function uses the `object.logMessage` as a callback, still, it invokes `object.logMessage` as a regular function, rather than a method.

And during a regular function invocation _this_ equals the global object which is `window` in the case of the browser environment.

That's why `console.log(this.message)` inside `logMessage` method logs `window.message`, which is `undefined`.

</p>
</li>

<li><h3>How can you fix the above code so that 'Mohammed Saif!' is logged to console?</h3>
<h4>Answer: Enclose the callback with a normal function </h4>

```js
const user = {
  name: "Mohammed Saif!",
  logMessage() {
    console.log(this.name); // What is logged?
  },
};
setTimeout(function () {
  user.logMessage();
}, 1000);
```

 </li>

 <li><h3>What logs to console of the following code snippet?</h3>
 
 ```js
 const user = { 
    name: 'Mohammed',
     greet() { 
         return Hello, ${this.name}!; 
    }, 
    farewell: () => { 
        return Goodbye, ${this.name}!; 
        } 
};
    console.log(user.greet()); // What is logged? 
    console.log(user.farewell()); // What is logged?
 ```

 <h4>Answer: </h4>
 <p>'Hello, Mohammed!' and 'Goodbye, undefined!' are logged to console.

When calling `object.greet()`, inside the method `greet()` `this` value equals `object` because `greet` is a regular function. Thus `object.greet()` returns `'Hello,Mohammed!'`.

But `farewell()` is an arrow function, so _[this_ value inside of an arrow function] always\_ equals `this` of the outer scope.

The outer scope of `farewell()` is the global scope, where `this` is the global object. Thus `object.farewell()` actually returns `'Goodbye, ${window.name}!'`, which evaluates to `'Goodbye, undefined!'`.

</p>
 </li>

<li><h3>Create an object `calculator` with three methods:</h3>
<h4>
- `read()` prompts for two values and saves them as object properties with names `a` and `b` respectively.<br/>
- `sum()` returns the sum of saved values.<br/>
- `mul()` multiplies saved values and returns the result.
</h4>
<h4>Answer: </h4>

```js
let calculator = {
  sum() {
    return this.a + this.b;
  },

  mul() {
    return this.a * this.b;
  },

  read() {
    this.a = +prompt("a?", 0);
    this.b = +prompt("b?", 0);
  },
};

calculator.read();
alert(calculator.sum());
alert(calculator.mul());
```

</li>

<li><h3>Give output of the following code snippet.</h3>

```js
var length = 4;

function callback() {
  console.log(this.length); // What is logged?
}

const object = {
  length: 5,
  method(callback) {
    callback();
  },
};

object.method(callback, 1, 2);
```

<h4>Answer: </h4>
<p>`4` is logged to console.

`callback()` is called using regular function invocation inside `method()`. Since this value during a regular function invocation equals the global object, `this.length` is evaluated as `window.length` inside `callback()` function.

The first statement `var length = 4`, being in the outermost scope, creates a property `length` on the global object: `window.length` becomes `4`.

Finally, inside the `callback()` function `this.length` evaluates as `window.length` — `4` being logged to console.

</p>
</li>

<li><h3>What is the output of the following code snippet?</h3>

```js
var length = 4;
function callback() {
  console.log(this.length); // What is logged?
}

const object = {
  length: 5,
  method() {
    arguments[0]();
  },
};

object.method(callback, 1, 2);
```

<h4>Answer: </h4>
<p>`3` is logged to console.

`obj.method(callback, 1, 2)` is invoked with 3 arguments: `callback`, `1` and `2`. As result the `arguments` special variable inside `method()` is an array-like object of the following structure:
{ 0: callback, 1: 1, 2: 2, length: 3 }

Because `arguments[0]()` is a method invocation of `callback` on `arguments` object, `this` inside the `callback` equals `arguments`. As result `this.length` inside `callback()` is same as `arguments.length` — which is `3`.

</p>
</li>

<li><h3>Write the implementation of this calc()</h3>

```js
const result = calc.add(10).multiply(5).subtract(30).add(10);
console.log(result.total); //What is logged
```

<h4>Answer: </h4>

```js
var calc = {
  total: 0,
  add(a) {
    this.total += a;
    return this;
  },
  subtract(a) {
    this.total -= a;
    return this;
  },
  multiply(a) {
    this.total *= a;
    return this;
  },
};
```

</li>

</ol>
