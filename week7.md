# React Advanced  
## Prerequisites  
- Basic knowledge of React JS, JS, of the DOM, Familiarity of ES6, Node.js and npm installed globally.
- BMI Challenge (testing w. jest, enzyme and cypress).
- Cooper Challenge (BDD and TDD driven development in React).
- Build our own API this week (interacting with back-end).
- Important to understand how a client talks with the backend and what part the client is in the MVC pattern.
- MC in the back end and client is the view.
- Use SemanticUI for Reacy, use the project as a "KitchenSink" for experimenting with React.
- More advanced usage of stateful/stateless components.
- Interaction with API (getting and writing data).
- Manage state - Introduction to redux.
- Testing (unit/component tests and integration tests).
## Testing
- Acceptance test (is the application doing what we want it to do?)
- Component test (are each individual component doing what we expect).
- BMI Challenge: simple logic. 
- Copper test challenge: back-end; does it matter? Client in React, back-end in Rails. Testing fetched data from API.
- Now it's time to learn how to 'think in React'.
### Shortcuts in VSC extension
imp  
imn  
est  
cmd  

# AUT cycle in React
- Not using 12.10 version of NPM? Issues with it.
- React Create App is scaffolded and comes with more additions that what the library React in itself does.
## Cypress
```js
//Initiating and installing cypress
$ ./node_modules/.bin/cypress open
// silent npm so only cypress is run and not pop up the browser (will not work in NPM 12.0.0)
"cy:open": "npm start --silent & cypress open"
$ nvm use 11.6.0
to change version.
//in the json, change this to make the server silent, doesn't work on windows:
"cy:open": "BROWSER=none npm start & cypress open"

//In VSC, json:
"extemnds"...
"globals": {
  "cy": "cy"
}

//Extensions VSC: Cypress Snippets
```
- Test files go into our integration files, of course.
### Our first test
```js
//New file in integrations folder
//e.g. displayEmplpyeeList.js
//just like in RSpec, we use the describe blocks
//mocha is what makes it like rspec
describe('/index Displays a list of employees', () => {
  it('when user visits the page', () => {
    //callback
    cy.visit('http://localhost:3000')
      .get('section[name="header"] h1')
      .should('contain', 'Employee List')
      .should('not.contain', "Hello")
      .should('have.length', 1)
      //first arg is matcher, 2nd is value
      //1 since there is only 1 h1
  })
});
//uses the 'contain' matcher passed in as a string

//Cypress is js-based.

```