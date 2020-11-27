---
title: "NodeJS Notes"
date: 2020-06-03
categories: NodeJS
---

<!--excerpt.start-->Node is often described as having event-driven architecture.<!--excerpt.end-->

## Concepts

**Process Object**  
 Node has a global `process` object, with useful methods and information about the current process.

- `process.env` property  
  is an objects which stores and controls information about the environment in which the process is currently runnings.

```JavaScript
// PWD property
process.env.PWD

// adding NODE_ENV with either "production" or "development" to perform different tasks
if (process.env.NODE_ENV === 'development'){
  console.log('Testing! Testing! Does everything work?');
}
```

- `process.memoryUsage()`

```JavaScript
// process.memoryUsage()
{ rss: 26247168,
  heapTotal: 5767168,
  heapUsed: 3573032,
  external: 8772 }
```

- `process.argv` property  
  returns an array containing the command line arguments passed when the Node.js process was launched.

```JavaScript
node myProgram.js testing several features
arg[0] arg[1]     arg[2]  arg[3]  arg[4]
```

- `process.stdout.write()` to handle outputs.

```JavaScript
// console.log()
process.stdout.write("I'm thinking of a number from 1 through 10. What do you think it is? \n(Write \"quit\" to give up.)\n\nIs the number ... ");
```

- `process.stdin.on()` is an instance of EventEmitter, to handle inputs.

```JavaScript
// 'data' is the name of an event
process.stdin.on('data', (userInput) => {
  let input = userInput.toString()
  console.log(input)
});
```

**Core Modules**

- Location: `lib/` folder
- `Require` code snippet

```JavaScript
// Require in the 'events' core module:
let events = require('events');
```

- common core modules:

  - events
  - fs
  - readline
  - http

  **fs**

  - `fs.readFile()` to read ALL data from a provided file.

  ```JavaScript
  //fs.readFile()
  const fs = require('fs');

  // error handling
  let readDataCallback = (err, data) => {
    if (err) {
      console.log(`Something went wrong: ${err}`);
    } else {
      console.log(`Provided file contained: ${data}`);
    }
  };

  // fs.readFile(<arg1:fileName>, <arg2:file char encoding>, <arg3:callback func when the async task of reading is complete.>)
  fs.readFile('./file.txt', 'utf-8', readDataCallback);
  ```

  - `fs.createReadSteam()`
  - `fs.createWriteStream()`

  ```JavaScript
  // write stream
  const readline = require('readline');
  const fs = require('fs');

  // read line-by-line
  const myInterface = readline.createInterface({
    input: fs.createReadStream('shoppingList.txt')
  });

  // define file to write to
  const fileStream = fs.createWriteStream('shoppingResults.txt');

  // EventEmitter
  let transformData = (line) => {
  fileStream.write(`They were out of: ${line}\n`);
  };

  myInterface.on('line', transformData);
  ```

  **readline** to read files line-by-line

  - `readline.createInterface()` returns an EventEmitter set up to emit `'line'`events

  ```JavaScript
  // read stream
  const readline = require('readline');
  const fs = require('fs');

  // call fs.createReadStream on 'shppingList.txt' to create a stream;
  // assgin as key of the 'input' property of the 'settings' object
  let settings = {
    input: fs.createReadStream('shoppingList.txt')
  };

  // assign myInterface the returned value from invoking readline.createInterface() with an object containing our designated settings
  const myInterface = readline.createInterface(settings);

  const printData = (data) => {
    console.log(`Item: ${data}`);
  };

  myInterface.on('line', printData);
  ```

  **http**

  - `http.createServer()` returns an instance of an `http.server`
    - `.listen()` causes the server to “listen” for incoming connections.

  ```JavaScript
  const http = require('http');

  let requestListener = (request, response) => {
    response.writeHead(200, {'Content-Type': 'text/plain' });
    response.write('Hello World!\n');
    response.end();
  };

  // create a http.server object named 'server' by calling 'http.createServer()' func; pass  a callback function 'requestListener' as para
  const server = http.createServer(requestListener);

  server.listen(3000);
  ```

**Local Modules**

- Location: a used defined location
- `Require` code snippet

```JavaScript
 // dog.js where local module is defined
module.exports = class Dog {

  constructor(name) {
    this.name = name;
  }

  praise() {
    return `Good dog, ${this.name}!`;
  }
};

// app.js where local module is required and used
let Dog = require('./dog.js');
const tadpole = new Dog('Tadpole');
console.log(tadpole.praise());
```

**EventEmitter** class

```JavaScript
// Require in the 'events' core module
let events = require('events');

// Create an instance of the EventEmitter class
let myEmitter = new events.EventEmitter();

// Here we create an instance of the EventEmitter class
let myEmitter = new events.EventEmitter();

// Here we subscribe to 'celebration' events and provide a callback function which will be passed the event's data
// last to execute
myEmitter.on('celebration', listenerCallback);

// Here we emit an event, we pass the event type, 'celebration', as the first argument, and the event data as the second
// first to execute
myEmitter.emit('celebration', 'good times, come on!');
```

**Errors**

- Using _error-first callback functions_ to handle errors.

```JavaScript
// An error-first callback function.
// error as the first sexpected arg
// only if error is false, then else statement will execute
const api = require('./api.js');

// An error-first callback
let errorFirstCallback = (err, data) => {
  if (err) {
    console.log(`Something went wrong. ${err}\n`);
  } else {
    console.log(`Something went right. Data: ${data}\n`);
  }
};

api.errorProneAsyncApi("problematic input", errorFirstCallback);
```

- Using `try...catch`` to handle errors.

```JavaScript
const api = require('./api.js');

let callbackFunc = (data) => {
   console.log(`Something went right. Data: ${data}\n`);
};

// a try...catch
try {
  api.naiveErrorProneAsyncFunction('problematic input', callbackFunc);
} catch(err) {
  console.log(`Something went wrong. ${err}\n`);
}
```

**event loop**

**npm**

- react
- express
- nodemon

Node APIs  
`setInterval()`  
`util.promisify`

## Terms

- REPL: REPL is an abbreviation for read–eval–print loop. It’s a program that loops, or repeatedly cycles, through three different states: a read state where the program reads input from a user, the eval state where the program evaluates the user’s input, and the print state where the program prints out its evaluation to a console. Then it loops through these states again.

- REST: REST, or REpresentational State Transfer, is an architectural style for providing standards between computer systems on the web, making it easier for systems to communicate with each other. REST-compliant systems, often called RESTful systems, are characterized by how they are stateless and separate the concerns of client and server. We will go into what these terms mean and why they are beneficial characteristics for services on the Web.
