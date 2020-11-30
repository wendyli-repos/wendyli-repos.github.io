---
title: "JavaScript Notes 01 - "
date: 2020-06-01
categories: Javascript
---
<!--excerpt.start-->Javascript is probably the origin of Web Development. Here are some notes of JavaScript. <!--excerpt.end-->

2. typeof <variablename>




# Concepts:

1.	const vs let. 一旦一个 variable 用 const 定义后，这个 variable 就不能被赋予其他值或类型。但是可以对 const 进行修改、添加等操作。
2.	let 定义的 variable 可以被赋值为其他变量。
3.	Primitives/Value Types
	- String
	- Number
	- Boolean
	- undefiend
	- null
4.  References Types
	- Array

Objects Notes:

1. factory fucntion to create object
2. every object has a construtor property that refers to the function used to create that object.
3. call()
4. apply()
5. primitive vs object type
6. object is not iterable
7. for in for object properties
8. for of iterable like array or

9. object constructor function 中的 this 指代创建的空 object{}，然后再把 function 里面的 parameter 赋值到空 array 里面给 function 的
   parameter 的存储位置，因此出现 this.title = title; this.name = name; etc.

Array Notes:

1. valid array defination:
   const numbers = [1, 2, 3, 5, { name: "s" }];
2. map method
3. splice method
4. pop, push
5. shift, unshift
6. reduce (an arrow function)

Function Notes:

1. function declaration, no';" at the end
   function walk() {
   consoloe.log('walk');
   }
2. function expression
   let run = function walk()
   {
   console.log('run');
   };
3. hoisting
   can call function b4 it is created using function declaration method
4. the rest operator ...args
5. getters and setters
   getter => access properties
   setter => change (mutate) them
6. change 'this' using _.call();
   _.apply();
   \*.bind();
   or using arrow function which inherates the upper
7. callback function

OOP Notes:

1.  prototypical inheritance. protytpe is namely parent.
2.  2 methods to rewrite prototype inhertance relation
    Method 1: intermediate function inhertance
    function extend(Child, Parent) {
    Child.prototype = Object.create(Parent.prototype); // line 1
    Child.prototype.constructor = Child; // line 2
    }
    extend(Circle, Shape);

    Method 2 :
    rewrite line 1 & 2 for each inherated object.

    Circle.prototype = Object.create(Shape.prototype);
    Circle.prototype.constructor = Circle;

    Square.prototype = Object.create(Shaoe.prototype);
    Square.prototype.constructor = Square;

3.  methold overwriting
    duplicate() is inheratated from Shape object, but I'd like to rewrite this menthod's implementation in Circle object.
    Circle.prototype.duplicate = function() {
    /// new function implementation
    }
4.  polymorphism means one method that is inherated from the baseObject can have multiple implementation in different objects.
    if you create an array with different objects inheratated fron the object base, then you can call this method directky as a menthod of the objectBase.
5.  composition mixins, namely create different objects then combine them as requested
6.  inheritance
    // inheritance only prototype methods
    HtmlSelectElememt.prototype = Object.create(HtmlElement.prototype);

// inheritance the entire parent object
HtmlSelectElememt.prototype = new HtmlElement();

7. constructor also has prototype proterity which is the prototype that used to create that Object.
8. instance members VS prototype members
   define prototype members:
   Circle.prototype.draw = function() {
   console.log('draw');
   }
9. iterating instance and prototype members
   Object.keys(c1); // can iterate all instance members

   for (let key in c1) console.log(key); // can iterate all members (including instance and prototype members)

   c1. hasOwnProperty('any instance members'); // will return true is parameter is any instance members.
   // In JS, instance members are usually referred as own property

10. super constructor to inherate prototype's property

ES6 class Notes;

1. class expression is not hoisted. Must declare class before.
   // class expression
   const Square = class {};
   // class declaration, use this method to define class
   class Circle {}
2. instace method vs static method
   instance method is availiale on the object
   static parse(str) {} to create utility functions that are not tight to one object but the class itslef.
3. this keyword - 'use strict' to prevent from modify window object.
   const Circle = function() {
   this.draw = function() {
   console.log(this);
   };
   };

const c = new Circle();
// method call
c.draw();

const draw = c.draw;
console.log(draw);
// function call, stand along function, which is not part of an object
draw();

// the body of the class is using 'strict' mode
class Circle {
draw() {
console.log(this);
}
}

const c = new Circle();
const draw = c.draw;
draw();

4. Private members using Symbol() three different approaches.
   1st: using Symbol()
   2nd: WeakMap()
5. inheritance

ES tools Notes:

1. module formats
   // AMD - brower application
   CommonJS - Node.js
   // UMD - Brower/ Node.js
   ES6 Modules

- **ES6 Class**

```JavaScript
class Circle {
  constructor(radius) {
    this.radius = radius;
    this.move = function() {}  // this method will NOT be included in the __proto__ of "c", but as a method of the instance "c"
  }

  draw() {  // this method will be included in the __proto__ of "c"
    console.log("draw");
  }
}
// create a Circle object named "c"
const c = new Circle(1);

//refactoring using prototypical inhertance//
function Circle(radius) {
  this.radius = radius;
  this.move = function() {};
}

Circle≥prototype.draw = function() {
  console.log("draw");
}
```

Not hosted

```JavaScript
// Class Declaration, preferred
class Circle {

}

// Class Expression
const Square = class {};
```

Instance methods VS static methods

```JavaScript
class Circle {
  constructor(radius) {
    this.radius = radius;
    this.move = function() {}
  }

// instance method
  draw() {
    console.log("draw");
  }

// static method, only avaiable for the Circle class, to create utility functions that are not tied to a particular object
static parse(str) {
  const radius = JSON.parse(str).radius;
  return new Circle(radius);
}
}

const c_static = Circle.parse("{"radius":1});

const c = new Circle(1);
c.draw();
```

strict mode

```JavaScript
'use strict';
```

private members using `Symbol()`

```JavaScript
const _radius = Symbol();
```

private members using `WeakMap()`

```JavaScript
const -radius = new WeakMap();

class Circle {
  constructor(radius) {
    _radius.set(this,radius);
  }
}

const c - new Circle(1);
```

private members using `Class Fields`

```JavaScript
class SmallRectangle {
  #width = 20;
  #height = 10;

  get dimension() {
    return {width: this.#width, height: this.#height};
  }
  increaseSize() {
    this.#width++;
    this.#height++;
  }
}
const rectangle = new SmallRectangle();
console.log(rectangle.dimension);    // => {width: 20, height: 10}
rectangle.#width = 0;       // => SyntaxError
rrectangle.#height = 50;    // => SyntaxError
```

getters and setters  
inheritance

```JavaScript
class Animal {
  constructor(name) {
    this._name = name;
    this._behavior = 0; // any properties have default values do not need a constructor
  }

  get name() {
    return this._name;
  }

  get behavior() {
    return this._behavior;
  }

  incrementBehavior() {
    this._behavior++;
  }
}

class Cat extends Animal {
  constructor(name, usesLitter) {
    super(name); // super(any properties will be reused in Cat object that inhertants from the Animal class)
    this._usesLitter = usesLitter;
  }
}
```

static method

```JavaScript
class Animal {
  constructor(name) {
    this._name = name;
    this._behavior = 0;
  }

// generateName() can only be accseed inside Animal class
  static generateName() {
    const names = ['Angel', 'Spike', 'Buffy', 'Willow', 'Tara'];
    const randomNumber = Math.floor(Math.random()*5);
    return names[randomNumber];
  }
}
```

- **regex expression**

```JavaScript
/access_token=([^&]*)/
/expires_in=([^&]*)/
```

- **return**  
  The return statement ends function execution and specifies a value to be returned to the function caller.

- **Asynchronous JavaScript and XML (AJAX)**  
  XMLHttpRequest (XHR) API named for XML, can be used to make many kinds of requests and supports other forms of data.

```JavaScript
// XHR GET request
// the boilerplate code for an AJAX GET request using an XMLHttpRequest object.
// creates new xhr object
const xhr = new XMLHttpRequest();
const url = "http://api-to-call.com/endpoint";

// handles response
xhr.responseType = "json";
xhr.onreadystatechange = () => {
  //The purpose of this conditional statement checks to see if the request has finished.
  if (xhr.readyState === XMLHttpRequest.DONE) {
    // Code to execute with response
  }
};

// opens requests and sends object
// .open() creates a new request and the arguments passed in determine the type and URL of the request.
xhr.open("GET), url);
xhr.send();
```

```JavaScript
// AJAX function
const getSuggestions = () => {
  const wordQuery = inputField.value;
  const endpoint = `${url}${queryParams}${wordQuery}`;
  const xhr = new XMLHttpRequest();
  xhr.responseType = "json";
  xhr.onreadystatechange = () => {
    if (xhr.readyState === XMLHttpRequest.DONE) {
      renderResponse(xhr.response);
    }
  };
  xhr.open("GET", endpoint);
  xhr.send();
}
```

query string `&topics="`

- **Promise**  
   Promises are objects that represent the eventual outcome of an asynchronous operation.
  Three states:
  - `Pending`: The initial state — the operation has not completed yet.
  - `Fulfilled`: The operation has completed successfully and the promise now has a resolved value. For example, a request’s promise might resolve with a JSON object as its value.
  - `Rejected`: The operation has failed and the promise has a reason for the failure. This reason is usually an Error of some kind.
    A Promise’s constructor has a single parameter, called the “executor function”. The executor function has two parameters – resolve and reject.

A promise is _settled_ if it is no longer pending.

Promise objects come with an aptly named `.then()` method.

- **setTimeout()**  
  setTimeout() is a Node API (a comparable API is provided by web browsers) that uses callback functions to schedule tasks to be performed after a delay.

  setTimeout(() => {
  <code to execute>;
  }, <waiting time>);

  setTimeout() has two parameters: a callback function and a delay in milliseconds.

  - Using `setTimeout()` to construct asynchronous promises

```JavaScript
const returnPromiseFunction = () => {
  return new Promise((resolve, reject) => {
    setTimeout(() => {resolve('I resolved!')}, 1000);
  });
};

const prom = returnPromiseFunction();
```

- **promise.then()**
  > Returns a Promise
  > promise1.then(<callback function for the success>, <failure case of the promise>)
  > .then() is a higher-order function— it takes two callback functions as arguments. We refer to these callbacks as handlers. When the promise settles, the appropriate handler will be invoked with that settled value.

The first handler, sometimes called `onFulfilled`, is a success handler, and it should contain the logic for the promise resolving.
The second handler, sometimes called `onRejected`, is a failure handler, and it should contain the logic for the promise rejecting.  
We can invoke .then() with one, both, or neither handler!

```JavaScript
let prom = new Promise((resolve, reject) => {
  let num = Math.random();
  if (num < .5 ){
    resolve('Yay!');
  } else {
    reject('Ohhh noooo!');
  }
});

const handleSuccess = (resolvedValue) => {
  console.log(resolvedValue);
};

const handleFailure = (rejectionReason) => {
  console.log(rejectionReason);
};

prom.then(handleSuccess, handleFailure);
```

- **promise.catch()**  
  The .catch() function takes only one argument, onRejected.

```JavaScript
  prom
  .then((resolvedValue) => {
    console.log(resolvedValue);
  })
  .then(null, (rejectionReason) => {
    console.log(rejectionReason);
  });
```

- **Chaining Multiple Promises**

```JavaScript
// chaining up .then() after promise not nesting inside one then() funcrion
// remember 'return' keyword
firstPromiseFunction()
.then((firstResolveVal) => {
  return secondPromiseFunction(firstResolveVal);
})
.then((secondResolveVal) => {
  console.log(secondResolveVal);
});
```

- **promise.all()**  
  Promise.all() accepts an array of promises as its argument and returns a single promise.  
  That single promise will settle in one of two ways:

If every promise in the argument array resolves, the single promise returned from Promise.all() will resolve with an array containing the resolve value from each promise in the argument array.
If any promise from the argument array rejects, the single promise returned from Promise.all() will immediately reject with the reason that promise rejected. This behavior is sometimes referred to as failing fast.

- **promise.finally()**

- **event loop**

- **fetch API**  
  fetch() is a web API that can be used to create requests. fetch() will return promises.

We can chain .then() methods to handle promises returned by fetch().

The .json() method converts a returned promise to a JSON object.

```JavaScript
// fetch GET
// fetch() itself is a function already writtern in JS, return a promise so we can chain it up using then()
fetch("http://api-to-call.com/endpoint").then(response => {
  if (response.ok) {
// Takes a Response stream and reads it to completion. It returns a promise that resolves with the result of parsing the body text as JSON
    return response.json();
  }
  throw new Error("Request failed!");
}, networkError => console.log(networkError.message)
). then(jsonResponse => {
  /// Code to execute with jsonResponse
});
```

```JavaScript
// fetch POST
// fetch() takes two args
// fetch(<endpoint>, <an object that containes info needed for the POST request>)
// This second argument determines that this request is a POST request and what information will be sent to the API.
fetch("http://api-to-call.com/endpoint", {
  method: "POST",
  body: JSON.stringify( {id: '200'})
}).then(response => {
  if (response.ok) {
// Takes a Response stream and reads it to completion. It returns a promise that resolves with the result of parsing the body text as JSON
    return response.json();
  }
  throw new Error("Request failed!");
}, networkError => console.log(networkError.message)
). then(jsonResponse => {
  /// Code to execute with jsonResponse
});
```

- **async await GET**  
  async is a keyword that is used to create functions that will return promises.
  await is a keyword that is used to tell a program to continue moving through the message queue while a promise resolves.
  await can only be used within functions declared with async.

`````JavaScript
// async await GET
async function getData() {
  // The code in the try block will send a request and handle the response.
  try {
    const response = await fetch("https://api-to-call.com/endpoint");
    if (response.ok) {
      const jsonResponse = await response.json();
      // Code to execute with jsonResponse
    }
    throw new Error("Request failed!");
  }
  // The catch statement will then take care of an error if it is thrown.
  catch(error) {
    console.log(error);
  }
}

````JavaScript
// async await POST
async function getData() {
  // The code in the try block will send a request and handle the response.
  try {
    const response = await fetch("https://api-to-call.com/endpoint", {
      method: "POST",
      body: JSON.stringify( {id: '200'})
    });
    if (response.ok) {
      const jsonResponse = await response.json();
      // Code to execute with jsonResponse
    }
    throw new Error("Request failed!");
  }
  // The catch statement will then take care of an error if it is thrown.
  catch(error) {
    console.log(error);
  }
}
`````

## DOM

- window.location.href  
  To get URL of a webpage

- window.history.pushState

- JSON.stingify
  The JSON.stringify() method converts a JavaScript object or value to a JSON string, optionally replacing values if a replacer function is specified or optionally including only the specified properties if a replacer array is specified.

  - http get request end point

- **JSON**  
  JSON, JavaScript Object Notation

- **TCP(Transmission Control Protocol)**  
  TCP is the channel and HTTP is the command transferring from client to server for data or vice versa.
- **HTTP(Hypertext Transfer Protocol) METHODS**
  - GET  
    Retrieves data from the server  
    Make requests using JavaScript’s **XHR** object  
    Incorporate query strings into our requests
  - POST  
    The major difference between a GET request and POST request is that a POST request requires additional information to be sent through the request. This additional information is sent in the body of the post request.
    Submit data to the server

```JavaScript
const xhr = new XMLHttpRequest();
const url = "http://api-to-call.com/endpoint";
// converts data to a string
// JSON.stringify() will convert a value to a JSON string. By converting the value to a string, we can then send the data to a server.
// check if must use single quote for id value?????
const data = JSON.stringify( {id: "200"});

// to define the response type to be json
xhr.responseType = "JSON";

// what will happen during the change
xhr.onreadystatechange = () => {
  // xhr object has a property readystate which has four states:
  // UNSENT
  // OPENED
  // HEADERS_RECEIVED
  // LOADING
  // DONE, the operation is complete
  if (xhr.readystate === XMLHttpRequest.DONE) {
    // code to execute with response
  }
};

// initializes a request
xhr.open("POST", url);

// pass data then data will be sent to the server
xhr.send(data);
```

- PUT
- DELETE
- **HTTP HEADER FIELDS**
- **HTTP STATUS CODE**
  1XX
  2XX
  3XX
  4XX
  5XX
- **HTTP/2**

- **HTTP BODY FIELDS**

- **APIs**
- Datamuse API
  concate sections of `endpoint` according to the API request
  > https://api.datamuse.com/words?rel_jjb=notebook&topics=stationary
  > const url = 'https://api.datamuse.com/words?';
  > const queryParams = 'rel_jjb=';
  > const additionalParams = "&topics=";
  > const wordQuery = inputField.value;
  > const topicQuery = topicField.value;
  > const endpoint = `${url}${queryParams}${wordQuery}${additionalParams}${topicQuery}`;
- Rebrandly URL Shortener API  
  send a POST request with data (as the long format link) to the API then will return a shortened link format

```

```
