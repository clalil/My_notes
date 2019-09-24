# React with Thomas  
React is a JS library, that allows us to build rich user interface.  
"Every framework can be viewed as an attempt to say: the hardest part to write a webapplication is {X} so here's some code to make it easier."  

There are pros and cons (like better code/app structure, common concepts and large communities) and cons (learning curve, setup and infrastructure and minimum requirements for size etc) with every framework.  

There are some frameworks that are better suited for small and large projects respectively.  

## About React  
- A JS library for building user interfaces  
- Declarative (a form of programming) 
- A component based framework  
- Learn once and write anywhere!  

Declarative vs Imperative programming approach:  
- In React, you can focus on what the state of your user interface should be once a component is in its place.  
- In imperative programming; you go step by step to tell the program what it is supposed to do.  

Component based:  
- A style of software development that focuses on creating small, self-contained components that can be strung together and build fully-featured user interfaces.  

Learn Once, Write anyhere:  
- A myth of the industry. 

## Choosing React  
- Hard to learn how to think in React due to the leverage of all the things that can be accomplished using React.  
- It's easy to learn React's basic concepts and API.  
- React applications are built around 2 main principles: components (for example a button) and states (a button is clicked, or not!).  
- Components === State Machines  
- React thinks of UI as state machines.  
- Components === JS Functions  
- Just like how functions take parameters: components take in values and return UI input.  

## Components  
- Functional components (cannot hold state, only functionality).  
<noscript>You need to enable JS to run this app</noscript>  
- Whatever happens in React is handled by that library, but it needs to be connected to the JS.  

JSX Syntax:  
- JSX is a preprocessor step that adds XML syntax to JS.  
- Requires compilation process (babel).  
- Makes React a lot more elegant.  
- {} escapes from the syntax
- Uses capitalization to differentiate between HTML elements and React components.  

**A class always needs a constructor!! (in JS)**

## The React way: separations of concerns  
- The idea of mixing the user interfaces into one single component is very crucial.  
- We do mix presentation and logic in the same files (compared with other situations).  

## Let's code!  
react_meetup_demo_app  (CA repo)
```
$ npm i
```
To run the React application
```
$ npm run start
```
```js
state = {
    name: 'Thomas'
}

<h1>Hello {this.state.name}<h1>
```
The first time: the name is set; if using a 
```js
this.clickHandler.bind(this)
onClick = this.setState({name: 'Random Person'})
```
it changes the state from 'Thomas' to 'Random person'.  
```js
clickHandler(event) {
    this.setState({name: event.target.value})
}
```
debugger == can be used to debug the code in JS to find where to call what to make the function work as needed to. **Just like binding.pry**.  

Difference between declaring a constructor or not in a class?  
None. The constructor will always be set.  

**A state can be passed around as props, but will not be shared.**  













