<div align="center"><h1>Closures</h1></div>

<h3>Closure is a combination of functions bundled together with it's lexical environment. It is a function that references variables in the outer scope from it's inner scope</h3>

### What is Lexical Scope?

A Lexical scope in JavaScript means that a variable defined outside a function can be accessible inside another function defined after the variable declaration. But the opposite is not true; the variables defined inside a function will not be accessible outside that function.

```js
function foo() {
  var name = "Javascript"; // name is a local variable created by foo
  function displayName() {
    // displayName() is the inner function
    alert(name); // variable used which is declared in the parent function
  }
  displayName();
}
foo();
```

### Why do we use Closures?

Closures makes it possible for a function to have "private" variables. JavaScript closure is used to control what is and isn't in scope in a particular function, along with which variables are shared between sibling functions in the same containing scope.

```js
function makeFunc() {
  var name = "Javascript";
  function displayName() {
    alert(name);
  }
  return displayName;
}

var myFunc = makeFunc();
myFunc();
```

### Closure Scope chain

Closures have three scopes :

<ul>
<li>Local Scope (Own scope)</li>
<li>Outer Functions Scope</li>
<li>Global Scope</li>
</ul>
If an outer function is a nested function then the outer function's scope includes the enclosing scope of the outer function which creates a chain of function scopes.
<br/>
<br/>
<br/>

# Interview Questions

<ol>
<li><h3>What are the advantages of Closures?</h3>
<h4>Answer: </h4>
<ul>
<li>Module Design Pattern</li>
<li>Currying</li>
<li>Memoize</li>
<li>Data Hiding & Encapsulation</li>
<li>setTimeOut and much more...</li>
</ul>
</li>

<li><h3>What are the disadvantages of Closures?</h3>
<h4>Answer: </h4>
<ul>
<li>Over consumption of memory</li>
<li>Memory Leak</li>
<li>Freeze Browser</li>
</ul>
</li>

<li><h3>What is the difference between closure and scope?</h3>
<h4>Answer: </h4>
<p>When you declare a variable in a function, you can only access it in the function. These variables are said to be scoped to the function.If you define any inner function within another function, this inner function is called a closure. It retains access to the variables created in the outer function.

Whereas a scope in JavaScript defines what variables you have access to.</p>

</li>

<li><h3>What will be the output for the following code snippet?</h3>

```js
let count = 0;
(function immediate() {
  if (count === 0) {
    let count = 1;
    console.log(count); // Output ?
  }
  console.log(count); // Output?
})();
```

<h4>Answer: </h4>
<p>1 and 0 is logged to the console.

The first statement let count = 0 declares a variable count.

immediate() is a closure that captures the count variable from the outer scope. Inside of the immediate() function scope count is 0.

However, inside the conditional, another let count = 1 declares a local variable count, which overwrites count from outer the scope. The first console.log(count)logs 1.

The second console.log(count) logs 0, since here count variable is accessed from the outer scope.</p>

</li>

<li><h3> Can you create a function named createBase to show the below functionality?</h3>

```js
var addSix = createBase(6);
addSix(10); // returns 16
addSix(21); // returns 27
```

<h4>Answer: </h4>
<p>You can create a closure to keep the value passed to the function createBase even after the inner function is returned. The inner function that is being returned is created within an outer function, making it a closure, and it has access to the variables within the outer function, in this case the variable baseNumber.</p>

```js
function createBase(baseNumber) {
  return function (N) {
    // we are referencing baseNumber here even though it was declared outside of this function. Closures allow us to do this in JavaScript
    return baseNumber + N;
  };
}

var addSix = createBase(6);
addSix(10);
addSix(21);
```

</li>

<li><h3>How do you optimise time using closures?</h3>

```js
function find(index) {
  let a = [];
  for (let i = 0; i < 1000000; i++) {
    a[i] = i * i;
  }

  console.log(a[index]);
}

console.time("6");
find(6); // this takes 37ms
console.timeEnd("6");
console.time("12");
find(12); // this takes 135ms
console.timeEnd("12");
```

<h4>Answer: </h4>

```js
function find() {
  let a = [];
  for (let i = 0; i < 1000000; i++) {
    a[i] = i * i;
  }

  return function (index) {
    console.log(a[index]);
  };
}

const closure = find();
console.time("6");
closure(6); // this takes 0.25 ms
console.timeEnd("6");
console.time("12");
closure(12); // this takes 0.025ms
console.timeEnd("12");
```

</li>

<li><h3>What will be the output for the following?</h3>

```js
for (var i = 0; i < 3; i++) {
  setTimeout(function log() {
    console.log(i); // What is logged?
  }, 1000);
}
```

<h4>Answer: 333 </h4>
</li>

<li><h3>How would you use a closure to create a private counter?</h3>
<h4>Answer: </h4>
<p>You can create a function within an outer function (a closure) that allows you to update a private variable but the variable wouldn't be accessible from outside the function without the use of a helper function.</p>

```js
function counter() {
  var _counter = 0;
  // return an object with several functions that allow you
  // to modify the private _counter variable
  return {
    add: function (increment) {
      _counter += increment;
    },
    retrieve: function () {
      return "The counter is currently at: " + _counter;
    },
  };
}

// error if we try to access the private variable like below// _counter;// usage of our counter function
var c = counter();
c.add(5);
c.add(9);

// now we can access the private variable in the following way
c.retrieve(); // => The counter is currently at: 14
```

</li>
<li><h3>Rewrite the function in such a way the output gets printed once even though the function is called multiple times.</h3>

```js
let view;
function likeTheVideo() {
  view = "Javascript";
  console.log("Subscribe to", view);
}

likeTheVideo(); // Subscribe to Javascript
likeTheVideo(); // Subscribe to Javascript
likeTheVideo(); // Subscribe to Javascript
likeTheVideo(); // Subscribe to Javascript
```

<h4>Answer: </h4>

```js
let view;
function likeTheVideo() {
  let called = 0;

  return function () {
    if (called > 0) {
      console.log("Already Subscribed");
    } else {
      view = "Javascript";
      called++;
      console.log("Subscribe to", view);
    }
  };
}

let isSubscribe = likeTheVideo();

isSubscribe(); // Subscribe to Javascript
isSubscribe(); // Already Subscribed
```

</li>
<li><h3> Write the polyfill for "_.memoize" method in lodash. </h3>

```js
function memoize(func) {
  let res = {};

  return function (...args) {
    const argsIndex = JSON.stringify(args);
    if (!res[argsIndex]) res[argsIndex] = func(...args);
    return res[argsIndex];
  };
}

const clumsysquare = memoize((num) => {
  for (let i = 1; i <= 100000000; i++) {}

  return num * 2;
});

console.time("First call");
console.log(clumsysquare(9467));
console.timeEnd("First call");

// use the same value two times
console.time("Second call");
console.log(clumsysquare(9467));
console.timeEnd("Second call");
```

</li>

</ol>
