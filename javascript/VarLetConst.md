<div align="center"><h1>Var Let Const</h1></div>

## Scope

Scope is a certain section/region of the program where a defined variable has it's existence and beyond that it cannot be accessed.
<br/>
Three types of scope

<ol>
<li>Global Scope</li>
<li>Functional Scope</li>
<li>Block Scope</li>

</ol>

<h4>Note: var is functional scope, let and const is block scoped</h4>

```js
var a = 5; // global scope
```

```js
{
  var a = 5;
}
console.log(a); // 5 -- a is accessible outside  the block ✅
{
  let a = 5;
}
console.log(a); //  ReferenceError: a is not defined ❌
{
  const a = 5;
}
console.log(a); // ReferenceError: a is not defined ❌
```

<h3>How can we make it work?</h3>

```js
{
  let a = 5;
  console.log(a); //5
}
{
  const a = 5;
  console.log(a); //5
}
```

You see why let and const are block scoped because their scope is within a block meaning a block of statements.

## Variable shadowing

let and const are block scoped and from there we get the concept of shadowing.

```js
function test() {
  let a = "Hello";

  if (true) {
    let a = "Bye";
    console.log(a); // -- 1.❓
  }

  console.log(a); // -- 2 ❓
}

test();
```

Explanation:

```js
function test() {
  let a = "Hello";

  if (true) {
    let a = "Bye"; // New value assigned
    console.log(a); //Bye  a shadows the a defined outside the block scope and prints "Bye"
  }

  console.log(a); // 2.Hello  it will print a which is in the available scope
}

test();
```

<h3>While variable shadowing it shouldn't cross the boundary of the scope.</br></br>

It means we can shadow var using let but not the opposite because if we try to do so let using var we will go into illegal shadowing.

</h3>
Example:
 
```js
function func() {
    var a = 'Hello';
    let b = 'Roadside coder';

    if (true) {
        let a = 'Hi'; // Legal Shadowing
        var b = 'Bye'; // Illegal Shadowing
        console.log(a); // 1.Hi ✅
        console.log(b); // 2. SyntaxError: Identifier 'b' has already been declared ❌
    }

}
test();

````

## Declaration

```js
var a;
var a; ✅

let a;
let a;❌ SyntaxError: Identifier 'a' has already been declared

const a;
const a; ❌ SyntaxError: Missing initializer in const declaration

````

We can declare var as many times as we want in the same scope but we cannot declare let and const in the same scope multiple times.

```js
let a;
{
  let a;
}
```

## Declaration without initialization

```js
var a; ✅
let a; ✅
const a; ❌ SyntaxError: Missing initializer in const declaration -- you need to intialise a const while declaring it

```

## Re-initialization

```js
var a=5;
a=6; ✅

let a=7;
a=10; ✅

const a=10;
a=12; ❌ TypeError: Assignment to constant variable.

```

const gives an error since you can not reinitialize a const variable where as you can do it with a let and const variable.
