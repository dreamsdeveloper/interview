# Interview Questions

<h2 align="center">
 JavaScript
</h2>

## Basic:

### 1. What are the possible ways to create objects in JavaScript?

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
var object = new Person('Sudheer');
```

5. **Function constructor with prototype:**

This is similar to function constructor but it uses prototype for their properties and methods,

```javascript
function Person() {}
Person.prototype.name = 'Sudheer';
var object = new Person();
```

This is equivalent to an instance created with an object create method with a function prototype and then call that function with an instance and parameters as arguments.

```javascript
function func() {}

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

var object = new Person('Sudheer');
```

7. **Singleton pattern:**

A Singleton is an object which can only be instantiated one time. Repeated calls to its constructor return the same instance and this way one can ensure that they don't accidentally create multiple instances.

```javascript
var object = new (function () {
  this.name = 'Sudheer';
})();
```

### 2. What is the difference between Call, Apply and Bind?

The difference between Call, Apply and Bind can be explained with below examples,

**Call:** The call() method invokes a function with a given `this` value and arguments provided one by one

```javascript
var employee1 = { firstName: 'John', lastName: 'Rodson' };
var employee2 = { firstName: 'Jimmy', lastName: 'Baily' };

function invite(greeting1, greeting2) {
  console.log(
    greeting1 + ' ' + this.firstName + ' ' + this.lastName + ', ' + greeting2
  );
}

invite.call(employee1, 'Hello', 'How are you?'); // Hello John Rodson, How are you?
invite.call(employee2, 'Hello', 'How are you?'); // Hello Jimmy Baily, How are you?
```

**Apply:** Invokes the function with a given `this` value and allows you to pass in arguments as an array

```javascript
var employee1 = { firstName: 'John', lastName: 'Rodson' };
var employee2 = { firstName: 'Jimmy', lastName: 'Baily' };

function invite(greeting1, greeting2) {
  console.log(
    greeting1 + ' ' + this.firstName + ' ' + this.lastName + ', ' + greeting2
  );
}

invite.apply(employee1, ['Hello', 'How are you?']); // Hello John Rodson, How are you?
invite.apply(employee2, ['Hello', 'How are you?']); // Hello Jimmy Baily, How are you?
```

**bind:** returns a new function, allowing you to pass any number of arguments

```javascript
var employee1 = { firstName: 'John', lastName: 'Rodson' };
var employee2 = { firstName: 'Jimmy', lastName: 'Baily' };

function invite(greeting1, greeting2) {
  console.log(
    greeting1 + ' ' + this.firstName + ' ' + this.lastName + ', ' + greeting2
  );
}

var inviteEmployee1 = invite.bind(employee1);
var inviteEmployee2 = invite.bind(employee2);
inviteEmployee1('Hello', 'How are you?'); // Hello John Rodson, How are you?
inviteEmployee2('Hello', 'How are you?'); // Hello Jimmy Baily, How are you?
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

### 4. What is the difference between == and === operators?

JavaScript provides both strict(===, !==) and type-converting(==, !=) equality comparison. The strict operators take type of variable in consideration, while non-strict operators make type correction/conversion based upon values of variables. The strict operators follow the below conditions for different types,

1. Two strings are strictly equal when they have the same sequence of characters, same length, and same characters in corresponding positions.
2. Two numbers are strictly equal when they are numerically equal. i.e, Having the same number value.
   There are two special cases in this,
3. NaN is not equal to anything, including NaN.
4. Positive and negative zeros are equal to one another.
5. Two Boolean operands are strictly equal if both are true or both are false.
6. Two objects are strictly equal if they refer to the same Object.
7. Null and Undefined types are not equal with ===, but equal with ==. i.e,
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

## Intermediate

### 1. What is optional chaining?

According to MDN official docs, the optional chaining operator (?.) permits reading the value of a property located deep within a chain of connected objects without having to expressly validate that each reference in the chain is valid.

The ?. operator is like the . chaining operator, except that instead of causing an error if a reference is nullish (null or undefined), the expression short-circuits with a return value of undefined. When used with function calls, it returns undefined if the given function does not exist.

```javascript
const adventurer = {
  name: 'Alice',
  cat: {
    name: 'Dinah',
  },
};

const dogName = adventurer.dog?.name;
console.log(dogName);
// expected output: undefined

console.log(adventurer.someNonExistentMethod?.());
// expected output: undefined
```

### 2. What is throttling?

Throttling is a technique used to limit the execution of an event handler function, even when this event triggers continuously due to user actions. The common use cases are browser resizing, window scrolling etc.

The below example creates a throttle function to reduce the number of events for each pixel change and trigger scroll event for each 100ms except for the first event.

```javascript
const throttle = (func, limit) => {
  let inThrottle;
  return (...args) => {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => (inThrottle = false), limit);
    }
  };
};
window.addEventListener('scroll', () => {
  throttle(handleScrollAnimation, 100);
});
```

### 3. What is debouncing?

Debouncing is a programming pattern that allows delaying execution of some piece of code until a specified time to avoid unnecessary CPU cycles, API calls and improve performance. The debounce function make sure that your code is only triggered once per user input. The common usecases are Search box suggestions, text-field auto-saves, and eliminating double-button clicks.

Let's say you want to show suggestions for a search query, but only after a visitor has finished typing it. So here you write a debounce function where the user keeps writing the characters with in 500ms then previous timer cleared out using clearTimeout and reschedule API call/DB query for a new time—300 ms in the future.

```javascript
function debounce(func, timeout = 500) {
  let timer;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => {
      func.apply(this, args);
    }, timeout);
  };
}
function fetchResults() {
  console.log('Fetching input suggestions');
}
const processChange = debounce(() => fetchResults());
```

### 4. What is function execution context?

Whenever a function is invoked, the JavaScript engine creates a different type of Execution Context known as a Function Execution Context (FEC) within the Global Execution Context (GEC) to evaluate and execute the code within that function.

### 5. What is global execution context?

The global execution context is the default or first execution context that is created by the JavaScript engine before any code is executed(i.e, when the file first loads in the browser). All the global code that is not inside a function or object will be executed inside this global execution context. Since JS engine is single threaded there will be only one global environment and there will be only one global execution context.

For example, the below code other than code inside any function or object is executed inside the global execution context.

```javascript
var x = 10;

function A() {
  console.log('Start function A');

  function B() {
    console.log('In function B');
  }

  B();
}

A();

console.log('GlobalContext');
```

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
userDetails('John');
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
var message = 'The variable Has been hoisted';
```

The above code looks like as below to the interpreter,

```javascript
var message;
console.log(message);
message = 'The variable Has been hoisted';
```

In the same fashion, function declarations are hoisted too

```javascript
message('Good morning'); //Good morning

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
    console.log(message + ' ' + name);
  };
  return greetingInfo;
}
var myFunction = Welcome('John');
myFunction('Welcome '); //Output: Welcome John
myFunction('Hello Mr.'); //output: Hello Mr.John
```

As per the above code, the inner function(i.e, greetingInfo) has access to the variables in the outer function scope(i.e, Welcome) even after the outer function has returned.

<h2 align="center">
 Node
</h2>

## Basic:

### 1. What is a first class function in Javascript?

When functions can be treated like any other variable then those functions are first-class functions. There are many other programming languages, for example, scala, Haskell, etc which follow this including JS. Now because of this function can be passed as a param to another function(callback) or a function can return another function(higher-order function). map() and filter() are higher-order functions that are popularly used.

### 2. What is Node.js and how it works?

Node.js is a virtual machine that uses JavaScript as its scripting language and runs Chrome’s V8 JavaScript engine. Basically, Node.js is based on an event-driven architecture where I/O runs asynchronously making it lightweight and efficient. It is being used in developing desktop applications as well with a popular framework called electron as it provides API to access OS-level features such as file system, network, etc.

### 3. What is fork in node JS?

A fork in general is used to spawn child processes. In node it is used to create a new instance of v8 engine to run multiple workers to execute the code.

### 4. What is REPL?

PL in Node.js stands for Read, Eval, Print, and Loop, which further means evaluating code on the go.

### 5. Why is Node.js single-threaded?

Node.js was created explicitly as an experiment in async processing. This was to try a new theory of doing async processing on a single thread over the existing thread-based implementation of scaling via different frameworks.

## Intermediate:

### 1. What do you understand by callback hell?

```javascript
async_A(function(){
   async_B(function(){
       async_C(function(){
           async_D(function(){
           ....
           });
       });
   });
});
```

For the above example, we are passing callback functions and it makes the code unreadable and not maintainable, thus we should change the async logic to avoid this.

### 2. What is an event-loop in Node JS?

Whatever that is async is managed by event-loop using a queue and listener. We can get the idea using the following diagram:

<img width="518" alt="eventloop" src="https://user-images.githubusercontent.com/112413233/206873315-9e1967d3-3a3b-45bd-ad19-982a9a75f577.png">

So when an async function needs to be executed(or I/O) the main thread sends it to a different thread allowing v8 to keep executing the main code. Event loop involves different phases with specific tasks such as timers, pending callbacks, idle or prepare, poll, check, close callbacks with different FIFO queues. Also in between iterations it checks for async I/O or timers and shuts down cleanly if there aren't any.

### 3. If Node.js is single threaded then how does it handle concurrency?

The main loop is single-threaded and all async calls are managed by libuv library.

For example:

```javascript
const crypto = require('crypto');
const start = Date.now();
function logHashTime() {
  crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
    console.log('Hash: ', Date.now() - start);
  });
}
logHashTime();
logHashTime();
logHashTime();
logHashTime();
```

This gives the output:

```javascript
Hash: 1213;
Hash: 1225;
Hash: 1212;
Hash: 1222;
```

This is because libuv sets up a thread pool to handle such concurrency. How many threads will be there in the thread pool depends upon the number of cores but you can override this.

### 4. Differentiate between process.nextTick() and setImmediate()?

Both can be used to switch to an asynchronous mode of operation by listener functions.

process.nextTick() sets the callback to execute but setImmediate pushes the callback in the queue to be executed. So the event loop runs in the following manner

timers–>pending callbacks–>idle,prepare–>connections(poll,data,etc)–>check–>close callbacks

In this process.nextTick() method adds the callback function to the start of the next event queue and setImmediate() method to place the function in the check phase of the next event queue

### 5. What is node.js streams?

Streams are instances of EventEmitter which can be used to work with streaming data in Node.js. They can be used for handling and manipulating streaming large files(videos, mp3, etc) over the network. They use buffers as their temporary storage.

There are mainly four types of the stream:

Writable: streams to which data can be written (for example, fs.createWriteStream()).
Readable: streams from which data can be read (for example, fs.createReadStream()).
Duplex: streams that are both Readable and Writable (for example, net.Socket).
Transform: Duplex streams that can modify or transform the data as it is written and read (for example, zlib.createDeflate()).

### 6. What are node.js buffers?

In general, buffers is a temporary memory that is mainly used by stream to hold on to some data until consumed. Buffers are introduced with additional use cases than JavaScript’s Unit8Array and are mainly used to represent a fixed-length sequence of bytes. This also supports legacy encodings like ASCII, utf-8, etc. It is a fixed(non-resizable) allocated memory outside the v8.

### 7. What is middleware?

Middleware comes in between your request and business logic. It is mainly used to capture logs and enable rate limit, routing, authentication, basically whatever that is not a part of business logic. There are third-party middleware also such as body-parser and you can write your own middleware for a specific use case.

### 8. Explain what a Reactor Pattern in Node.js?

Reactor pattern again a pattern for nonblocking I/O operations. But in general, this is used in any event-driven architecture.

There are two components in this: 1. Reactor 2. Handler.

Reactor: Its job is to dispatch the I/O event to appropriate handlers
Handler: Its job is to actually work on those events

## Advanced:

### 1. What is an Event Emitter in Node.js?

EventEmitter is a Node.js class that includes all the objects that are basically capable of emitting events. This can be done by attaching named events that are emitted by the object using an eventEmitter.on() function. Thus whenever this object throws an even the attached functions are invoked synchronously.

```javascript
const EventEmitter = require('events');
class MyEmitter extends EventEmitter {}
const myEmitter = new MyEmitter();
myEmitter.on('event', () => {
  console.log('an event occurred!');
});
myEmitter.emit('event');
```

### 2. Enhancing Node.js performance through clustering.

Node.js applications run on a single processor, which means that by default they don’t take advantage of a multiple-core system. Cluster mode is used to start up multiple node.js processes thereby having multiple instances of the event loop. When we start using cluster in a nodejs app behind the scene multiple node.js processes are created but there is also a parent process called the cluster manager which is responsible for monitoring the health of the individual instances of our application.

<img width="2275" alt="cluster" src="https://user-images.githubusercontent.com/112413233/206873347-6cbcde9f-6a82-4875-b219-feb1a90e3bb0.png">

Clustering in Node.js

### 3. What is a thread pool and which library handles it in Node.js

The Thread pool is handled by the libuv library. libuv is a multi-platform C library that provides support for asynchronous I/O-based operations such as file systems, networking, and concurrency.
<img width="1524" alt="sss" src="https://user-images.githubusercontent.com/112413233/206873365-e85ed49f-a713-4a95-b716-2ad04906b37f.png">

Thread Pool

### 4. What is WASI and why is it being introduced?

Web assembly provides an implementation of WebAssembly System Interface specification through WASI API in node.js implemented using WASI class. The introduction of WASI was done by keeping in mind its possible to use the underlying operating system via a collection of POSIX-like functions thus further enabling the application to use resources more efficiently and features that require system-level access.

### 5. How are worker threads different from clusters?

Cluster:

There is one process on each CPU with an IPC to communicate.
In case we want to have multiple servers accepting HTTP requests via a single port, clusters can be helpful.
The processes are spawned in each CPU thus will have separate memory and node instance which further will lead to memory issues.
Worker threads:

There is only one process in total with multiple threads.
Each thread has one Node instance (one event loop, one JS engine) with most of the APIs accessible.
Shares memory with other threads (e.g. SharedArrayBuffer)
This can be used for CPU-intensive tasks like processing data or accessing the file system since NodeJS is single-threaded, synchronous tasks can be made more efficient leveraging the worker's threads.

### 6. How to measure the duration of async operations?

Performance API provides us with tools to figure out the necessary performance metrics. A simple example would be using async_hooks and perf_hooks

```javascript
'use strict';
const async_hooks = require('async_hooks');
const { performance, PerformanceObserver } = require('perf_hooks');
const set = new Set();
const hook = async_hooks.createHook({
  init(id, type) {
    if (type === 'Timeout') {
      performance.mark(`Timeout-${id}-Init`);
      set.add(id);
    }
  },
  destroy(id) {
    if (set.has(id)) {
      set.delete(id);
      performance.mark(`Timeout-${id}-Destroy`);
      performance.measure(
        `Timeout-${id}`,
        `Timeout-${id}-Init`,
        `Timeout-${id}-Destroy`
      );
    }
  },
});
hook.enable();
const obs = new PerformanceObserver((list, observer) => {
  console.log(list.getEntries()[0]);
  performance.clearMarks();
  observer.disconnect();
});
obs.observe({ entryTypes: ['measure'], buffered: true });
setTimeout(() => {}, 1000);
```

This would give us the exact time it took to execute the callback.

### 7. How to measure the performance of async operations?

Performance API provides us with tools to figure out the necessary performance metrics.

A simple example would be:

```javascript
const { PerformanceObserver, performance } = require('perf_hooks');
const obs = new PerformanceObserver((items) => {
  console.log(items.getEntries()[0].duration);
  performance.clearMarks();
});
obs.observe({ entryTypes: ['measure'] });
performance.measure('Start to Now');
performance.mark('A');
doSomeLongRunningProcess(() => {
  performance.measure('A to Now', 'A');
  performance.mark('B');
  performance.measure('A to B', 'A', 'B');
});
```

<h2 align="center">
 React
</h2>

## Basic:

### 1. What is the difference between state and props?

Both _props_ and _state_ are plain JavaScript objects. While both of them hold information that influences the output of render, they are different in their functionality with respect to component. Props get passed to the component similar to function parameters whereas state is managed within the component similar to variables declared within a function.

### 2. What are synthetic events in React?

`SyntheticEvent` is a cross-browser wrapper around the browser's native event. Its API is same as the browser's native event, including `stopPropagation()` and `preventDefault()`, except the events work identically across all browsers.

### 3. Why should we not update the state directly?

If you try to update the state directly then it won't re-render the component.

```javascript
//Wrong
this.state.message = 'Hello world';
```

Instead use `setState()` method. It schedules an update to a component's state object. When state changes, the component responds by re-rendering.

```javascript
//Correct
this.setState({ message: 'Hello World' });
```

**Note:** You can directly assign to the state object either in _constructor_ or using latest javascript's class field declaration syntax.

### 4. What is the use of refs?

The _ref_ is used to return a reference to the element. They _should be avoided_ in most cases, however, they can be useful when you need a direct access to the DOM element or an instance of a component.

### 5. What is Virtual DOM?

The _Virtual DOM_ (VDOM) is an in-memory representation of _Real DOM_. The representation of a UI is kept in memory and synced with the "real" DOM. It's a step that happens between the render function being called and the displaying of elements on the screen. This entire process is called _reconciliation_.

## Intermediate

### 1. What is the difference between useState and useRef hook?

i. useState causes components to re-render after state updates whereas useRef doesn’t cause a component to re-render when the value or state changes. Essentially, useRef is like a “box” that can hold a mutable value in its (.current) property.

ii. useState allows us to update the state inside components. While useRef allows refrencing DOM elements.

### 2. What is state mutation and how to prevent it?

State mutation happens when you try to update the state of a component without actually using setState function. This can happen when you are trying to do some computations using a state variable and unknowingly save the result in the same state variable. This is the main reason why it is advised to return new instances of state variables from the reducers by using Object.assign({}, ...) or spread syntax.

This can cause unknown issues in the UI as the value of the state variable got updated without telling React to check what all components were being affected from this update and it can cause UI bugs.

Ex:

```javascript
class A extends React.component {
constructor(props) {
super(props);
this.state = {
loading: false
}
}

componentDidMount() {
let { loading } = this.state;
loading = (() => true)();
}
```

How to prevent it: Make sure your state variables are immutable by either enforcing immutability by using plugins like Immutable.js, always using setState to make updates, and returning new instances in reducers when sending updated state values.

### 3. What is prop drilling?

Prop Drilling is the process by which you pass data from one component of the React Component tree to another by going through other components that do not need the data but only help in passing it around.

### 4. What are the benefits of using typescript with reactjs?

Below are some of the benefits of using typescript with Reactjs,

i. It is possible to use latest JavaScript features
ii. Use of interfaces for complex type definitions
iii. IDEs such as VS Code was made for TypeScript
iv. Avoid bugs with the ease of readability and Validation

### 5. What is the difference between Imperative and Declarative in React?

Imagine a simple UI component, such as a "Like" button. When you tap it, it turns blue if it was previously grey, and grey if it was previously blue.

The imperative way of doing this would be:

```javascript
if (user.likes()) {
  if (hasBlue()) {
    removeBlue();
    addGrey();
  } else {
    removeGrey();
    addBlue();
  }
}
```

Basically, you have to check what is currently on the screen and handle all the changes necessary to redraw it with the current state, including undoing the changes from the previous state. You can imagine how complex this could be in a real-world scenario.

In contrast, the declarative approach would be:

```javascript
if (this.state.liked) {
  return <blueLike />;
} else {
  return <greyLike />;
}
```

Because the declarative approach separates concerns, this part of it only needs to handle how the UI should look in a sepecific state, and is therefore much simpler to understand.

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

- **getDerivedStateFromProps:** Invoked right before calling `render()` and is invoked on _every_ render. This exists for rare use cases where you need a derived state. Worth reading [if you need derived state](https://reactjs.org/blog/2018/06/07/you-probably-dont-need-derived-state.html).
- **componentDidMount:** Executed after first rendering and where all AJAX requests, DOM or state updates, and set up event listeners should occur.
- **shouldComponentUpdate:** Determines if the component will be updated or not. By default, it returns `true`. If you are sure that the component doesn't need to render after the state or props are updated, you can return a false value. It is a great place to improve performance as it allows you to prevent a re-render if component receives a new prop.
- **getSnapshotBeforeUpdate:** Executed right before rendered output is committed to the DOM. Any value returned by this will be passed into `componentDidUpdate()`. This is useful to capture information from the DOM i.e. scroll position.
- **componentDidUpdate:** Mostly it is used to update the DOM in response to prop or state changes. This will not fire if `shouldComponentUpdate()` returns `false`.
- **componentWillUnmount** It will be used to cancel any outgoing network requests, or remove all event listeners associated with the component.

### 4. What are Higher-Order Components?

A _higher-order component_ (_HOC_) is a function that takes a component and returns a new component. Basically, it's a pattern that is derived from React's compositional nature.

We call them **pure components** because they can accept any dynamically provided child component but they won't modify or copy any behavior from their input components.

```javascript
const EnhancedComponent = higherOrderComponent(WrappedComponent);
```

HOC can be used for many use cases:

1. Code reuse, logic and bootstrap abstraction.
2. Render hijacking.
3. State abstraction and manipulation.
4. Props manipulation.

### 5. What is context and why we prefer redux then context?

_Context_ provides a way to pass data through the component tree without having to pass props down manually at every level.

For example, authenticated users, locale preferences, UI themes need to be accessed in the application by many components.

```javascript
const { Provider, Consumer } = React.createContext(defaultValue);
```

Comparing Redux & Context API
| Context API | Redux |
|:-:|:-:|
| Built-in tool that ships with React | Additional installation Required, driving up the final bundle size |
| Requires minimal Setup | Requires extensive setup to integrate it with a React Application |
| Specifically designed for static data, that is not often refreshed or updated | Works like a charm with both static and dynamic data |
| Adding new contexts requires creation from scratch | Easily extendible due to the ease of adding new data/actions after the initial setup |
| Debugging can be hard in highly nested React Component Structure even with Dev Tool | Incredibly powerful Redux Dev Tools to ease debugging |
| UI logic and State Management Logic are in the same component | Better code organization with separate UI logic and State Management Logic |

<h2 align="center">
 GQL
</h2>

## Basics

### 1. What is GraphQL?

GraphQL is a query language which provides a common interface between the client and the server for data fetching and manipulations.

The client asks for various data from the GraphQL server via queries. The response format is described in the query and defined by the client instead of the server: they are called client‐specified queries.
The structure of the data is not hardcoded as in traditional REST APIs - this makes retrieving data from the server more efficient for the client.

### 2. Is GraphQL a Database Technology?

No. GraphQL is often confused with being a database technology. This is a misconception, GraphQL is a query language for APIs - not databases. In that sense it’s database agnostic and can be used with any kind of database or even no database at all.

### 3. What is an exclamation point in GraphQL?

That means that the field is non-nullable. By default, all types in GraphQL are nullable. When non-null is applied to the type of a field, it means that if the server resolves that field to null, the response will fail validation.

### 4. What is difference between Mutation and Query?

Technically any GraphQL query could be implemented to cause a data write. But there is a convention that any operations that cause writes should be sent explicitly via a mutation.

Besides the difference in the semantic, there is one important technical difference:

Query fields can be executed in parallel by the GraphQL engine while Mutation top-level fields MUST execute serially according to the spec.

### 5. What is GraphQL schema?

Every GraphQL server has two core parts that determine how it works: a schema and resolve functions.

The schema is a model of the data that can be fetched through the GraphQL server. It defines what queries clients are allowed to make, what types of data can be fetched from the server, and what the relationships between these types are.

Consider:

```javascript
type Author {
    id: Int
  name: String
  posts: [Post]
}
type Post {
    id: Int
  title: String
  text: String
  author: Author
}
type Query {
  getAuthor(id: Int): Author
  getPostsByTitle(titleContains: String): [Post]
}
schema {
    query: Query
}
```

## Intermediate

### 1. List the key concepts of the GraphQL query language

<b> 1 – Schema Definition Language (SDL)</b>

GraphQL has its own type system. This system is used to define the schema of an API. Basically, the syntax for writing schemas is known as Schema Definition Language or SDL.

<b> 2 – Queries </b>

Queries are one of the fundamental reasons of using GraphQL. At its core, GraphQL is a query language.

In REST API, we fetch data from specific endpoints. Each endpoint has a particular structure. In other words, the client needs to adhere to the API structure. Basically, the request URL determines the query parameters in a REST API.

However, GraphQL has a considerably different approach. Instead of multiple endpoints, a GraphQL server typically exposes only one endpoint. The structure of the response is not fixed. Instead, it is quite flexible. Basically, the client specifies what data is required and the server responds with the required data.

This means that the client needs to send more information to the server. This information is nothing but the query.

<b> 3 – Mutations </b>

While queries are great, we also need to update information using APIs. GraphQL supports updating data using the concept of mutations. We can create, update as well as delete data using mutations.

Mutations also follow a similar structure as queries. However, the only difference is the use of mutation keyword.

<b> 4 – Subscriptions </b>

Another one of the important GraphQL Core Concepts is around the topic of subscriptions. In many modern application, it is important to have a real-time connection between server and client so that the client can be immediately informed about important events.

Subscriptions don’t follow the typical request-response cycle. When a client subscribes to an event, it will hold the connection. When the particular event occurs, the server pushes the data to the client.

Subscriptions are also written using the same format as queries and mutations.

### 2. How to do Server-side Caching?

One common concern with GraphQL, especially when comparing it to REST, are the difficulties to maintain server-side cache. With REST, it’s easy to cache the data for each endpoint, since it’s sure that the structure of the data will not change.

With GraphQL on the other hand, it’s not clear what a client will request next, so putting a caching layer right behind the API doesn’t make a lot of sense.

Server-side caching still is a challenge with GraphQL. More info about caching can be found on the GraphQL website.

### 3. How to do Authentication and Authorization?

Authentication and authorization are often confused. Authentication describes the process of claiming an identity. That’s what you do when you log in to a service with a username and password, you authenticate yourself. Authorization on the other hand describes permission rules that specify the access rights of individual users and user groups to certain parts of the system.

Authentication in GraphQL can be implemented with common patterns such as OAuth.

To implement authorization, it is recommended to delegate any data access logic to the business logic layer and not handle it directly in the GraphQL implementation.

### 4. Does GraphQL Support Offline Usage?

GraphQL is a query language for (web) APIs, and in that sense by definition only works online. However, offline support on the client-side is a valid concern. The caching abilities of Relay and Apollo might already be enough for some use cases, but there isn’t a popular solution for actually persisting stored data yet. You can gain some more insights in the GitHub issues of Relay and Apollo where offline support is discussed.

### 5. Explain the main difference between REST and GraphQL

A REST API is an architectural concept for network-based software. GraphQL, on the other hand, is a query language, a specification, and a set of tools that operates over a single endpoint using HTTP. In addition, over the last few years, REST has been used to make new APIs, while the focus of GraphQL has been to optimize for performance and flexibility.

## Advanced

### 1. Are there any disadvantages to GraphQL?

1. You need to learn how to set up GraphQL. The ecosystem is still rapidly evolving so you have to keep up.
2. You need to send the queries from the client, you can just send strings but if you want more comfort and caching you'll use a client library -> extra code in your client
3. You need to define the schema beforehand => extra work before you get results
4. You need to have a graphql endpoint on your server => new libraries that you don't know yet
5. Graphql queries are more bytes than simply going to a REST endpoint
6. The server needs to do more processing to parse the query and verify the parameters

### 2. What is AST in graphql?

GraphQL is two things:

A query language
A Type System
When a GraphQL server receives a query to process it generally comes in as a single String. This string must be split into meaningful sub-strings (tokenization) and parsed into a representation that the machine understands. This representation is called an abstract syntax tree, or AST.

When GraphQL Processes the query, it walks the tree executing each part against the schema.

Converting raw strings to an AST is the first step of every compiler from C++ to Chrome's JavaScript's VM to Babel.

As for what GraphQL does and how it helps, here is a video that may explain it in a bit more detail. https://www.youtube.com/watch?v=PmWho45WmQY

### 3. Can a GraphQL input type inherit from another type or interface?

No, the spec does not allow input types to implement interfaces. And GraphQL type system in general does not define any form of inheritance (the extends keyword adds fields to an existing type, and isn't for inheritance). The spec is intentionally constrained to stay simple. This means that you're stuck repeating fields across input types.

That said, depending on the way you construct your schema, you could build some kind of type transformer that appends the common fields programmatically based on some meta-data, e.g. a directive.

Better yet, you might be able to solve your problem via composition (always keep composition over inheritance in mind). E.g.

input Name {
firstName: String
lastName: String
}

input UserInput {
name: Name
password: String!
}

input UserChangesInput {
name: Name
id: ID!
password: String
}
The client now has to send an object a level deeper, but that doesn't sound like much of a price for avoiding big repeating chunks. It might actually be good for the client as well, as they can now have common logic for building names, regardless of the query/mutation using them.

In this example, where it's only 2 simple fields, this approach is an overkill, but in general - I'd say it's the way to go.

<h2 align="center">
 HTML
</h2>

## Basics

### 1. What are the entities in HTML?

The HTML character entities are used as a replacement for reserved characters in HTML. You can also replace characters that are not present on your keyboard by entities. These characters are replaced because some characters are reserved in HTML.

```html
<h2>The greater-than sign: &gt;</h2>
```

### 2. What are the different new form element types in HTML 5?

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

| Block                                                                                                                                                                                                                                                                     | Inline                                                                                                                                                                                                                                                                                        |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| A block-level element is drawn as a block that stretches to fill the full width available to it i.e, the width of its container and will always start on a new line. <br/>Elements that are block-level by default: <br/> `html <div>, <img>, <section>, <form>, <nav> `. | Inline elements are drawn where they are defined and only take up space that is absolutely needed. The easiest way to understand how they work is to look at how text flows on a page. <br/>Examples of elements that are inline by default: <br/>`html <span>, <b>, <strong>, <a>, <input>`. |

### 5. What is semantic HTML?

Semantic HTML is a coding style. It is the use of HTML markup to reinforce the semantics or meaning of the content. For example: In semantic HTML
`html <b> </b>` tag is not used for bold statement as well as `html <i> </i>` tag is used for italic. Instead of these we use `html <strong></strong>` and `html<em></em>` tags.

### 6. Explain The Key Differences Between LocalStorage And SessionStorage Objects.

The key differences between localStorage and sessionStorage objects are as follows:

- The localStorage object stores the data without an expiry date. However, sessionStorage object stores the data for only one session.
- In the case of a localStorage object, data will not delete when the browser window closes. However, the data gets deleted if the browser window closes, in the case of sessionStorage objects.
- The data in sessionStorage is accessible only in the current window of the browser. But, the data in the localStorage can be shared between multiple windows of the browser.

<h2 align="center">
 CSS
</h2>

## Basics

### 1. What is the Box model in CSS? Which CSS properties are a part of it?

A rectangle box is wrapped around every HTML element. The box model is used to determine the height and width of the rectangular box. The CSS Box consists of Width and height (or in the absence of that, default values and the content inside), padding, borders, margin.

![image](https://user-images.githubusercontent.com/6243528/187034617-878f36b5-4cca-4bfe-a601-ae22d79540db.png)

- Content: Actual Content of the box where the text or image is placed.
- Padding: Area surrounding the content (Space between the border and content).
- Border: Area surrounding the padding.
- Margin: Area surrounding the border.

### 2. What are the different types of Selectors in CSS?

A CSS selector is the part of a CSS ruleset that actually selects the content you want to style. Different types of selectors are listed below.

<b>Universal Selector</b>: The universal selector works like a wildcard character, selecting all elements on a page. In the given example, the provided styles will get applied to all the elements on the page.

```css
* {
  color: 'green';
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

<b>Class Selector</b>: The class selector also matches all elements on the page that have their class attribute set to the same value as the class. In the given example, the provided styles will get applied to all the elements having ID as the box on the page.

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

In this example, all paragraph elements (`<p>`) will be styled with the specified rules, but only if they are siblings of `<h2>` elements. There could be other elements in between the `<h2>` and `<p>`, and the styles would still apply.

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

- Style an element when a user mouses over it
- Style visited and unvisited links differently
- Style an element when it gets focus

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

<b>Block Element</b>: The block elements always start on a new line. They will also take space for an entire row or width. List of block elements are `<div>, <p>`.

<b>Inline Elements<b>: Inline elements don't start on a new line, they appear on the same line as the content and tags beside them. Some examples of inline elements are `<a>, <span> , <strong>,` and ``<img>` tags.

<b>Inline Block Elements</b>: Inline-block elements are similar to inline elements, except they can have padding and margins and set height and width values.

### 5. How is border-box different from content-box?

`content-box` is the default value box-sizing property. The height and the width properties consist only of the content by excluding the border and padding. Consider an example as shown:

```css
div {
  width: 300px;
  height: 200px;
  padding: 15px;
  border: 5px solid grey;
  margin: 30px;
  -moz-box-sizing: content-box;
  -webkit-box-sizing: content-box;
  box-sizing: content-box;
}
```

Here, the box-sizing for the div element is given as content-box. That means, the height and width considered for the div content exclude the padding and border. We will get full height and width parameters specified for the content as shown in the below image.

![image](https://user-images.githubusercontent.com/6243528/187038330-65a49fdd-fbe3-404e-bb41-971d95e59ddf.png)

The border-box property includes the content, padding and border in the height and width properties. Consider an example as shown:

```css
div {
  width: 300px;
  height: 200px;
  padding: 15px;
  border: 5px solid grey;
  margin: 30px;
  -moz-box-sizing: border-box;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
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

- <b>Centering with Table</b>:
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
  width: 200px;
  height: 200px;
}
```

- <b>Centering with Transform</b>
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
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 200px;
  height: 200px;
}
```

- <b>Centering with Flexbox</b>
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

- <b>Centering with Grid</b>
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
<div
  class='wrapper'
  > <div
  > One</div
  > <div
  > Two</div
  > <div
  > Three</div
  > <div
  > Four</div
  > <div
  > Five</div
  > </div
  > .wrapper {
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
<div
  class='wrapper'
  > <div
  > One</div
  > <div
  > Two</div
  > <div
  > Three</div
  > <div
  > Four</div
  > <div
  > Five</div
  > </div
  > .wrapper {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
}
```

![image](https://user-images.githubusercontent.com/6243528/187037953-e12c0dee-f185-4ed7-8fd8-07155d57aff1.png)

A simple question to ask yourself when deciding between grid or flexbox is:

do I only need to control the layout by row or column – use a flexbox
do I need to control the layout by row and column – use a grid

### 5. What is specificity? How to calculate specificity?

A process of determining which CSS rule will be applied to an element. It actually determines which rules will take precedence. Inline style usually wins then ID then the class value (or pseudo-class or attribute selector), the universal selector (\*) has no specificity. ID selectors have a higher specificity than attribute selectors.

### 6. What is progressive rendering? How do you implement progressive rendering in the website?. What are the advantages of it?

Progressive rendering is the name given to techniques used to improve the performance of a webpage (in particular, improve perceived load time) to render content for display as quickly as possible.

We can implement the progressive rendering of the page by loading the lazy loading of the images. We can use Intersection Observer API to lazy load the image. The API makes it simple to detect when an element enters the viewport and take an action when it does. Once the image enters the viewport, we will start loading the images.

A sample snippet is given below.

```css
<img class="lazy"
src="placeholder-image.jpg"
data-src="image-to-lazy-load-1x.jpg"
data-srcset="image-to-lazy-load-2x.jpg 2x, image-to-lazy-load-1x.jpg 1x"
alt="I'm an image!">
```

```javascript
document.addEventListener('DOMContentLoaded', function () {
  var lazyImages = [].slice.call(document.querySelectorAll('img.lazy'));

  if ('IntersectionObserver' in window) {
    let lazyImageObserver = new IntersectionObserver(function (
      entries,
      observer
    ) {
      entries.forEach(function (entry) {
        if (entry.isIntersecting) {
          let lazyImage = entry.target;
          lazyImage.src = lazyImage.dataset.src;
          lazyImage.srcset = lazyImage.dataset.srcset;
          lazyImage.classList.remove('lazy');
          lazyImageObserver.unobserve(lazyImage);
        }
      });
    });

    lazyImages.forEach(function (lazyImage) {
      lazyImageObserver.observe(lazyImage);
    });
  } else {
    // Possibly fall back to event handlers here
  }
});
```

Credit goes to https://github.com/sudheerj and Myself :)
