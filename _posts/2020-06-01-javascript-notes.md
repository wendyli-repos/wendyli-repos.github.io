---
title: "JavaScript Notes"
date: 2020-06-01
categories: Javascript
---
Javascript
1. let vs const 
2. typeof <variablename>
	
3. Primitives/Value Types
	String
	Number
	Boolean
	undefiend
	null
4. References Types


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
