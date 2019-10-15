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

//Pretend we already have the JS component
import EmployeeList from './components/EmployeeList'

return (
  <EmployeeList />
)
// Install enzyme for component testing
$ yarn add enzyme enzyme-adapter-react-16

//nvm use 11.10.1 for installing enzyme

$ touch src/setupTests.js
//import configure module from enzyme
import {configure} from 'enzyme'
import Adapter from 'enzyme-adapter-react-16'
//issue following command
configure({ adapter: new Adapter() })

//Another configuration is the src folder that will contain our components tests, name by convention
$ mkdir src/__tests__
$ touch src/__tests__/EmployeeList.test.js //same name as component name

//Add the following inside of the testing component
import React from 'react'
import {mount, shallow} from 'enzyme'
import EmployeeList from '../components/EmployeeList'
//by convention the naming should be what component we are using
describe('<EmployeeList />', () => {
  //component needs to be declared before the described block, of course
  let describedComponent
  beforeEach(() => {
    describedComponent = shallow(<EmployeeList />)
  })

  //test and it works the same; they are just aliases for the same thing i.e.

  test('renders <ul>....')

  it('renders <ul> with 5 <li>', () => {
    expect(describedComponent.find('ul')).toHaveLength(1)
    //to have two expect statements in one it block is considered bad practice
    expect(describedComponent.find('li')).toHaveLength(5)
    //shallow is a way to take a react component and render it in memory to do what react actually does with components; takes jsx and transpiles it into HTML view.
    //mount does the same but also takes its children with it.
  })
})
$ yarn run test
//gets error message due to component not created yet.

$ mkdir src/components/EmployeeList.jsx

//using react fragments <> is because they are not being rendered in the browser as such, can hence be used sort of like a placeholder

//Reach out to external API to fetch the users for our EmployeesList.
//A library called axios to read the JSON object to fetch the information about our projects/grab our data; for the portfolio challenge.

import axios from 'axios'

it('should use axios to fetch data', () => {
  //spy on any get request being made by axios; we're telling our test framework to keep a lookout for whatever is happening in the axios component
  const axiosSpy = jest.spyOn(axios, 'get')
  mount(<EmployeeList />)
  //I expect the axiosSpy to be called upon at least once
  expect(axiosSpy).toBeCalled()
})
//add axios to our application
$ yarn add axios
//Change component accordingly, create state (an object holding a key)
//populates it with data, but initially it is empty
state = {
  employees: []
}

//lifecycle event componentDidMount, that will be triggered whenever this component is being used somewhere (i.e. it calls on axios when it is being used)
import axios from 'axios'

componentDidMount() {
  axios.get('').then(result => {
    // do stuff
  })
}

//API REQ|RES is an hosted RESTful API that we can use for test purposes i.e. dummy data.

componentDidMount() {
  axios.get('https://reqres.in/api/users?per_page=5').then(result => {
    this.setState({employees: 
    //result is the entire response we get from axios, and the response has headers and body etc. The body in axious i called "data" and the strcuture of the api also holds a key called 'data', hence the double data call.
    result.data.data})
  })
}

//test file to see if state is updated
// it('should have state after mount', () => {
//   const list = mount(<EmployeeList />)
// })

//in render method for component
render() {
  let employeeListDisplay = this.state.employees.map(employee => {
    return (
      //need key!
      <li key={employee.id}>
      //JS injection
      {`${employee.first_name} ${employee.last_nane}`}
      </li>
    )
  })

  return (
    <>
    <ul>
    {employeeListDisplay}
    </ul>
    </>
  )
)
}

//cypress test file again
beforeEach(() => {
  cy.visit('https....')
});

its('shows the 5 list items', () => {
  cy.get('li')
  .first().should('contain', 'George Bluth')
  .next().should('contain', 'Janet Weaver')
})

//Stub it out! (the API call)
//Go to fixtures, create new file mockerResponse.json and insert the mock data of choice.
beforeEach(() => {
  cy.server()
  cy.route({
    url: 'https://reqres.in/api/users?per_page=5',
    method: 'GET',
    response: 'fixture:mockedResponse.json'
  })
  cy.visit('https....')
});

its('shows the 5 list items', () => {
  cy.get('li')
  .first().should('contain', 'George Bluth')
  .next().should('contain', 'Janet Weaver')
})

$ yarn add semantic-ui-react

import { Container } from 'semantic-ui-react'

//What it looks like inside of React is not how it is rendered when we look inside of the browser for Semantic UI Components...
//needs to change the tests when rendering semantic UI into your components as <li> becomes <List> etc
.find('div[role="listitem"]')

//using shallow the test will fail, using mount will make it pass because shallow only renders itself while mount renders the child components (Semantic UIs components) i.e. now the component is dependent on its children styling components. 

//react.semantic-ui.com
//this page is interactive, click </> tri it to change it yourself to see how the display updates. Aside for the react mark-up it also shows how it would be rendered in html. 

```
- In Cypress you can use "*" symbol right to the "back" symbol to get suggestions on selectors, or inspect the browser as usual.
- 'state' is enough inside of the actual class, but the 'this.state' is to reference back to the class.

# Semantic UI with React
## Install Semantic UI
First, run the following terminal commands:
>$ yarn add semantic-ui-react semantic-ui-css
OR
>$ npm i -S semantic-ui-react semantic-ui-css
```js
//add to index.js to ensure the entire application has access to it.
import 'semantic-ui-css/semantic.min.css';

//import style into component of choice
import { Container } from 'semantic-ui-react'
```
## About styling with Semantic UI in react
- Semantic UI is a fully featured CSS library that allows us to create responsive layouts using human friendly HTML.
- There is a Semantic UI wrapper; Semantic UI React, that is especially made for React.
- https://react.semantic-ui.com
- Good examples, live examples.
- 'semantic-ui-css' is the actual default css package from semantic ui, while the 'semantic-ui-react' is the specifics for React itself.
- Import what you need:
```js
import {
  Container,
  Form,
  Grid,
  Header,
  Message,
  Segment,
} from 'semantic-ui-react'

<Header as="h1" textAlign="center">
<Grid centered columns={3}>
```
### Navigation bar in React w. UI
```js
//add separate function component
<>
<Navbar />
</>

//inside of component
import './Components/NavBar.css'

return (
  <Menu stackable className="logo">
  <Container>
  <Menu.Item>
    BMI Calculator
  </Menu.Item>
  </Container>
  </Menu>
)

//Use CSS file inside of component to add specific CSS styling to that particular component.

//Using Semantic UI it seemds you need to override the fonts with important?
//content of NavBar.css
.logo {
  font-size: 15px !important;
  font-family: blalla !important;
}
```
## Props in Semantic UI
```js
super()
this.state = {
  alignment: 'center'
}

changeAlignment = (e) => {
  this.setState({
    alignment: e.target.innerText
  })
}

buttonClickHandler = (e) => {
  this.changeAlignment(e)
  this.test()
}

test () => {
  //debugger
}


<Header>
textAlign={this.state.alignment}
</Header>

<DisplayResult />
<div>
<button onClick={this.changeAlignment}>Left</button>

<button onClick={this.buttonClickHandler}>Center</button>

<button onClick={this.changeAlignment}>Right</button>

<button onClick={this.changeAlignment}>Justified</button>
</div>
```
- On every input type of component used in Semantic, we can pass in a lot of different props(as="h1") is a prop, "textAlign=Center" is a prop etc...
- You can always debug checking "event"."target" and see what is abailable and what is not.
