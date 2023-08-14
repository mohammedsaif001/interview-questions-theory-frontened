<div align="center">
<h1>Debouncing & Throttling</h1>
</div>
Debouncing and throttling are both techniques used to enhance performance optimization. These two functions are higher-order functions that take a callback function as input and return a new function, introducing a specified delay.

## Debouncing

The debouncing function is invoked when the interval between two keystroke events matches the provided delay. In other words, it ensures that the callback is executed only after a pause in the user's input, effectively reducing the number of invocations and conserving resources.

For example, when searching by typing "bangalore," instead of making API calls for each letter typed (b, a, n, g), the function is triggered only once after I've stopped interacting (typing "bangalore"), with a delay of say around 400ms.

```html
<div class="container">
  <div>
    <input type="text" placeholder="search" id="inputSearch" />
    <!-- Input Search Devounce -->
    <div id="text"></div>
    <div id="triggered"></div>
    <div id="debounce_triggered"></div>
  </div>
  <!-- Button Pressed Debounc -->
  <div>
    <button class="buttonClicked" onclick="btnClickedFunction()">
      Click Me
    </button>
    <div id="btn_clicked"></div>
    <div id="btn_clicked_debounced"></div>
  </div>
</div>
```

```js
// Debouncing Function
const myDebouncing = (cb, delay) => {
  let timer;
  return function (...args) {
    if (timer) clearTimeout(timer);
    timer = setTimeout(() => {
      cb(...args);
    }, delay);
  };
};
```

```js
// Button Clicked
const btn_clicked = document.querySelector("#btn_clicked");
const btn_clicked_debounced = document.querySelector("#btn_clicked_debounced");
const btn = document.querySelector(".buttonClicked");

let btn_clicked_count = 0;
let btn_clicked_count_debounced = 0;

const debouncedFunctionCall = myDebouncing(() => {
  btn_clicked_count_debounced += 1;
  btn_clicked_debounced.innerHTML =
    "Debounced Function Clicked " + btn_clicked_count_debounced;
}, 800); // Adjust the debounce delay as needed

const btnClickedFunction = () => {
  btn_clicked.innerHTML = "Button Clicked " + ++btn_clicked_count;
  debouncedFunctionCall();
};
```

```js
const functionCall = myDebouncing((cb) => {
  cb();
}, 200);

// Input Search
const inputElement = document.getElementById("inputSearch");
const text = document.getElementById("text");
const triggered = document.getElementById("triggered");
const debounce_triggered = document.getElementById("debounce_triggered");

let debounced_count = 0;
let count = 0;

inputElement.addEventListener("keyup", (e) => {
  functionCall(() => {
    debounce_triggered.innerText = "Debounced Count " + ++debounced_count;
  });
  text.innerHTML = e.target.value;
  triggered.innerText = "Normal Count " + ++count;
  // console.log(e.target.value)
});
```

<br/>

## Throttling

Throttling is triggered when the time elapsed between the first invocation of the function and the subsequent call surpasses the given delay. This means the throttled function is executed at a controlled rate, preventing an excessive number of executions, often used for scenarios where continuous updates need to be limited such as window resizing, infine scrolling.

For Example: When typing "bangalore karnataka," it doesn't trigger the event after 400ms from the completion of typing; instead, it starts a timer when I press the first letter and then calls the function after 400ms, continuously calling it at those intervals as long as I'm interacting.

This approach is useful for scenarios like infinite scrolling for data fetching. If the time difference between the last function call and the current one is a certain duration (e.g., 400ms), it triggers the function, preventing rapid, continuous calls.

```html
<div>
  <button class="buttonClicked_throttle" onclick="btnClickedFunctionThrottle()">
    Click Me
  </button>
  <div id="btn_clicked_throttle_basic"></div>
  <div id="btn_clicked_throttle"></div>
</div>
```

```js
const myThrottle = (cb, delay) => {
  let flag = true;
  return function (...args) {
    if (flag) {
      cb(...args);
      flag = false;
      setTimeout(() => {
        flag = true;
      }, delay);
    }
  };
};
```

```js
const btn_clicked_throttle_basic = document.querySelector(
  "#btn_clicked_throttle_basic"
);
const btn_clicked_throttle = document.querySelector("#btn_clicked_throttle");
const btn_throttle = document.querySelector(".buttonClicked_throttle");

let btn_clicked_throttle_basic_count = 0;
let btn_clicked_count_throttle = 0;

const callingMyThrottling = myThrottle(() => {
  btn_clicked_throttle.innerHTML =
    "Throttling Clicked " + ++btn_clicked_count_throttle;
}, 800);

function btnClickedFunctionThrottle() {
  btn_clicked_throttle_basic.innerHTML =
    "Btn Clicked " + ++btn_clicked_throttle_basic_count;
  callingMyThrottling();
}
```
