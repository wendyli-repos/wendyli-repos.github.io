---
title: "React Notes"
date: 2020-10-24 14:21:03 +1100
categories: React
---

## Browser compatibility

### Concepts

- [caniuse.com](https://caniuse.com/)

- Babel - A JavaScript library to convert ES6 to ES5

### Practices

#### Practice 1

Set up a JavaScript project that transpiles code when run `npm run build` from the **root directory** of a JavaScript project.

1.1. Setup JavaScript project folder structure:

```
project
|_ src
|___ main.js
```

1.2 Run `npm init` in root directory  
1.3 Answer prompts about project information to be saved in a **package.json** file

```json
// prompts examples:
version: (1.0.0)
description: Use Babel to transpile JavaScript ES6 to ES5
entry point: (index.js)
test command:
git repository:
keywords:
author:
license: (ISC)
```

The package.json file includes:

- Metadata — This includes a project title, description, authors, and more.
- A list of node packages required for the project — for `npm` to look inside package.json and downloads the packages in this list if others want to run this project.
- Key-value pairs for command line scripts — You can use npm to run these shorthand scripts to perform some process.

```
// sample package.json file
{
"name": "learning-babel",
"version": "1.0.0",
"description": "Use Babel to transpile JavaScript ES6 to ES5",
"main": "index.js",
"scripts": {
"test": "echo \"Error: no test specified\" && exit 1"
},
"author": "",
"license": "ISC"
}
```

1.4 Updated folder strucure

```
project
|\_ src
|_\_\_ main.js
|_ package.json
```

1.5 Install Babel Node packages locally

```
$ npm install babel-cli -D
$ npm install babel-preset-env -D
```

`npm install` command creates a folder called **node_modules** and copies the package files to it, also installs all of the dependencies for the given package.  
`babel-cli` package includes command line Babel tools.  
`-D` flag instructs npm to add each package to a property called `devDependencies` in **package.json**.
`babel-preset-env` package has the code that maps any JavaScript feature, Es6 and above, to ES5.

1.6 Create **.babelrc**, which includes the version of the source JavaScript code, in root directory and set "preset" value.

```
{
  "presets": ["env"]
}
```

1.7 Specify a script in **package.json** that initiates the ES6+ to ES5 transpilation.

```
...
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1",
  "build": "babel src -d lib"
}
```

`babel` command calls responsible for transpiling code.  
`src` instructs Babel to transpile all JavaScript code inside the **src** directory.  
`-d` instructs Babel to write the transpiled code to a directory.
`lib` indicates Babel writes the transpiled code to a directory called **lib**.

1.8 Run `npm rub build` to transpile.  
Folder strucutre after transpilation.

```
project
|_ lib
|___ main.js
|_ node_modules
|___ .bin
|___ ...
|_ src
|___ main.js
|_ .babelrc
|_ package.json
```

## JSX

### Concepts

- `className` instead of `class`

```JSX
<h1 className="big">Hey</h1>
```

- slef-closing tag must include `/`

```JSX
<br />
```

- JavaScript expressions inside JSX tags

```JSX
const name = "Addition";
ReactDOM.render(
  <h1>`{name} of 2+ 3 is {2 + 3}`</h1>,
  document.getElementById('app')
);
```

- variable attributes

```JSX
const sideLength = "200px";
const panda = (
  <img
    src="images/panda.jpg"
    alt="panda"
    height={sideLength}
    width={sideLength} />
);
```

- event listeners

```
<img onClick={myFunc} />
```

- JSX Conditions: if

```JSX
// if statements - if stays OUTSIDE JSX
import React from 'react';
import ReactDOM from 'react-dom';

let message;

if (user.age >= drinkingAge) {
  message = (
    <h1>
      Hey, check out this alcoholic beverage!
    </h1>
  );
} else {
  message = (
    <h1>
      Hey, check out these earrings I got at Claire's!
    </h1>
  );
}

ReactDOM.render(
  message,
  document.getElementById('app')
);

// Ternary Operator - INSIDE JSX
const headline = (
  <h1>
    { age >= drinkingAge ? 'Buy Drink' : 'Do Teen Stuff' }
  </h1>
);

// using function to render element
class Track extends Component {
    renderAction() {
    if(this.props.isRemoval) {
      return <button className="Track-action">-</button>
    } else {
      return <button className="Track-action">+</button>
    }
  }

  render() {
    return {
      <div>
        {this.renderAction()}
      </div>
    }
  }
}
```

- JSX Conditionals: &&  
  && works best in conditionals that will sometimes do an action, but other times do nothing at all.

```JSX
const tasty = (
  <ul>
    <li>Applesauce</li>
    { !baby && <li>Pizza</li> }
    { age > 15 && <li>Brussels Sprouts</li> }
    { age > 20 && <li>Oysters</li> }
    { age > 25 && <li>Grappa</li> }
  </ul>
);
```

- .map() to create a list of items in React

```JSX
const strings = ['Home', 'Shop', 'About Me'];
const listItems = strings.map(string => <li>{string}</li>);
<ul>{listItems}</ul>
```

Other ways to create a list

```JSX
const liArray = [
  <li>item 1</li>,
  <li>item 2<li>,
  <li>item 3</li>
];
<ul>{liArray}</ul>
```

- keys  
  A key is a JSX attribute. The attribute’s name is key. The attribute’s value should be something unique, similar to an id attribute.

```JSX
import React from 'react';
import ReactDOM from 'react-dom';
const people = ['Rowe', 'Prevost', 'Gare'];
const peopleLis = people.map((person, i) =>
<li key={"person_" + i}>{person}</li>
); // i is the second argurement in the .map() callback function, indicates the index of each element in the array
ReactDOM.render(<ul>{peopleLis}</ul>, document.getElementById("app"));
```

- React.createElement();

```JSX
// JSX code to create React element
const h1 = <h1>Hello world</h1>;

// rewritten without JSX
const h1 = React.createElement(
 "h1",
 null,
 "Hello, world"
);
```

## React

### Setting up

1.1 Install node

```
npm install -g create-react-app
```

1.2 Run `create-react-app` to create a React app

```
npx create-react-app <directory to save this app>
```

1.3 Launch React project

```
cd <directory to save this app>
npm start
```

### Concepts

- **React Element**  
  React element is an object which has 2 properties(actually more but we’re interested in only 2 props now): type(string), props(object).

- **React Component**  
  Components are basically functions! A component takes two optional inputs, `props` and `state`, and outputs HTML and/or other components.

- **this.props**  
  A component’s props is an object. It holds information about that component. `this.props` refers to that storage object.

  A React component should use props to store information that can be changed, but can only be changed by a different component.  
  props should not be changed.

* **this.props.children**  
  Every component’s props object has a property named children.

  this.props.children will return everything in between a component’s opening and closing JSX tags.

* **defaultProps**

```JSX
class Example extends React.Component {
  render() {
    return <h1>{this.props.text}</h1>;
  }
}
// The defaultProps property should be equal to an object
Example.defaultProps = { text: 'yo' };
```

- **this.state**  
  A React component should use state to store information that the component itself can change.
  - initialization state

```JSX
class Example extends React.Component {
  // set initial state inside constructor()
  constructor(props) {
    super(props);
    this.state = { mood: 'decent' };
  }

  render() {
    return (
      <h1>
        I'm feeling {this.state.mood}!
      </h1>
    );
  }
}

<Example />
```

- update state

```JSX
// this.setState() takes an object, and merges that object with the component’s current state.
class Example extends React.Component {
constructor(props) {
  super(props);
  this.state = { weather: 'sunny' };
  this.makeSomeFog = this.makeSomeFog.bind(this);
}

makeSomeFog() {
  this.setState({
    weather: 'foggy'
  });
}}
```

- **Stateless Fucntional Component (SFC)**
  - a plain JavaScript function
  - takes props as an argument
  - returns a react element
  - cannot reach `this.state`
  - cannot use lifecycle hooks
  - ONLY render props based on `props.state`, like `<Button />`
  - file size is small

```JSX
const MyStatelessComponent = props => <div>{props.name}</div>;

// without JSX
const MyStatelessComponent = props => React.createElement('div', null, props.name);
```

```
{
   type: 'div',
   props: {
     children: props.name,
   }
}
```

```JSX
const Button = props => (
  <button className="our_button" onClick={props.onClick}>{props.label}</button>);
```

- **Component class**
  - a JavaScript class, which has `constructor(){}`, initial `state`
  - React to create an instance of it
  - takes props as an argument
  - returns a react element
  - has a `state` and more
  - can use lifecycle hooks
  - whenever to work with state, fetch data,
  - file size is large after build

```JSX
class MyComponentClass extends React.Component {
  render() {
    return <div>{this.props.name}</div>;
  }
}
```

- **Lifecycle hooks**

  - **Constructor()**  
    Assiging `props` to this React.Component subclass; otherwise `props` is `undefined`.

    - Initializing local `state` by assigning an object to `this.state`.
    - Binding event handler methods to an instance.

```JSX
constructor(props) {
  super(props);
  // Don't call this.setState() here!
  this.state = { counter: 0 };
  this.handleClick = this.handleClick.bind(this);
}
```

- **propTypes**  
  propTypes is a property of the class; and propTypes itself is usually an object with key-value pairs
  - prop validation to ensure props are doing what they’re supposed to be doing. If props are missing, or if they’re present but they aren’t what you’re expecting, then a warning will print in the console.
  - Documentation to understand the component class inside

```JSX
// propTypes defination step
// If a component class expects a prop, then component class should have a propType.
// Step 1: Search for a property named propTypes on the instructions object. If there isn’t one, make one! Note to declare it after the close of your component declaration, since it will be a static property.
// Step 2: Add a property to the propTypes object. For each prop that your component class expects to receive, there can be one property on your propTypes object.
// propTypes example in Component Class
import React from 'react';

export class MessageDisplayer extends React.Component {
  render() {
    return <h1>{this.props.message}</h1>;
  }
}

// This propTypes object should have one property for each expected prop:
// React.PropTypes.expected-data-type-goes-here
MessageDisplayer.propTypes = {
  message: React.PropTypes.string.isRequired
};

// propTypes in SFC
const Example = (props) => {
  return <h1>{props.message}</h1>;
}

Example.propTypes = {
  message: React.PropTypes.string.isRequired
};
```

- **React Forms - Handle Inputs**

```JSX
export class Input extends React.Component {
  constructor(props) {
    super(props);
    this.state = { userInput: '' }; // 3. set initial state
    this.handleUserInput = this.handleUserInput.bind(this); // 4. bind this to the class
  }

// 2. eventHandler function
// e.target.value will equal the text in the <input /> field.
  handleUserInput(e) {
    this.setState({userInput: e.target.value});
  }

// 1. onChange={} attribute
// 5. update an Input's value
  render() {
    return (
      <div>
        <input type="text" onChange={this.handleUserInput} value={this.state.userInput} />
        <h1>{this.state.userInput}</h1>
      </div>
    );
  }
}
  ...
```

- **Controlled vs Uncontrolled**
  - An uncontrolled component is a component that maintains its own internal state, by remembering data about itself.
  - A controlled component is a component that does not maintain any internal state. Must be controlled by other components. Get self information through `prop`.
  - Most React componentns are _controlled_.

### Design pattern

- **Container Components**  
   [Container Components](https://medium.com/@learnreact/container-components-c0e67432e005#.gacsoomn1)

  - Container
    - to fetch data using **Lifecycle Hooks** then render the `component`
  - Component
    - to render(present) data (in a format of list, etc) fetched using `render(){}`
    - to set PropTypes and fail loudly

```JSX
// folder structure
components
containers

// naming conventions
component
|--GuineaPigs.js.
container
|-- GuineaPigsContainer.js.
```

- **Naming Convention on eventHandlers**
  - event handler function inside `Component class`

```
  handle<eventName>
  e.g. handleClick() {}, handleHoover() P
```

- prop name on `<button />`, `<input />`etc

```
  on<eventName>
  e.g. onClock={this.handleClick}, onHoover={this.onHoover}
```

- **Stateless child upgrade their stateful parent's state**

```JSX
// 1. define a state-changeing method on the parent component
// 2. pass this method to the child as value of an attribue of the child component
// 3. call this passing method as a prop of the child component as an event listener
// Note that what we pass down is a method. But the parent change state function requires an object. So we need to create a function in the child component
// 4. This new function should take an event object as an argument, extract the name that you want from that event object, and then call the event handler, passing in the extracted name!
// ensure that the child component pass the correct argument to the method passed down
// 5. bind this function to this
// 6. change the event handler from {this.props.onChange} to {this.handleChange}
export class Child extends React.Component {
handleCHange(e) {
  const name = e.target.value;
  this.props.onChange(name);
}

  render() {
    return (
      <div>
        <h1>
          Hey my name is {this.props.name}!
        </h1>
        <select id="great-names" onChange={this.props.onChange}>
          <option value="Frarthur">
            Frarthur
          </option>

          <option value="Gromulus">
            Gromulus
          </option>

          <option value="Thinkpiece">
            Thinkpiece
          </option>
        </select>
      </div>
    );
  }
}
```

- **Child components update sibling components**  
  A child component updates its parent’s state, and the parent passes that state to a sibling component.

- **API**

### Code Snippets

component definations

```JSX
// create a class component then render
import React from 'react';
import ReactDOM from 'react-dom';
class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}
ReactDOM.render(
	<MyComponentClass />,
	document.getElementById('app')
);
```

logic goes inside `render()`

```JSX
// logic and JS expressions
class Random extends React.Component {
  render() {
    // First, some logic that must happen before rendering:
    const n = Math.floor(Math.random() * 10 + 1);
    // Next, a return statement using that logic:
    return <h1>The number is {n}!</h1>;
  }
}
```

conditons

```JSX
// conditions
class TodaysPlan extends React.Component {
  render() {
    let task;
    if (!apocalypse) {
      task = 'learn React.js'
    } else {
      task = 'run around'
    }
    return <h1>Today I am going to {task}!</h1>;
  }
}
// refactoring ????
return <h1>Today I am going to { !apocalypse ? "learn React.js" : "run around"}</h1>;
```

render class dynamically

```JavaScript
// using a class method to check the state of a component then apply different classes
需要实际应该
```

this

```JSX
// this
class IceCreamGuy extends React.Component {
  get food() {
    return 'ice cream';
  }
  render() {
    return <h1>I like {this.food}.</h1>;
  }
}
```

event listener

```JSX
// event listener
class MyClass extends React.Component {
// event fucntion locates inside the component class
  myFunc() {
    alert('Stop it.  Stop hovering.');
  }
  render() {
    return (
      <div onHover={this.myFunc}>
      </div>
    );
  }
}
```

styling

```JSX
// inline style
<h1 style={{ color: 'red' }}>Hello world</h1>
```

```JSX
// style variable
const styles = {
  color: 'darkcyan',
  marginTop: '20', // no 'px' after '20'
  backgroundColor: 'mintcream'
};
// style name are written in camelCase
// style value 'px' is assumed
...
    return (<h1 style={this.styles}>Hello world</h1>);
...
```

```JSX
// export style file
export const styles = {
  fontFamily: fontFamily,
  background: background,
  fontSize:   fontSize,
  padding:    padding,
  color:      color
};

// import style file
import { styles } from "./styles";

const divStyle = {
  background: styles.background,
  height: '100%'
};
...
```

```JavaScript
// className
<button className="btn btn-secondary btn-sm"></button>
```

---

## CSS

```CSS
/* import Google font inside index.css */
/* then change body{font-family}font */
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@600&display=swap");

body{
  font-family: Poppins,
}
```

## bootstrap

```
npm i bootstrap@4.1.1
Note: no need to include --save option as npm automatically adding bootstrap into dependencies
```

## Advanced React Topics

### builder(webpack, gulp, grunt)

### redux, replay or internal react state

### hooks

---

## Terms

- Transpilation: The process of converting one programming language to another.
- npm: Developers use npm to access and manage Node packages.
- Node packages: Directories that contain JavaScript code written by other developers.
- package.json file: A file contains information about the current JavaScript project.
  package.json file can be generated by running `npm init` as long as node is installed

---
