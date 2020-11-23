---
title: "Express Notes"
date: 2020-06-04
categories: Express
permalink: /:categories/:title
---

Express is a powerful but flexible Javascript framework for creating web servers and APIs. It can be used for everything from simple static file servers to JSON APIs to full production servers.

## Concepts

**REST**

- separate server and client
- server side is stateless, not knowing the state on client side
- requesting data from server by client:

  - an HTTP verb, which defines what kind of operation to perform
    - GET
    - POST, used for creating new resources.
    - PUT, used for updating existing resources.
    - DELETE, used to delete resources.
  - a header, which allows the client to pass along information about the request. Usually the client sends the type of conetent that it is able to receive from the server.

    - `Accept` field with MIME Types

    ```JavaScript
    GET /articles/23
    Accept: text/html, application/xhtml
    ```

    - commonly used subtypes:
      - image — image/png, image/jpeg, image/gif
      - audio — audio/wav, image/mpeg
      - video — video/mp4, video/ogg
      - application — application/json, application/pdf, application/xml, application/octet-stream

  - a path to a resource

  ```JavaScript
  GET fashionboutique.com/customers/:id
  ```

  - an optional message body containing data

- sending responses from server to client

```JavaScript
// response header
HTTP/1.1 200 (OK)
Content-Type: text/html

// response codes
GET — return 200 (OK)
POST — return 201 (CREATED)
PUT — return 200 (OK)
DELETE — return 204 (NO CONTENT) If the operation fails, return the most specific status code possible corresponding to the problem that was encountered.
```

**express** node module

- `.listen()` on the specified port and respond to any requests that come into it.

```JavaScript
// Import the express library here
const express = require('express');
// Instantiate the app here
const app = express();

const PORT = process.env.PORT || 4001;

// Invoke the app's `.listen()` method below:
app.listen(PORT, () => {console.log("The server is listening for requests")});
```

- `.get()` to register routes to match `GET` request

```JavaScript
app.get('/expressions/:id', (req, res, next) => {
  const foundExpression = getElementById(req.params.id, expressions);
  if (foundExpression) {
    res.send(foundExpression);
  } else {
    res.status(404).send();
  }
});
```

- `.put()`

```JavaScript
const monsters = { '1': { name: 'cerberus', age: '4'  } };
// PUT /monsters/1?name=chimera&age=1
app.put('/monsters/:id', (req, res, next) => {
  // save what is query to monsterUpdates
  const monsterUpdates = req.query;
  // match with data with that property
  monsters[req.params.id] = monsterUpdates;
  // send response back
  res.send(monsters[req.params.id]);
});
```

- `.post()`

```JavaScript
// POST example 1
app.post('/expressions', (req, res, next) => {
  const receivedExpression = createElement('expressions', req.query);
  if (receivedExpression) {
    expressions.push(receivedExpression);
    res.status(201).send(receivedExpression);
  } else {
    res.status(400).send();
  }
});
```

```JavaScript
// POST example 2
app.post('/soups', (req, res, next) => {
  const name = req.query.name
  soups.push(name);
  res.status(201).send(name);
})
```

- `.delete()`

```JavaScript
// DELETE example 1
app.delete('/expressions/:id', (req, res, next) => {
  const expressionIndex = getIndexById(req.params.id, expressions);
  if (expressionIndex !== -1) {
    expressions.splice(expressionIndex, 1);
    res.status(204).send();
  } else {
    res.status(404).send();
  }
});
```

```JavaScript
// DELETE example 2
app.delete('/puddings/:flavor', (req, res, next) => {
  const index = findPuddingIndex(req.params.flavor);
  if(index !== -1){
    deletePuddingAtIndex(index);
    res.status(204).send();
  } else {
    res.status(404).send();
  }
})

```

**response**

- `.send()` will take any input and include it in the response body.

* `.status`

```JavaScript
const express = require('express');
const app = express();

// Serves Express Yourself website
app.use(express.static('public'));

const { getElementById, seedElements } = require('./utils');

const expressions = [];
seedElements(expressions, 'expressions');

const PORT = process.env.PORT || 4001;
// Use static server to serve the Express Yourself Website
app.use(express.static('public'));

app.get('/expressions', (req, res, next) => {
  res.send(expressions);
});

app.get('/expressions/:id', (req, res, next) => {
  const foundExpression = getElementById(req.params.id, expressions);
  if (foundExpression) {
    res.send(foundExpression);
  } else {
    res.status(404).send();
  }
});

app.listen(PORT, () => {
  console.log(`Listening on port ${PORT}`);
});
```

**Route parameters**

Parameters are route path segments that begin with `:` in their Express route definitions. They act as wildcards, matching any text at that path segment.

```JavaScript
const monsters = { hydra: { height: 3, age: 4 }, dragon: { height: 200, age: 350 } };
// GET /monsters/hydra
app.get('/monsters/:name', (req, res, next) => {
  console.log(req.params) // { name: 'hydra' };
  res.send(monsters[req.params.name]);
});
```

**Status Codes**

**Routes**

```JavaScript
const expressionsRouter = express.Router();
app.use('/expressions', expressionsRouter);

// Get all expressions
expressionsRouter.get('/', (req, res, next) => {
  res.send(expressions);
});
```

**Middleware**

Middleware is code that executes between a server receiving a request and sending a response. It operates on the boundary, so to speak, between those two HTTP actions.

An Express middleware is a function with three parameters: (req, res, next). The sequence is expressed by a set of callback functions invoked progressively after each middleware performs its purpose. The third argument to a middleware function, next, should get explicitly called as the last part of the middleware’s body. This will hand off the processing of the request and the construction of the response to the next middleware in the stack.

- `app.use()`  
  “argument: path

description: The path for which the middleware function is invoked; can be any of:

A string representing a path.
A path pattern.
A regular expression pattern to match paths.
An array of combinations of any of the above. “

**morgan** library  
an open-source library for logging information about the HTTP request-response cycle in a server application. morgan() is a function that will return a middleware function, to reiterate: the return value of morgan() will be a function, that function will have the function signature (req, res, next) that can be inserted into an app.use(), and that function will be called before all following middleware functions. Morgan takes an argument to describe the formatting of the logging output. For example, morgan('tiny') will return a middleware function that does a “tiny” amount of logging. With morgan in place, we’ll be able to remove the existing logging code. Once we see how fast it is to add logging with morgan, we won’t have to spend time in the future trying to figure out how to replicate that functionality.

**error handling**

**router.param**

## Terms

- CRUD: Create, Read, Update, and Delete (CRUD) are the four basic functions that models should be able to do, at most.
- MIME: Multipurpose Internet Mail Extensions
- REST: REST, or REpresentational State Transfer, is an architectural style for providing standards between computer systems on the web, making it easier for systems to communicate with each other. REST-compliant systems, often called RESTful systems, are characterized by how they are stateless and separate the concerns of client and server. We will go into what these terms mean and why they are beneficial characteristics for services on the Web.
- routes: Routes define the control flow for requests based on the request’s path and HTTP verb.
