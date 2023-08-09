<div align="center"><h1>Currying</h1></div>

<h3>Currying is a function that takes one argument at a time and returns a new function expecting the next argument. It is a conversion of functions from callable as f(a,b,c)into callable as f(a)(b)(c).</h3>

Basically Currying doesn’t call a function. It just transforms a function. They are constructed by chaining closures by immediately returning their inner functions simultaneously.

### Convert f(a, b) into f(a)(b).

```js
/*f(a,b) implementation */
function f(a, b) {
  return "Works";
}

/*f(a)(b) implementation */
function f(a) {
  return (b) => {
    "Works";
  };
}
console.log(f(1)(2)); // works
console.log(f(1)); /* (b) => {return "Works" } */
```

## Why should currying be used?

<ol>
<li> It makes a function pure which makes it expose to less errors and side effects.</li>
<li>It helps in avoiding the same variable again and again.</li>
<li> It is a checking method that checks if you have all the things before you proceed.</li>
<li> It divides one function into multiple functions so that one handles one set of responsibility.</li>
</ol>

## How does currying work?

Currying is a function that takes multiple arguments as input. It transform the function into a number of functions where every function will accept one argument.

```js
/*Simple function*/
const add = (a, b, c) => {
  return a + b + c;
};
console.log(add(1, 2, 3)); // 6

/* Curried Function */
const addCurry = (a) => {
  // takes one argument
  return (b) => {
    //takes second argument
    return (c) => {
      //takes third argument
      return a + b + c;
    };
  };
};
console.log(addCurry(1)(2)(3)); //6
```

<br/>
<br/>

# Interview Questions

<ol>
<li><h3>Convert sum(2,6,1) to sum(2)(6)(1)</h3>
<h4>Answer: </h4>

```js
function sum(a) {
    return (b) => {
        return (c) => {
            return a + b + c
        }
    }
}
/* you can call it in two ways*/
1️⃣ console.log(sum(1)(2)(3)); //6

2️⃣ const sum1 = sum(1);  //Returns 2nd function expecting the argument b
const sum2 = sum1(2);
const result = sum2(3);
console.log(result); // 6

```

</li>
<li><h3>Evaluate(”sum”)(2)(4) ⇒ 2+4 = 6 on basis of input given to first param.
</h3>
<h4>Answer: </h4>

```js
function sum(operation) {
  return (a) => {
    return (b) => {
      if (operation === "sum") return a + b;
      else if (operation === "multiply") return a * b;
      else if (operation === "divide") return a / b;
      else if (operation === "subtract") return a - b;
      else return "No / Invalid Operation Selected";
    };
  };
}
```

</li>
<li><h3>Write a currying function that takes infinite arguments.</h3>

```js
/*Straightforward and time-taking solution*/
const sum = function(a) {
    return function(b) {
        return function(c) {
            return function(d) {
                ...
                ...
                ...
                return a + b + c + d + ... n;
            }
        }
    }
}
```

<h4>Answer: </h4>

```js
//recursive solution
const sum = function (a) {
  return function (b) {
    if (b) {
      return sum(a + b);
    } else {
      return a;
    }
  };
};
```

</li>
<li><h3>Write the above Infinite Currying in one line</h3>
<h4>Answer: </h4>

```js
const sum = (a) => (b) => b ? sum(a + b) : a;
```

</li>
<li><h3>Currying vs Partial application</h3>
<h4>Answer: </h4>

```js
// Normal Currying Function
function sum(a) {
  return (b) => {
    return (c) => {
      return a * b * c;
    };
  };
}
const result = sum(2)(3)(4); // Result: 24
```

```js
// Partial Application
function sum(a) {
  return (b, c) => {
    return a * b * c;
  };
}

let x = sum(10);
x(1, 2);
x(20, 30);
x(40, 50);
// OR
sum(10)(1, 2);
sum(10)(20, 30);
sum(10)(40, 50);
```

<h4>
<ul>
<li>Currying transforms a function into a sequence of functions, each taking one argument.</li>
<li>Partial Application fixes a certain number of arguments in a function, generating a new function that takes the remaining arguments.</li>
</ul>
</h4>
</li>

<li><h3>How can we manipulate DOM using currying?</h3>

```js
<div>
  <h1 id="header">Hello Mohammed</h1>
</div>
```

<h3>I want browser to show "Hello Saif" instead of "Hello Mohammed".</h3>
<h4>Answer: </h4>
<ol>
<li>Take the id of the element as one argument and the content inside the element as another argument.

```js
const updateElemText = (id) => (content) =>
  (document.querySelector(`#${id}`).textContent = content);
```

</li>
<li>Now call the function with element id and and the content

```js
const updateHeaderText = updateElemText("header");
updateHeaderText("Hello RoadsideCoder!");
```

</li>
</ol>

</li>

</ol>
