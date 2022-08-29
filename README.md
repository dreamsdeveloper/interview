# Interview Questions

<h2 align="center">
 JavaScript
</h2>

## Basic:

###  1. What are the possible ways to create objects in JavaScript?
There are many ways to create objects in javascript as below

1. **Object constructor:**

The simplest way to create an empty object is using the Object constructor. Currently this approach is not recommended.

```javascript
var object = new Object();
```

2. **Object's create method:**

The create method of Object creates a new object by passing the prototype object as a parameter

```javascript
var object = Object.create(null);
```

3. **Object literal syntax:**

The object literal syntax (or object initializer), is a comma-separated set of name-value pairs wrapped in curly braces.

```javascript
var object = {
  name: "Sudheer"
  age: 34
};

Object literal property values can be of any data type, including array, function, and nested object.
```

**Note:** This is an easiest way to create an object

4. **Function constructor:**

Create any function and apply the new operator to create object instances,

```javascript
function Person(name) {
  this.name = name;
  this.age = 21;
}
var object = new Person("Sudheer");
```

5. **Function constructor with prototype:**

This is similar to function constructor but it uses prototype for their properties and methods,

```javascript
function Person() {}
Person.prototype.name = "Sudheer";
var object = new Person();
```

This is equivalent to an instance created with an object create method with a function prototype and then call that function with an instance and parameters as arguments.

```javascript
function func() {};

new func(x, y, z);
```

**(OR)**

```javascript
// Create a new instance using function prototype.
var newInstance = Object.create(func.prototype)

// Call the function
var result = func.call(newInstance, x, y, z),

// If the result is a non-null object then use it otherwise just use the new instance.
console.log(result && typeof result === 'object' ? result : newInstance);
```

6. **ES6 Class syntax:**

ES6 introduces class feature to create the objects

```javascript
class Person {
  constructor(name) {
 this.name = name;
  }
}

var object = new Person("Sudheer");
```

7. **Singleton pattern:**

A Singleton is an object which can only be instantiated one time. Repeated calls to its constructor return the same instance and this way one can ensure that they don't accidentally create multiple instances.

```javascript
var object = new (function () {
  this.name = "Sudheer";
})();
```
### 2. What is the difference between Call, Apply and Bind?
 The difference between Call, Apply and Bind can be explained with below examples,

**Call:** The call() method invokes a function with a given `this` value and arguments provided one by one

```javascript
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(
 greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2
  );
}

invite.call(employee1, "Hello", "How are you?"); // Hello John Rodson, How are you?
invite.call(employee2, "Hello", "How are you?"); // Hello Jimmy Baily, How are you?
```

**Apply:** Invokes the function with a given `this` value and allows you to pass in arguments as an array

```javascript
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(
 greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2
  );
}

invite.apply(employee1, ["Hello", "How are you?"]); // Hello John Rodson, How are you?
invite.apply(employee2, ["Hello", "How are you?"]); // Hello Jimmy Baily, How are you?
```

**bind:** returns a new function, allowing you to pass any number of arguments

```javascript
var employee1 = { firstName: "John", lastName: "Rodson" };
var employee2 = { firstName: "Jimmy", lastName: "Baily" };

function invite(greeting1, greeting2) {
  console.log(
 greeting1 + " " + this.firstName + " " + this.lastName + ", " + greeting2
  );
}

var inviteEmployee1 = invite.bind(employee1);
var inviteEmployee2 = invite.bind(employee2);
inviteEmployee1("Hello", "How are you?"); // Hello John Rodson, How are you?
inviteEmployee2("Hello", "How are you?"); // Hello Jimmy Baily, How are you?
```

Call and apply are pretty interchangeable. Both execute the current function immediately. You need to decide whether it’s easier to send in an array or a comma separated list of arguments. You can remember by treating Call is for **comma** (separated list) and Apply is for **Array**.

Whereas Bind creates a new function that will have `this` set to the first parameter passed to bind().
### 3. What is the difference between slice and splice?
Some of the major difference in a tabular form

| Slice                                        | Splice                                          |
| -------------------------------------------- | ----------------------------------------------- |
| Doesn't modify the original array(immutable) | Modifies the original array(mutable)            |
| Returns the subset of original array         | Returns the deleted elements as array           |
| Used to pick the elements from array         | Used to insert or delete elements to/from array |

### 4.  What is the difference between == and === operators?
JavaScript provides both strict(===, !==) and type-converting(==, !=) equality comparison. The strict operators take type of variable in consideration, while non-strict operators make type correction/conversion based upon values of variables. The strict operators follow the below conditions for different types,

1. Two strings are strictly equal when they have the same sequence of characters, same length, and same characters in corresponding positions.
2. Two numbers are strictly equal when they are numerically equal. i.e, Having the same number value.
There are two special cases in this,
1. NaN is not equal to anything, including NaN.
2. Positive and negative zeros are equal to one another.
3. Two Boolean operands are strictly equal if both are true or both are false.
4. Two objects are strictly equal if they refer to the same Object.
5. Null and Undefined types are not equal with ===, but equal with ==. i.e,
null===undefined --> false but null==undefined --> true

Some of the example which covers the above cases,

```javascript
0 == false// true
0 === false  // false
1 == "1"  // true
1 === "1" // false
null == undefined // true
null === undefined // false
'0' == false // true
'0' === false // false
[]==[] or []===[] //false, refer different objects in memory
{}=={} or {}==={} //false, refer different objects in memory
```
### 5. What is the currying function?
Currying is the process of taking a function with multiple arguments and turning it into a sequence of functions each with only a single argument. Currying is named after a mathematician **Haskell Curry**. By applying currying, a n-ary function turns it into a unary function.

Let's take an example of n-ary function and how it turns into a currying function,

```javascript
const multiArgFunction = (a, b, c) => a + b + c;
console.log(multiArgFunction(1, 2, 3)); // 6

const curryUnaryFunction = (a) => (b) => (c) => a + b + c;
curryUnaryFunction(1); // returns a function: b => c =>  1 + b + c
curryUnaryFunction(1)(2); // returns a function: c => 3 + c
curryUnaryFunction(1)(2)(3); // returns the number 6
```

Curried functions are great to improve **code reusability** and **functional composition**.

## Advanced
### 1. What is a pure function?
A **Pure function** is a function where the return value is only determined by its arguments without any side effects. i.e, If you call a function with the same arguments 'n' number of times and 'n' number of places in the application then it will always return the same value.

Let's take an example to see the difference between pure and impure functions,

```javascript
//Impure
let numberArray = [];
const impureAddNumber = (number) => numberArray.push(number);
//Pure
const pureAddNumber = (number) => (argNumberArray) =>
  argNumberArray.concat([number]);

//Display the results
console.log(impureAddNumber(6)); // returns 1
console.log(numberArray); // returns [6]
console.log(pureAddNumber(7)(numberArray)); // returns [6, 7]
console.log(numberArray); // returns [6]
```

As per the above code snippets, the **Push** function is impure itself by altering the array and returning a push number index independent of the parameter value. . Whereas **Concat** on the other hand takes the array and concatenates it with the other array producing a whole new array without side effects. Also, the return value is a concatenation of the previous array.

Remember that Pure functions are important as they simplify unit testing without any side effects and no need for dependency injection. They also avoid tight coupling and make it harder to break your application by not having any side effects. These principles are coming together with **Immutability** concept of ES6 by giving preference to **const** over **let** usage.

### 2. What is the difference between let and var?
You can list out the differences in a tabular format

| var                                                   | let                         |
| ----------------------------------------------------- | --------------------------- |
| It is been available from the beginning of JavaScript | Introduced as part of ES6   |
| It has function scope                                 | It has block scope          |
| Variables will be hoisted                             | Hoisted but not initialized |

Let's take an example to see the difference,

```javascript
function userDetails(username) {
  if (username) {
console.log(salary); // undefined due to hoisting
console.log(age); // ReferenceError: Cannot access 'age' before initialization
let age = 30;
var salary = 10000;
  }
  console.log(salary); //10000 (accessible to due function scope)
  console.log(age); //error: age is not defined(due to block scope)
}
userDetails("John");
```
### 3. What is the Temporal Dead Zone?
The Temporal Dead Zone is a behavior in JavaScript that occurs when declaring a variable with the let and const keywords, but not with var. In ECMAScript 6, accessing a `let` or `const` variable before its declaration (within its scope) causes a ReferenceError. The time span when that happens, between the creation of a variable’s binding and its declaration, is called the temporal dead zone.

Let's see this behavior with an example,

```javascript
function somemethod() {
  console.log(counter1); // undefined
  console.log(counter2); // ReferenceError
  var counter1 = 1;
  let counter2 = 2;
}
```
### 4. What is Hoisting?
 Hoisting is a JavaScript mechanism where variables, function declarations and classes are moved to the top of their scope before code execution. Remember that JavaScript only hoists declarations, not initialisation.
Let's take a simple example of variable hoisting,

```javascript
console.log(message); //output : undefined
var message = "The variable Has been hoisted";
```

The above code looks like as below to the interpreter,

```javascript
var message;
console.log(message);
message = "The variable Has been hoisted";
```

In the same fashion, function declarations are hoisted too

```javascript
message("Good morning"); //Good morning

function message(name) {
  console.log(name);
}
```

This hoisting makes functions to be safely used in code before they are declared.

### 5. What are closures?
 A closure is the combination of a function and the lexical environment within which that function was declared. i.e, It is an inner function that has access to the outer or enclosing function’s variables. The closure has three scope chains

1. Own scope where variables defined between its curly brackets
2. Outer function’s variables
3. Global variables

Let's take an example of closure concept,

```javascript
function Welcome(name) {
  var greetingInfo = function (message) {
console.log(message + " " + name);
  };
  return greetingInfo;
}
var myFunction = Welcome("John");
myFunction("Welcome "); //Output: Welcome John
myFunction("Hello Mr."); //output: Hello Mr.John
```

As per the above code, the inner function(i.e, greetingInfo) has access to the variables in the outer function scope(i.e, Welcome) even after the outer function has returned.

<h2 align="center">
 React
</h2>

## Basic:

###  1. What is the difference between state and props?

 Both *props* and *state* are plain JavaScript objects. While both of them hold information that influences the output of render, they are different in their functionality with respect to component. Props get passed to the component similar to function parameters whereas state is managed within the component similar to variables declared within a function.

### 2. What are synthetic events in React?

`SyntheticEvent` is a cross-browser wrapper around the browser's native event. Its API is same as the browser's native event, including `stopPropagation()` and `preventDefault()`, except the events work identically across all browsers.

### 3. Why should we not update the state directly?

If you try to update the state directly then it won't re-render the component.

```javascript
//Wrong
this.state.message = 'Hello world'
```

Instead use `setState()` method. It schedules an update to a component's state object. When state changes, the component responds by re-rendering.

```javascript
//Correct
this.setState({ message: 'Hello World' })
```

**Note:** You can directly assign to the state object either in *constructor* or using latest javascript's class field declaration syntax.

### 4. What is the use of refs?

The *ref* is used to return a reference to the element. They *should be avoided* in most cases, however, they can be useful when you need a direct access to the DOM element or an instance of a component.

### 5. What is Virtual DOM?

The *Virtual DOM* (VDOM) is an in-memory representation of *Real DOM*. The representation of a UI is kept in memory and synced with the "real" DOM. It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called *reconciliation*.



## Advanced

### 1. What is Redux and explain how it works?

Redux is an open-source JavaScript library used to manage application state. React uses Redux for building the user interface. 

React Redux is the official React binding for Redux. It allows React components to read data from a Redux Store, and dispatch Actions to the Store to update data. Redux helps apps to scale by providing a sensible way to manage state through a unidirectional data flow model. React Redux is conceptually simple. It subscribes to the Redux store, checks to see if the data which your component wants have changed, and re-renders your component.

To use react redux we have to wrap our app with React Redux Provider and component has to be wrapped with connect method. Connect method is a higher order component which takes two methods and the component itself. 

`e.g connect(mapStateToPrps, mapDispatchToProps)(Component);`

### 2. What are the different phases of component lifecycle?

The component lifecycle has three distinct lifecycle phases:

1. **Mounting:** The component is ready to mount in the browser DOM. This phase covers initialization from `constructor()`, `getDerivedStateFromProps()`, `render()`, and `componentDidMount()` lifecycle methods.

2. **Updating:** In this phase, the component gets updated in two ways, sending the new props and updating the state either from `setState()` or `forceUpdate()`. This phase covers `getDerivedStateFromProps()`, `shouldComponentUpdate()`, `render()`, `getSnapshotBeforeUpdate()` and `componentDidUpdate()` lifecycle methods.

3. **Unmounting:** In this last phase, the component is not needed and gets unmounted from the browser DOM. This phase includes `componentWillUnmount()` lifecycle method.

It's worth mentioning that React internally has a concept of phases when applying changes to the DOM. They are separated as follows

1. **Render** The component will render without any side effects. This applies to Pure components and in this phase, React can pause, abort, or restart the render.

2. **Pre-commit** Before the component actually applies the changes to the DOM, there is a moment that allows React to read from the DOM through the `getSnapshotBeforeUpdate()`.

3. **Commit** React works with the DOM and executes the final lifecycles respectively `componentDidMount()` for mounting, `componentDidUpdate()` for updating, and `componentWillUnmount()` for unmounting.

React 16.3+ Phases (or an [interactive version](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/))

![image](https://user-images.githubusercontent.com/6243528/186761818-61fe3f74-fec9-4204-87e1-623d2a572a94.png)


Before React 16.3

![image](https://user-images.githubusercontent.com/6243528/186762258-fd3f2db4-4469-4899-b25e-6c37d7abf4ba.png)

### 3. What are the lifecycle methods of React?

Before React 16.3

- **componentWillMount:** Executed before rendering and is used for App level configuration in your root component.
- **componentDidMount:** Executed after first rendering and here all AJAX requests, DOM or state updates, and set up event listeners should occur.
- **componentWillReceiveProps:** Executed when particular prop updates to trigger state transitions.
- **shouldComponentUpdate:** Determines if the component will be updated or not. By default it returns `true`. If you are sure that the component doesn't need to render after state or props are updated, you can return false value. It is a great place to improve performance as it allows you to prevent a re-render if component receives new prop.
- **componentWillUpdate:** Executed before re-rendering the component when there are props & state changes confirmed by `shouldComponentUpdate()` which returns true.
- **componentDidUpdate:** Mostly it is used to update the DOM in response to prop or state changes.
- **componentWillUnmount:** It will be used to cancel any outgoing network requests, or remove all event listeners associated with the component.

React 16.3+

- **getDerivedStateFromProps:** Invoked right before calling `render()` and is invoked on *every* render. This exists for rare use cases where you need a derived state. Worth reading [if you need derived state](https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html).
- **componentDidMount:** Executed after first rendering and where all AJAX requests, DOM or state updates, and set up event listeners should occur.
- **shouldComponentUpdate:** Determines if the component will be updated or not. By default, it returns `true`. If you are sure that the component doesn't need to render after the state or props are updated, you can return a false value. It is a great place to improve performance as it allows you to prevent a re-render if component receives a new prop.
- **getSnapshotBeforeUpdate:** Executed right before rendered output is committed to the DOM. Any value returned by this will be passed into `componentDidUpdate()`. This is useful to capture information from the DOM i.e. scroll position.
- **componentDidUpdate:** Mostly it is used to update the DOM in response to prop or state changes. This will not fire if `shouldComponentUpdate()` returns `false`.
- **componentWillUnmount** It will be used to cancel any outgoing network requests, or remove all event listeners associated with the component.

### 4. What are Higher-Order Components?

A *higher-order component* (*HOC*) is a function that takes a component and returns a new component. Basically, it's a pattern that is derived from React's compositional nature.

We call them **pure components** because they can accept any dynamically provided child component but they won't modify or copy any behavior from their input components.

```javascript
const EnhancedComponent = higherOrderComponent(WrappedComponent)
```

HOC can be used for many use cases:

1. Code reuse, logic and bootstrap abstraction.
2. Render hijacking.
3. State abstraction and manipulation.
4. Props manipulation.
    
### 5. What is context and why we prefer redux then context?

*Context* provides a way to pass data through the component tree without having to pass props down manually at every level.

For example, authenticated users, locale preferences, UI themes need to be accessed in the application by many components.

```javascript
const {Provider, Consumer} = React.createContext(defaultValue)
```
Comparing Redux & Context API
| Context API  | 	Redux  |
|:-:|:-:|
| Built-in tool that ships with React  | Additional installation Required, driving up the final bundle size  |
| Requires minimal Setup  | Requires extensive setup to integrate it with a React Application  |
| Specifically designed for static data, that is not often refreshed or updated  | Works like a charm with both static and dynamic data  |
| Adding new contexts requires creation from scratch	  | Easily extendible due to the ease of adding new data/actions after the initial setup  |
| Debugging can be hard in highly nested React Component Structure even with Dev Tool | Incredibly powerful Redux Dev Tools to ease debugging  |
| UI logic and State Management Logic are in the same component	  | Better code organization with separate UI logic and State Management Logic  |
	
	
<h2 align="center">
 HTML
</h2>

## Basics

### 1. What are the entities in HTML?
The HTML character entities are used as a replacement for reserved characters in HTML. You can also replace characters that are not present on your keyboard by entities. These characters are replaced because some characters are reserved in HTML.
```html
<h2>The greater-than sign: &gt;</h2>
```
### 2.  What are the different new form element types in HTML 5?

Following is a list of 10 frequently used new elements in HTML 5:
Color
Date
Datetime-local
Email
Time
Url
Range
Telephone
Number
Search

### 3. What is the difference between progress and meter tag?
The progress element represents the completion progress of a task. The meter element represents a scalar measurement within a known range, or a fractional value; for example disk usage, the relevance of a query result, or the fraction of a voting population to have selected a particular candidate.

### 4. What is the difference between a block-level element and an inline element?

| Block                                                   | Inline                         |
| ----------------------------------------------------- | --------------------------- |
| A block-level element is drawn as a block that stretches to fill the full width available to it i.e, the width of its container and will always start on a new line. <br/>Elements that are block-level by default: <br/> ```html <div>, <img>, <section>, <form>, <nav> ```.| Inline elements are drawn where they are defined and only take up space that is absolutely needed. The easiest way to understand how they work is to look at how text flows on a page. <br/>Examples of elements that are inline by default: <br/>```html <span>, <b>, <strong>, <a>, <input>```.   |

### 5. What is semantic HTML?
Semantic HTML is a coding style. It is the use of HTML markup to reinforce the semantics or meaning of the content. For example: In semantic HTML
```html <b> </b>``` tag is not used for bold statement as well as ```html <i> </i>``` tag is used for italic. Instead of these we use ```html <strong></strong>``` and ```html<em></em>``` tags.

### 6. Explain The Key Differences Between LocalStorage And SessionStorage Objects.
The key differences between localStorage and sessionStorage objects are as follows:

* The localStorage object stores the data without an expiry date. However, sessionStorage object stores the data for only one session.
* In the case of a localStorage object, data will not delete when the browser window closes. However, the data gets deleted if the browser window closes, in the case of sessionStorage objects.
* The data in sessionStorage is accessible only in the current window of the browser. But, the data in the localStorage can be shared between multiple windows of the browser.

<h2 align="center">
 CSS
</h2>

## Basics

### 1. What is the Box model in CSS? Which CSS properties are a part of it?
A rectangle box is wrapped around every HTML element. The box model is used to determine the height and width of the rectangular box. The CSS Box consists of Width and height (or in the absence of that, default values and the content inside), padding, borders, margin.

![image](https://user-images.githubusercontent.com/6243528/187034617-878f36b5-4cca-4bfe-a601-ae22d79540db.png)

* Content:  Actual Content of the box where the text or image is placed.
* Padding: Area surrounding the content (Space between the border and content).
* Border: Area surrounding the padding.
* Margin: Area surrounding the border.

### 2. What are the different types of Selectors in CSS?
A CSS selector is the part of a CSS ruleset that actually selects the content you want to style. Different types of selectors are listed below.

<b>Universal Selector</b>: The universal selector works like a wildcard character, selecting all elements on a page. In the given example, the provided styles will get applied to all the elements on the page.
```css
* {
  color: "green";
  font-size: 20px;
  line-height: 25px;
}
```
<b>Element Type Selector</b>: This selector matches one or more HTML elements of the same name. In the given example, the provided styles will get applied to all the ul elements on the page.
```css
ul {
  line-style: none;
  border: solid 1px #ccc;
}
```
<b>ID Selector</b>: This selector matches any HTML element that has an ID attribute with the same value as that of the selector. In the given example, the provided styles will get applied to all the elements having ID as a container on the page.
```css
#container {
  width: 960px;
  margin: 0 auto;
}
```

```html
<div id="container"></div>
```
<b>Class Selector</b>: The class selector also matches all elements on the page that have their class attribute set to the same value as the class.  In the given example, the provided styles will get applied to all the elements having ID as the box on the page.
```css
.box {
  padding: 10px;
  margin: 10px;
  width: 240px;
}
```
```html
<div class="box"></div>
```
<b>Descendant Combinator</b>: The descendant selector or, more accurately, the descendant combinator lets you combine two or more selectors so you can be more specific in your selection method.
```css
#container .box {
	float: left;
	padding-bottom: 15px;
} 

<div id="container">
	<div class="box"></div>
	
	<div class="box-2"></div>
</div>

<div class=”box”></div>
```
This declaration block will apply to all elements that have a class of box that is inside an element with an ID of the container. It’s worth noting that the .box element doesn’t have to be an immediate child: there could be another element wrapping .box, and the styles would still apply.

<b>Child Combinator</b>: A selector that uses the child combinator is similar to a selector that uses a descendant combinator, except it only targets immediate child elements.
```css
#container> .box {
	float: left;
	padding-bottom: 15px;
}

<div id="container">
	<div class="box"></div>
	
	<div>
		<div class="box"></div>
	</div>
</div>
```
The selector will match all elements that have a class of box and that are immediate children of the #container element. That means, unlike the descendant combinator, there can’t be another element wrapping .box it has to be a direct child element.

<b>General Sibling Combinator</b>: A selector that uses a general sibling combinator to match elements based on sibling relationships. The selected elements are beside each other in the HTML.
```css
h2 ~ p {
	margin-bottom: 20px;
}

<h2>Title</h2>
<p>Paragraph example.</p>
<p>Paragraph example.</p>
<p>Paragraph example.</p>
<div class=”box”>
	<p>Paragraph example.</p>
</div>
```
In this example, all paragraph elements (```<p>```) will be styled with the specified rules, but only if they are siblings of ```<h2>``` elements. There could be other elements in between the ```<h2>``` and ```<p>```, and the styles would still apply.

<b>Adjacent Sibling Combinator</b>: A selector that uses the adjacent sibling combinator uses the plus symbol (+), and is almost the same as the general sibling selector. The difference is that the targeted element must be an immediate sibling, not just a general sibling.
```css
p + p {
	text-indent: 1.Sem;
	margin-bottom: 0;
}
<h2>Title</h2>
<p>Paragraph example.</p>
<p>Paragraph example.</p>
<p>Paragraph example.</p>

<div class=”box”>
	<p>Paragraph example.</p>
	<p>Paragraph example.</p>
</div>
```
The above example will apply the specified styles only to paragraph elements that immediately follow other paragraph elements. This means the first paragraph element on a page would not receive these styles. Also, if another element appeared between two paragraphs, the second paragraph of the two wouldn’t have the styles applied.

<b>Attribute Selector</b>: The attribute selector targets elements based on the presence and/or value of HTML attributes, and is declared using square brackets.
```css
input [type=”text”] {
	background-color: #444;
	width: 200px;
}

<input type="text">
```
<b>Pseudo-classes Selector</b>: A pseudo-class is used to define a special state of an element.

For example, it can be used to:
* Style an element when a user mouses over it
* Style visited and unvisited links differently
* Style an element when it gets focus

```css
input [type=”text”] {
	background-color: #444;
	width: 200px;
}

<input type="text">
```
### 4. What are Pseudo elements and Pseudo classes?
Pseudo-elements allows us to create items that do not normally exist in the document tree, for example ::after.

::before
::after
::first-letter
::first-line
::selection

In the below example, the color will appear only on the first line of the paragraph.
```css
p: :first-line {
	color: #ffOOOO;
	font-variant: small-caps;
}
```
Pseudo-classes select regular elements but under certain conditions like when the user is hovering over the link.

:link
:visited
:hover
:active
:focus
Example of the pseudo-class, In the below example, the color applies to the anchor tag when it’s hovered.
```css
/* mouse over link */
a:hover {
	color: #FFOOFF;
}
```
### 4. What is the difference between inline, inline-block, and block?
<b>Block Element</b>: The block elements always start on a new line. They will also take space for an entire row or width. List of block elements are ```<div>, <p>```.

<b>Inline Elements<b>: Inline elements don't start on a new line, they appear on the same line as the content and tags beside them. Some examples of inline elements are ```<a>, <span> , <strong>,``` and ```<img>`` tags. 

<b>Inline Block Elements</b>: Inline-block elements are similar to inline elements, except they can have padding and margins and set height and width values.

### 5. How is border-box different from content-box?

```content-box``` is the default value box-sizing property. The height and the width properties consist only of the content by excluding the border and padding. Consider an example as shown:
```css
div{
    width:300px;
    height:200px;
    padding:15px;
    border: 5px solid grey;
    margin:30px;
    -moz-box-sizing:content-box;
    -webkit-box-sizing:content-box;
    box-sizing:content-box;
}
```
Here, the box-sizing for the div element is given as content-box. That means, the height and width considered for the div content exclude the padding and border. We will get full height and width parameters specified for the content as shown in the below image.

![image](https://user-images.githubusercontent.com/6243528/187038330-65a49fdd-fbe3-404e-bb41-971d95e59ddf.png)

The border-box property includes the content, padding and border in the height and width properties. Consider an example as shown:
```css
div{
    width:300px;
    height:200px;
    padding:15px;
    border: 5px solid grey;
    margin:30px;
    -moz-box-sizing:border-box;
    -webkit-box-sizing:border-box;
    box-sizing:border-box;
}
```
Here, the box-sizing for the div element is given as border-box. That means the height and width considered for the div content will also include the padding and border. This means that the actual height of the div content will be:
```
actual height = height - 
                padding on top and bottom - 
                border on top and bottom
              = 200 - (15*2) - (5*2) 
              = 160 px
```
and the actual width of the div content would be:
```
actual width  = width - 
                padding on right and left - 
                border on right and left
              = 300 - (15*2) - (5*2) 
              = 260 px
```
This is represented in the image below:

![image](https://user-images.githubusercontent.com/6243528/187038308-05e8299f-3e18-41d9-bfa9-771d3fca39cf.png)

## Advanced

### 1. Explain CSS position property?
<b>Absolute</b>: To place an element exactly where you want to place it. absolute position is actually set relative to the element's parent. if no parent is available then the relative place to the page itself (it will default all the way back up to the element).
<b>Relative</b>: "Relative to itself". Setting position: relative; on an element and no other positioning attributes, it will no effect on its positioning. It allows the use of z-index on the element and it limits the scope of absolutely positioned child elements. Any child element will be absolutely positioned within that block. 
<b>Fixed</b>: The element is positioned relative to the viewport or the browser window itself. viewport doesn't change if you scroll and hence the fixed element will stay right in the same position. 
<b>Static</b>: Static default for every single page element. The only reason you would ever set an element to position: static is to forcefully remove some positioning that got applied to an element outside of your control.
<b>Sticky</b>: Sticky positioning is a hybrid of relative and fixed positioning. The element is treated as relative positioned until it crosses a specified threshold, at which point it is treated as fixed positioned.

### 2. Different Box Sizing Property?
The box-sizing CSS property sets how the total width and height of an element are calculated.

<b>Content-box</b>: The default width and height values apply to the element's content only. The padding and border are added to the outside of the box.
<b>Padding-box</b>: Width and height values apply to the element's content and its padding. The border is added to the outside of the box. Currently, only Firefox supports the padding-box value.
<b>Border-box</b>: Width and height values apply to the content, padding, and border.

### 3. How to center align a div inside another div?

* <b>Centering with Table</b>:
HTML:

```css
<div class=”cn”><div class=”inner”>your content</div></div>
CSS:

.cn {
	display: table-cell;
	width: 500px;
	height: 500px;
	vertical-align: middle;
	text-align: center;
}

.inner {
	display: inline-block;
	width: 200px; height: 200px;
}
```
* <b>Centering with Transform</b>
HTML:
```css
<div class="cn"><div class="inner">your content</div></div>
```
CSS:
```css
.cn {
	position: relative;
	width: 500px;
	height: 500px;
}

.inner {
	position: absolute;
	top: 50%; left: 50%;
	transform: translate(-50%,-50%);
	width: 200px;
	height: 200px;
}
```
* <b>Centering with Flexbox</b>
HTML:
```css
<div class="cn"><div class="inner">your content</div></div>
```
CSS:
```css
.cn {
	display: flex;
	justify-content: center;
	align-items: center;
}
```
* <b>Centering with Grid</b>
HTML:
```css
<div class=”wrap_grid”>
	<div id=”container”>vertical aligned text<br />some more text here
	</div>
</div>
```
CSS:
```css
.wrap-grid {
	display: grid;
	place-content: center;
}
```

### 4. Difference between CSS grid vs flexbox?

The basic difference between CSS Grid Layout and CSS Flexbox Layout is that flexbox was designed for layout in one dimension - either a row or a column. Grid was designed for two-dimensional layout - rows, and columns at the same time. The two specifications share some common features, however, and if you have already learned how to use flexbox, the similarities should help you get to grips with Grid.

One-dimensional versus two-dimensional layout
A simple example can demonstrate the difference between one- and two-dimensional layouts.

In this first example, I am using flexbox to lay out a set of boxes. I have five child items in my container, and I have given the flex properties values so that they can grow and shrink from a flex-basis of 150 pixels.

I have also set the flex-wrap property to wrap, so that if the space in the container becomes too narrow to maintain the flex basis, items will wrap onto a new row.

```css
<div class="wrapper">
  <div>One</div>
  <div>Two</div>
  <div>Three</div>
  <div>Four</div>
  <div>Five</div>
</div>


.wrapper {
  width: 500px;
  display: flex;
  flex-wrap: wrap;
}
.wrapper > div {
  flex: 1 1 150px;
}

```
![image](https://user-images.githubusercontent.com/6243528/187037923-2715bb68-3fdd-4ed7-8f9b-6b7ae94ac41e.png)

In the image, you can see that two items have wrapped onto a new line. These items are sharing the available space and not lining up underneath the items above. This is because when you wrap flex items, each new row (or column when working by column) is an independent flex line in the flex container. Space distribution happens across the flex line.

A common question then is how to make those items line up. This is where you want a two-dimensional layout method: You want to control the alignment by row and column, and this is where grid comes in.

The same layout with CSS grids
In this next example, I create the same layout using Grid. This time we have three 1fr column tracks. We do not need to set anything on the items themselves; they will lay themselves out one into each cell of the created grid. As you can see they stay in a strict grid, lining up in rows and columns. With five items, we get a gap on the end of row two.
```css
<div class="wrapper">
  <div>One</div>
  <div>Two</div>
  <div>Three</div>
  <div>Four</div>
  <div>Five</div>
</div>

.wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```
![image](https://user-images.githubusercontent.com/6243528/187037953-e12c0dee-f185-4ed7-8fd8-07155d57aff1.png)

A simple question to ask yourself when deciding between grid or flexbox is:

do I only need to control the layout by row or column – use a flexbox
do I need to control the layout by row and column – use a grid

### 5. What is specificity? How to calculate specificity?
A process of determining which CSS rule will be applied to an element. It actually determines which rules will take precedence. Inline style usually wins then ID then the class value (or pseudo-class or attribute selector), the universal selector (*) has no specificity. ID selectors have a higher specificity than attribute selectors.

### 6. What is progressive rendering? How do you implement progressive rendering in the website?. What are the advantages of it?
Progressive rendering is the name given to techniques used to improve the performance of a webpage (in particular, improve perceived load time) to render content for display as quickly as possible.

We can implement the progressive rendering of the page by loading the lazy loading of the images.  We can use Intersection Observer API to lazy load the image. The API makes it simple to detect when an element enters the viewport and take an action when it does. Once the image enters the viewport, we will start loading the images.

A sample snippet is given below.

```css
<img class="lazy"
src="placeholder-image.jpg"
data-src="image-to-lazy-load-1x.jpg"
data-srcset="image-to-lazy-load-2x.jpg 2x, image-to-lazy-load-1x.jpg 1x"
alt="I'm an image!">
```
```javascript
document.addEventListener("DOMContentLoaded", function() {
  var lazyImages = [].slice.call(document.querySelectorAll("img.lazy"));

  if ("IntersectionObserver" in window) {
    let lazyImageObserver = new IntersectionObserver(function(entries, observer) {
      entries.forEach(function(entry) {
        if (entry.isIntersecting) {
          let lazyImage = entry.target;
          lazyImage.src = lazyImage.dataset.src;
          lazyImage.srcset = lazyImage.dataset.srcset;
          lazyImage.classList.remove("lazy");
          lazyImageObserver.unobserve(lazyImage);
        }
      });
    });

    lazyImages.forEach(function(lazyImage) {
      lazyImageObserver.observe(lazyImage);
    });
  } else {
    // Possibly fall back to event handlers here
  }
});
```

Credit goes to https://github.com/sudheerj and Myself :)
