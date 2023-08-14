<div align="center">
<h1>Event Propagation</h1>
</div>

Event propagation refers to the way events (such as mouse clicks or keyboard inputs) are handled and passed through the elements in a web page's Document Object Model (DOM) hierarchy. There are two phases of event propagation: capturing phase and bubbling phase.

## Event Bubbling

Events start from the target element and move towards the root of the DOM in a bottom-up manner by default.

```html
<div class="outer_div">
  DIV
  <form>
    FORM
    <button>Click Here for Bubbling</button>
  </form>
</div>
```

```js
const div = document
  .querySelector("div")
  .addEventListener("click", function () {
    alert("Clicked on " + "div");
  });
const form = document
  .querySelector("form")
  .addEventListener("click", function () {
    alert("Clicked on " + "form");
  });
const button = document
  .querySelector("button")
  .addEventListener("click", function () {
    alert("Clicked on " + "button");
  });
```

The following Code will alert in the following manner

```js
Clicked on button
Clicked on form
Clicked on div
```

In this HTML and JavaScript example, we have a DOM structure consisting of an outer `<div>` element containing a `<form>` element, which in turn contains a `<button>` element.

By default, in the event propagation process:

<ol>
<li>When you click on the <b>button</b> element, the event starts at the target element (the button) and then bubbles up towards the root of the DOM. This means that first, the button's click event handler is triggered, displaying an alert indicating that the button was clicked.
</li>
<li>Next, the event continues to bubble up to the <b>form</b> element, and its click event handler is triggered, showing an alert indicating that the form was clicked.</li>
<li>Finally, the event continues to bubble up to the outermost <b>div</b> element, and its click event handler is triggered, displaying an alert indicating that the div was clicked.</li>
</ol>

## Event Capturing or Trickling

The default behaviour of Event Propagation is bottom-up approach but if you want to go top-down approach then add a 2nd parameter to the event listener as true or an object { capture:true }

```html
<div class="outer_div">
  DIV
  <form>
    FORM
    <button>Click Here for Bubbling</button>
  </form>
</div>
```

```js
const div = document.querySelector("div").addEventListener(
  "click",
  function () {
    alert("Clicked on " + "div");
  },
  { capture: true }
);
const form = document.querySelector("form").addEventListener(
  "click",
  function () {
    alert("Clicked on " + "form");
  },
  true
);
const button = document.querySelector("button").addEventListener(
  "click",
  function () {
    alert("Clicked on " + "button");
  },
  true
);
```

The following Code will alert in the following manner

```js
Clicked on div
Clicked on form
Clicked on button
```

## Stop Propagation

`stopPropagation()` method is used to prevent event propagation, specifically both the capturing phase (when events travel from the root to the target) and the bubbling phase (when events travel from the target to the root) of the DOM.

```js
const div = document
  .querySelector("div")
  .addEventListener("click", function (e) {
    e.stopPropagation();
    alert("Clicked on " + "div");
  });
const form = document
  .querySelector("form")
  .addEventListener("click", function (e) {
    e.stopPropagation();
    alert("Clicked on " + "form");
  });
const button = document
  .querySelector("button")
  .addEventListener("click", function (e) {
    e.stopPropagation();
    alert("Clicked on " + "button");
  });
```

Each event listener attached to the div, form, and button elements has the stopPropagation() method called within its respective function. This means that when any of these elements are clicked, the event will not continue to propagate further up the DOM hierarchy, preventing any parent elements from receiving the event.

## Target vs CurrentTarget

`target` and `currentTarget` are properties used in event propagation when dealing with DOM events

<ol>
<li>target: This property refers to the element that triggered the event. It's the element on which the event occurred, typically the one you clicked or interacted with.</li>
<li>currentTarget: This property refers to the element that has the currently executing event listener. It may be a parent of the target if event propagation (bubbling) is in progress, and you've attached the event listener to a higher-level element.</li>
</ol>

```html
<div class="outer_div">
  DIV
  <form>
    FORM
    <button>Click Here for <span class="event_prop"></span></button>
  </form>
</div>
```

```js
const div = document.querySelector("div").addEventListener("click", getTarget);
const form = document
  .querySelector("form")
  .addEventListener("click", getTarget);
const button = document
  .querySelector("button")
  .addEventListener("click", getTarget);

function getTarget(e) {
  e.preventDefault();
  curr_target = e.currentTarget.tagName;
  target_clicked = e.target.tagName;
  event_this = this.tagName;
}
```

For the above Code snippet this is what the output will be

<table>
<thead>
<tr>
<th>Clicked On</th>
<th>e.currentTarget</th>
<th>e.target</th>
<th>this</th>
</tr>
</thead>
<tbody>
<tr>
<td>DIV</td>
<td>div</td>
<td>div</td>
<td>div</td>
</tr>
<tr>
<td>FORM</td>
<td>div</td>
<td>form</td>
<td>div</td>
</tr>
<tr>
<td>BUTTON</td>
<td>div</td>
<td>button</td>
<td>div</td>
</tr>
</tbody>
</table>

PS: this keyword in here will work similar to that of currentTarget
<br/>
<br/>

## Event Delegation

Event delegation is attaching a single event listener to a higher-level element (usually a parent) that will handle events for multiple child elements. This approach is useful when you have many elements with similar behavior, like a list of items, and you want to avoid attaching individual event listeners to each item.

By using event delegation, you can reduce the number of event listeners and improve performance, especially when dealing with dynamic content or large lists. This technique takes advantage of event bubbling, where events triggered on child elements will "bubble up" to the parent element where the event listener is attached, allowing you to handle the events efficiently.

```html
<div class="event_delegation">
  <span class="event_delegation__span">react</span>
  <span class="event_delegation__span">nextjs</span>
  <span class="event_delegation__span">javascript</span>
</div>
```

```js
const event_delegation = document.querySelector(".event_delegation");

// Instead of adding event listeners to individual elements we can take advantage of bubbling and add event listener only to the parent element and do the computation
event_delegation.onclick = (e) => {
  alert(e.target.innerText);
};
```

<br/><br/>

# Creating a Modal using Event Delegation

```html
<body>
  <h1>Modal Website</h1>
  <button class="open_modal_button">Click to open Modal</button>

  <p class="long_content">Website Content Goes Here</p>

  <!-- Modal -->
  <div class="modal_outer">
    <div class="modal_inner">
      <h3>Inside Modal</h3>
      <p>Modal Content Here</p>
      <button class="close_modal_button">Close Modal</button>
    </div>
  </div>
  <script src="./modal.js"></script>
</body>
```

```css
.modal_inner {
  background-color: beige;
  position: absolute;
  padding: 2rem;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.modal_outer {
  background-color: rgba(252, 249, 249, 0.882);
  height: 100%;
  position: absolute;
  display: none;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

body > p {
  font-size: 17px;
}
```

```js
const body = document.querySelector("body");
const modal_inner = document.querySelector(".modal_inner");
const modal_outer = document.querySelector(".modal_outer");
const long_content = document.querySelector(".long_content");

const open_modal_button = document
  .querySelector(".open_modal_button")
  .addEventListener("click", () => toggleModal(true));

const close_modal_button = document
  .querySelector(".close_modal_button")
  .addEventListener("click", () => toggleModal(false));

// Function to open and close modal
function toggleModal(flag) {
  if (flag) {
    modal_outer.style.display = "block";
    body.style.overflowY = "hidden";
  } else {
    modal_outer.style.display = "none";
    body.style.overflowY = "auto";
  }
}

// Closing Modal on clicking negative space
modal_outer.addEventListener("click", function (e) {
  if (e.target.className.includes("modal_outer")) {
    toggleModal(false);
  }
});
```
