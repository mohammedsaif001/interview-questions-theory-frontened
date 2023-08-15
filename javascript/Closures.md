<div align="center"><h1>Closures</h1></div>

<h3>Closure is a combination of functions bundled together with it's lexical environment. It is a function that references variables in the outer scope from it's inner scope</h3>

<h4>A closure is a function that has access to its outer function scope even after the function has returned. Meaning, A closure can remember and access variables and arguments reference of its outer function even after the function has returned.</h4>

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
<li><h3> Will the below code still forms a closure?</h3>

```js
function outer() {
  function inner() {
    console.log(a);
  }
  var a = 10;
  return inner;
}
outer()(); // 10
```

<h4>Answer: </h4>Yes, because inner function forms a closure with its outer environment so sequence doesn't matter.
</li>

<li><h3>Changing var to let, will it make any difference?</h3>

```js
function outer() {
  let a = 10;
  function inner() {
    console.log(a);
  }
  return inner;
}
outer()(); // 10
```

<h4>Answer: </h4>It will still behave the same way
</li>
<li><h3>Will inner function have the access to outer function argument?</h3>

```js
function outer(str) {
  let a = 10;
  function inner() {
    console.log(a, str);
  }
  return inner;
}
outer("Hello There")(); // 10 "Hello There"
```

<h4>Answer: </h4>Inner function will now form closure and will have access to both a and str.
</li>
<li><h3> In below code, will inner form closure with outest?</h3>

```js
function outest() {
  var c = 20;
  function outer(str) {
    let a = 10;
    function inner() {
      console.log(a, c, str);
    }
    return inner;
  }
  return outer;
}
outest()("Hello There")(); // 10 20 "Hello There"
```

<h4>Answer: </h4>Yes, inner will have access to all its outer environment.
</li>

<li><h3>What will be the output of the following code with explanaion.</h3>

```js
function outest() {
  var c = 20;
  function outer(str) {
    let a = 10;
    function inner() {
      console.log(a, c, str);
    }
    return inner;
  }
  return outer;
}
let a = 100;
outest()("Hello There")(); // 10 20 "Hello There"
```

<h4>Answer:</h4>Still the same output, the inner function will have reference to inner a, so conflicting name won't matter here. If it wouldn't have find a inside outer function then it would have went more outer to find a and thus have printed 100. So, it try to resolve variable in scope chain and if a wouldn't have been found it would have given reference error.
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

<li><h3>What will be the output?</h3>

```js
function x() {
  var i = 1;
  setTimeout(function () {
    console.log(i);
  }, 3000);
  console.log("Javascript");
}
x();
// Output:
// Javascript
// 1 // after waiting 3 seconds
```

<ul>
<li>We expect JS to wait 3 sec, print 1 and then go down and print the string. But JS prints string immediately, waits 3 sec and then prints 1.</li>
<li>The function inside setTimeout forms a closure (remembers reference to i). So wherever function goes it carries this ref along with it.</li>
<li>setTimeout takes this callback function & attaches timer of 3000ms and stores it. Goes to next line without waiting and prints string.</li>
<li>After 3000ms runs out, JS takes function, puts it into call stack and runs it.</li>
</ul>
</li>

<li><h3>Print 1 after 1 sec, 2 after 2 sec till 5 : Tricky interview question
</h3>

```js
function x() {
  for (var i = 1; i <= 5; i++) {
    setTimeout(function () {
      console.log(i);
    }, i * 1000);
  }
  console.log("Javascript");
}
x();
// Output:
// Javascript
// 6
// 6
// 6
// 6
// 6
```

<ul>
<li>This happens because of closures. When setTimeout stores the function somewhere and attaches timer to it, the function remembers its reference to i, not value of i. All 5 copies of function point to same reference of i. JS stores these 5 functions, prints string and then comes back to the functions. By then the timer has run fully. And due to looping, the i value became 6. And when the callback fun runs the variable i = 6. So same 6 is printed in each log</li>
<li>This happens because of closures. When setTimeout stores the function somewhere and attaches timer to it, the function remembers its reference to i, not value of i. All 5 copies of function point to same reference of i. JS stores these 5 functions, prints string and then comes back to the functions. By then the timer has run fully. And due to looping, the i value became 6. And when the callback fun runs the variable i = 6. So same 6 is printed in each log</li>
</ul>

<h4>Printing 1,2,3,4,5 using let</h4>

```js
function x() {
  for (let i = 1; i <= 5; i++) {
    setTimeout(function () {
      console.log(i);
    }, i * 1000);
  }
  console.log("Javascript");
}
x();
// Output:
// Javascript
// 1
// 2
// 3
// 4
// 5
```

</li>

<li><h3>Print the same without let using var</h3>

```js
function x() {
  for (var i = 1; i <= 5; i++) {
    function close(i) {
      setTimeout(function () {
        console.log(i);
      }, i * 1000);
      // put the setT function inside new function close()
    }
    close(i); // everytime you call close(i) it creates new copy of i. Only this time, it is with var itself!
  }
  console.log("Namaste Javascript");
}
x();
```

</li>

<li><h3>Discuss more on Data hiding and encapsulation?</h3>

```js
// without closures
var count = 0;
function increment(){
  count++;
}
// in the above code, anyone can access count and change it.

------------------------------------------------------------------

// (with closures) -> put everything into a function
function counter() {
  var count = 0;
  function increment(){
    count++;
  }
}
console.log(count); // this will give referenceError as count can't be accessed. So now we are able to achieve hiding of data

------------------------------------------------------------------

//(increment with function using closure) true function
function counter() {
  var count = 0;
  return function increment(){
    count++;
    console.log(count);
  }
}
var counter1 = counter(); //counter function has closure with count var.
counter1(); // increments counter

var counter2 = counter();
counter2(); // here counter2 is whole new copy of counter function and it wont impack the output of counter1

*************************

// Above code is not good and scalable for say, when you plan to implement decrement counter at a later stage.
// To address this issue, we use *constructors*

// Adding decrement counter and refactoring code:
function Counter() {
//constructor function. Good coding would be to capitalize first letter of constructor function.
  var count = 0;
  this.incrementCounter = function() { //anonymous function
    count++;
    console.log(count);
  }
   this.decrementCounter = function() {
    count--;
    console.log(count);
  }
}

var counter1 = new Counter();  // new keyword for constructor fun
counter1.incrementCounter();
counter1.incrementCounter();
counter1.decrementCounter();
// returns 1 2 1
```

</li>
</ol>
