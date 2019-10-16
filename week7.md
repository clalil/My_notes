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

# Cooper Challenge
- Learn how to build an API using RoR.
- Learn about CORS
- Learn avout testing API endpoints with Rspec using so-called request specs
- Learn how to authenticate users from a React application
- Learn how to make a post request to an API from a client

## Persist data
- User login
- Rails to save the user data
- Back-end in Rails (Model, Controller)
- Client-side in React (View)

# Rest on Rails  
## What is REST
- An artitechtural style of building applications (we provide inter-operability; a computer system om the internet. That means we can connect with a computer system on the internet). REST is the artitechtural style that also uses the rrequest-response cycle.
- A proven design pattern for building loosely-couples, highly-scalable applications. 
- Stateless; it's based on request-response architecture, that you send off a request and gets one back. But it does not remmeber what it receives and sends (has no state). 
## What is state?
- Application state (it should live on the client, and we supply with each client request, we need to make sure that the client/not server is responsible for remembering the data.)
- Resource State; we need to make sure that the state that is passed in is persistent if the client dies (needs to be persisten on the client side).
## What is statelessness?
- Client state should not be stored on the server between requests.
- Each individual request should have no context of the reqtests that came before it.
- It is stateful when/if we have designed it to remember what has happened before. Stateless; designed NOT to remember.
- The server should not remember what information it receives; the consequence is that the client shuld send all of the information that tje client needs. This also means we need to send all of our important data every time we do a request; because the servers do not remmber what happens.
### Why statelessness?
- statelessness makes the web scale. The design is great when the application is separated from the data.
- visibility: every request contains all context neccessary to understand it. Looking at a single request is sufficient to visualize the interaction.
- reliability: since a request stands on its own, failure of one request doesn not influence others.
- scalibility: the server does not have to rememer the application state, enabling it to serve more requests in a shorter amount of time.
## To think about in REST
- Whenver we deal with the CRUD actions we are dealing with REST.
- CRUD actions are robust, consistent and understandable within the entire industry; the same kind of resources over the different kind of protocols.
- Names identifies resources; 'get_cocktails' is shown in the URL when connection to the API.
### What is resource identification?
- Each request should uniquely identify a single resource; when dealing with a show/index action we are dealing with one resource.
- Each request that modifies the database shpuld act on one and only one row of one and only one table.
- Requests that only fetch information should get zero or more rows from one table.
## What is REST?
- The information that is returned as data.
- To make sure the system understands what information we're getting we need to use the standardized formats: XML or JSON (JSON nowadays).
- The returned information shpiuld be sifficoent for the client to uniquely identify and manipulate the database rows in question.
## REST in RoR
- RoR is built upon this.
- Default way of building resources; also built upon basic CRUD methods that are automatically connected to a HTTP protocol.
- Uniform interface (anyone with programming knowledge will know what these type of actions are)
- Convention over configuration! I.e. we do not think about how to set things up that RoR does for us.
### Nouns vs Verbs
- Try to use nouns instead of verbs when naming resources.
- Use concrete names and not action verbs (person ist for can/begin) etc.
## APIs in RoR
- Why build our own API? We want to use an API b/c it is our easiest way to connect to an external resource. We can skip the interface and straight go to the back-end and then bring that to our front. Instead of communcating with servers using links/forms, we can get it directly using our API.
- Why use RoR to create API insgtead of Sinatra? Answer: it gets us all that we want and is built upon the RESTful architecture for free w. RoR. Otherwise, we need to configure all of this manually. RoR also gives us a lot of security with its conventions. Also, we can use a lot of testing.
The command:  
>$ rails new my_api --api
creates an application that is api only, and does not have all the logic needed for a front-end application.  
- We can add our own api functionality to extend functionality of an already existing application. 
- Easy versioning of the API, i.e. different versions of the API v0, v1, v2 etc... which we can use to ensure backwards compatibility. I.e. when we update our API then people might loose all of their functionality when upgrading; once we updated and add functionality to our new version then it is up to the client to update to the new version or not; we provide new entry points to it. I.e. new user = new functionality, old user = still working functionality.
### Request specs
- Request specs are for APIs what acceptance tests are for web applications.
- Monolit application = an application entirely built in e.g. RoR.
- Industry standard is to do request specs in rspec.
- Whenever you deal with APIs you need to have request specs first.
- 
