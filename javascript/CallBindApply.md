<div align="center">
<h1>Call, Bind & Apply</h1>
</div>

<h3>Call, bind and Apply are three super important JavaScript methods that are available to all JavaScript functions, which are used to set the this keyword independent of how the function is called. You can use these methods to tie a function into an object and call the function as if it belonged to that object</h3>

So let's go and have a deep dive into explicit object binding in javascript i.e., Call, Bind and Apply methods and discuss some of the most commonly asked interview questions on it!

We will take a code snippet and solve it using call(), bind() and apply() and know how it is used to set this.

```js
var obj = { name: "Saif" };
function sayHello() {
  return "Hello " + this.name;
}

console.log(sayHello());

// Output: Hello
```

call(), apply() and bind() methods belong to the Function.prototype property.

## call()

The call() method calls the function with a given this value and arguments provided individually.

```js
function sayHello() {
  return "Hello " + this.name;
}

var obj = { name: "Saif" };

sayHello.call(obj); //Hello Saif
```

Here we are passing the obj to the call() and then this points to "obj" object.

## apply()

The apply() method calls the specified function with a given this value, and arguments provided as an array (or an array-like object).

```js
function sayHello(day, status) {
  return "Hello " + this.name + " today is " + day + " and feel " + status;
}

var obj = { name: "Saif" };

sayHello.apply(obj, ["tuesday", "good"]); // 'Hello Saif today is tuesday'
```

If the same is to be done with call() it would be like

```js
function sayHello(day, status) {
  console.log(
    "Hello " + this.name + " today is " + day + " and feel " + status
  );
}

var obj = { name: "Saif" };

sayHello.call(obj, "tuesday", "good"); // 'Hello Saif today is tuesday and feel good'
```

**Note: The only difference between call and apply is while passing the argument where in call() we pass it as individual args and whereas in apply() we pass it as an array of arguments**

Here we are passing the arguments as an array.As we can the the length of the arguments array should be equal to the no. of arguments to be passed to the function.

apply() is almost identical to call() except for the fact call() accepts an argument list, while apply() accepts a single array of arguments — for example, func.apply(this, ['eat', 'bananas']) vs. func.call(this, 'eat', 'bananas').

## bind()

The bind() method creates a new function that, when called, has its this keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called.

```js
function sayHello() {
  return "Hello " + this.name;
}

var obj = { name: "Saif" };

const helloFn = sayHello.bind(obj);

console.log(helloFn());
```

helloFn has the binded method and when we call helloFn it gives us the value of "this".

**The difference bwtween call() and bind() is that when we pass this with call it will be called then & there itself whereas in bind() a function is returned which can be invoked later**

# Interview Questions

<ol>

<li>

```js
const person = { name: "sAIF" };

function sayHi(age) {
  return `${this.name} is ${age} years`;
}

console.log(sayHi.call(person, 34));
console.log(sayHi.bind(person, 44));

// Output
// It will give "sAIF is 34 years"
// It will return the function "sayHi"
```

</li>

<li>

```js
const age = 10;
var person = {
  name: "Saif",
  age: 20,
  getAge: function () {
    return this.age;
  },
};

var person2 = { age: 24 };

person.getAge(); //20
person.getAge.call(person2); //24
person.getAge.apply(person2); //24
person.getAge.bind(person2)(); //24
```

</li>

<li>

```js
var status = "😎";

setTimeout(() => {
  const status = "😍";

  const data = {
    status: "🥑",
    getStatus() {
      return this.status;
    },
  };

  console.log(data.getStatus());
  console.log(data.getStatus.call(this));
}, 0);
```

<ol>
<li>
🥑
</li>
<li>
😎
</li>
</ol>

**Explanation:** <p>In a method, like the getStatus method, the this keyword refers to the object that the method belongs to. The method belongs to the data object, so this refers to the data object. When we log this.status, the status property on the data object gets logged, which is "🥑"

With the call method, we can change the object to which the this keyword refers.

In functions, the this keyword refers to the the object that the function belongs to.

We declared the setTimeout function on the global object, so within the setTimeout function, the this keyword refers to the global object. On the global object, there is a variable called status with the value of "😎". When logging this.status, "😎" gets logged.</p>

</li>
<br/>
<li>

**Write printAnimals() in such a way that it prints all animals in object below.**

```js
const animals = [
  { species: "Lion", name: "King" },
  { species: "Whale", name: "Queen" },
];

function printAnimals(i) {
  this.print = function () {
    console.log("#" + i + " " + this.species + ": " + this.name);
  };
  this.print();
}
```

**Explanation**

<p>Let's try to call the function using call method</p>

```js
printAnimals.call(animals); // #undefined undefined: undefined
```

<p>It gives output of undefined. Why? Well call demands object to be the parameter not array of objects like animals.

Approach will be run a for loop iterate through array of objects and call it on every object.</p>

```js
for (let i = 0; i < animals.length; i++) {
  printAnimals.call(animals[i], i);  #0 Lion: King #1 Whale: Queen
}
```

</li>

<br/>

<li>

**How to append an array to another array.**

```js
const array = ["a", "b"];
const elements = [0, 1, 2];
array.push(elements);
//Output: ['a', 'b',[0,1,2]]
```

To overcome this we use apply()

```js
const array = ["a", "b"];
const elements = [0, 1, 2];
array.push.apply(array, elements);

console.log(array); // OP: ['a','b',0,1,2]
```

After ES6 the same can be achieved using spread operator

```js
let array = ["a", "b"];
const elements = [0, 1, 2];
array = [...array, ...elements];
console.log(array);
```

</li>

<li>

**Find min/max in an array and use apply to enhance a built-in function.**

```js
const numbers = [5, 6, 2, 3, 7];

// using Math.min/Math.max apply

let max = Math.max.apply(null, numbers); // equal to Math.max

let min = Math.min.apply(null, numbers); // equal to Math.min

// vs. simple loop based algorithm

(max = -Infinity), (min = +Infinity);

for (let i = 0; i < numbers.length; i++) {
  if (numbers[i] > max) {
    max = numbers[i];
  }
  if (numbers[i] < min) {
    min = numbers[i];
  }
}
```

</li>

</ol>
