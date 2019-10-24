# NewsRoom Challenge (building an SaaS application)  
- Produce a digital newspaper.
- News is defined in the first room here.
- Build a fully featured news platform.
- Project time is 3 weeks.
- Sprint lenght is 7 days.
- Practice more advanced strategies with continuous deployment, and more advanced Rails concepts like Action Mailer, Active Storage and ActiveJob. 
- Make use of Geolocation and analytics.
- Build more engaging user interfaces.
## Definition of an MVP
- A version of a new service or product which allows a team to collect the maximum amount of validated learning about customers with the least possible effort.
- The MVP (Minimum Viable Product - the minimal to make the application going) can be further developed to a complete web application w/o having to design it from scratch.
- For us, RoR is suitable both for low cost prototype development and for developing fully featured web applications.
## Core principles of Agile
- Working software is the primary measure of progress.
- Deliver working software frequently, from a couple of weeks to a couple of months, with a preference to the shorter timescale.
- Our highest priority is to satisfy the customer.
- An approach that embraces change; welcoming changing requirements even late in the development. Agile process harness change for the customer's competitive advantage.
- Develop a business oriented approach. Business people and developers must work together daily throguhtout the project.
- The project must make sense from a business perspective; that we are focusing on the right things at the right time.
- "Don't think as developers first-hand, think of people who are building an application for the first time".
## Cross functional teams
- Groups people with different functional specialities or multidisciplinary skills, responsible for carrying out all phases of a project from start to finish.
- Cross-functional: representatives from the various functions in a development team. As opposed to functional expertise (system analytics, developers, testers...). Nowadays, everyone is part of the team with their expertise like UX Designer, TDD expert, programmer etc...
- We are going to work with project management tool Pivotal tracker again.
- We will work with the user stories again.
- We will build this with an API and React Client. The current stories, these are "pointers" at the moment to set the direction to move towards.
- First challenge: rewrite the stories to represent both the backend and the client side. 
- All of the stories are important and should be implemented first.
- Further on we can add more stories, but these ones are the most important part of the MVP. "Implemented at the very least, a scoped version of the feature."
- One PR per chore!!!!
## Engaging user interfaces - going mobile
- Make sure to consider all of the options on the client side.
- We can either build our mobile application into an Ionic App (we wrap the application inside of the framework Ionic that will help us build applications that will be hosted both by macos and android), React framework will build native applications for android and apple.
- Mobile application != responsive website.
### Challenge: build an end-to-end news creation, production, curation, distribution and publishing platform for localized news.
- Create news, display and delete them.
- Location; if in Sweden see swedish news, not from Ukrain or China and view them in my own language. I.e. relevant news and correct language.
- Different categories; i.e. today I want sports and not politics. Be able to filter or see news in a good way.
- Monetization; how do we make money from this application?
- Multiple language support.
- Administration/moderation; someone needs to be able to check the articles our before publication. 
#### The Paywall
- A big part of the NewsRoom Challenge is about monetization. As developers, we need to understand the underlyng business the applications we build support. This challenge is about that.
- As you browse around the various publishing sites, you'll notice that there are many different wats to implement a paywall solution (f.eks on aftonbladet you have to pay for a subscription to extra content), as well as how to build a user interface that is inclusive and provides a good user experience (UX). Another experience is WallStreet where you pay after a certain amount of free articles.
- The monetary stratergy depends on the market.
- Make sure to research before deciding on a specific stratergy. Hybrid model? A pwaywall is a requirement.
## Deployment
- Deploy to Heroku and use that servering during development (staging).
- For production, we will create and deploy to Digital Ocean (www.digitalocean.com).
- Challenge time: week 8, 9 and 10.
- Coach support: the coach is supposed to be a team member and treated as such.
- Coach meetings: at least 1 during the project and a final delivery meeting. But form your own stratergy.
- Deploy the final application individually from your own repos.
- Sprints: if you follow Scrum; 7 days.
- Deliveries: Depending on the project managements method you choose. Form your own strategy.
- Requirements: meet them in a creative way. If a client has asked you to do certain things; they need to get what they want. You need to be mindful that you have the user perspective and the perspective of the client.
- Always be able to answer why you have prioritized in a certain way. 

# Design Sprint Recap
## Basics of a design phase
- Design sprint is a time-constrained, five-phase process that uses design thinking to reduce the risk when bringing in a new product, service or a feature on the market.
- We sit down as a team and dive down into what we are going to build, it's a planning phase where we kind of makes sure that everyone in the development team knows what is going on. 
- The entire group needs to be totally in agreement on what and how something is going to be built.
- During the first design sprint we envison how the MVP will look as the final product. 
## Purpose
- A Minimum Viable Product is a product with just enough features to satisfy early customers, and provide feedback for future product development.
- Create user stories to build a MVP.
- We basically add the core functionality of the application to take it from A to B.
- First we need to ask our customers what they think of the application.
## Lo-Fis
- Representation or image of how our application should be created; one low-fi for each feature. 
## Wireframes
- More advanced version of Lo-Fis, often done together with the designer. Used in a later stage in teamwork with a UX designer. (We do only need Lo-Fis so far).
- Aim of it is to provide a visual understanding of a page early in the project to get stakeholder and project team apporoval.
## Checklist
- Start with the idea and the wireframes (Lo-Fis).
- Check if the wireframes meet the requirements.
- Create acceptance criterias to each stories.
- Create ERD (optional); visuellt how the databases are intertwined(?).
- Prioritize stories.
- Do a dry-run with the team members.
- Add chores.
- Add a few stories to the backlog and vote on these.
- Start with core functionality!
## Epics
- Epics are a large bodies of work that can be broken down into smaller chunks called stories.
- F.ek.s Stripe functionality can be broken down into "Add product to chart", "Add details", "Make payment", "Receive confirmation email".
- Have 4-5 stories to an epic.
- Have one user story for each epic?
- The Epic is the book and the user stories are the chapters of that book.
### When to use an epic?
- The time to use an epic is something big like a payment gateway, to create articles etc. Basically, when you're unsure of the process (like adding geolocation) and it contains multiple steps and if it's a big feature (will take a couple of days to finish off) and to me a new feature.
## Voting 
- The voting itself is a process when you take a user story and assigns it a complexity point (how complex a user story is; how long time it will take to implement, how much functionality do we need to add, how much previous research do we need? All of those things add to the complexity of the user story).
- Why vote? To keep track of the velocity, for future reference, create a baseline (how capable is our group?).
- Voting is for assessing complexity points of a user story.
## Voting questions
- Have I done it before, or has any other team member done it before?
- Is there any good documentation?
- Is it easy to test (time consuming to get into place?)?
- Do we need external resources(do we need to call in someone to help/hire them or do we have that competence in-house?)?
- Time equivalent(will it take days, weeks or months?)?
- Business value(how highly prioritized is this functionaloty and how hard to implement?)
- Assess the complexity; 1-3 points (easy-harder). Everyone needs to be in agreement (unanimous result of voting in the group), if not - have a discussion.
- When do we do the assessing of complexity/voting; right before we start developing those stories. I.e. we add a couple of user stories to the backlog and then we assign the complexity points. We can assign them before the daily scrum, drag chosen user stories to backlog from icebox, vote on them.
- You cannot as an individual go in and assign a complexity point w/o the agreement of the entire group.
- If you for some reason have to change the point of the story, the whole group has to go in and give an OK i.e. re-vote on a story.
- Use slack to vote simultaneously on the user story complexity points.
- Asses, re-evaluate, assess etc...
## Chart flow:
Application => Requirements (2) => Epic (2) => User stories (2) => Acceptance criteria(3)  
- I.e. When multiple acceptance criteria is met; the user story is met. When the user stories are met, the epics are done. When the epics are done - the requirements are met. When the requirements are done - the application is done.

# [Agile methodologies](https://youtu.be/502ILHjX9EE)
- The agile approach is a business oriented approach; i.e. business people and developers must work together daily throughout the whole process.
- It is also a people oriented approach; trust the people to get the job done and build projects around motivated individuals.
- It is a learning oriented approach; continuous attention to technical excellence and good design enhances agility.
- Agile practices vs Agile mindset (doing agile vs being agile).
- Scrum is an agile framework for completing complex projects; simple but not easy.
* Roles: ScumMaster, Product Owner and Scrum Team
### Artifacts:  
* Product backlog (bucket for requirements)
* Sprint backlog(subset of PB, highest priorities deemed by Product Owner)
* Burndown Chart (chart indicating how much work is remining in the sprint)
## Scrum + XP (Extreme programming)
- Behavior Driven Design (BDD)
- Test Driven Development (TDD)
- Pair programming
- Automated testing
- Refactoring
- Code Reviews
- Continuous integration
- Continuous deployment
- Great combo because it leverages the popularity of Scrum with the sound engineering practices of XP.
- This approach is used at Craft Academy boot camp.
- We will face pitfalls and slipperly slopes in the newsroom challenge when trying to connect our API to the client side.
## Agile myths
- Agile is a silver bullet (nope, agile requires hard work and great planning but anything in a group will always expose risk to conflict etc)  
- Agile is a anti-documentation (nope, documentation us as means of communication and gets estimated, sized and prioritized like any other user story, our tets are our documentation)  
- Agile is anti-planning (nope,a lot of planning goes into this; the daily stand-up is sort of a planning meeting as well as during iteration/sprint planning meetings)  
- Agile is undisciplined (nope, you have to test, get feedback, ship software regularly, change and update plan and deliver bad news early)  
- Agile requires a lot of rework(as every other method..., not a silver bullet. any creative work with a deadline faces the same challenges; you've got to let go of the pride and rethink your solution if it doesn't fix the problem anymore)  
- Agile doesn't scale (it scales as every other software delivery process; not that well. the only thing we can do is to scale things down!)  
- Agile is anti-architecture(agile is not a religion; follow the company way)
## Agile: Incremental and Iterative
- Working software quickly and early
- Less costly to change requirements
- Easy to test and debug during smaller iteration
- Customers can respond to each built
- Lowers initial delivery cost
- Better risk management

You can become a good developer with good habits in just 12 weeks, but not the best programmer in the world, of course.

# Authentication w. Oliver (Rails side)
```rb
#/devise_token_auth.rb

#Need to change token from js to text because we use text in cooper challenge and not json format that we send.

#/session_spec.rb
#We nwws to add the data response due to devise but can be nil b/c we do not use them.

$ rails g migration AddTrackableColumnsToUsers
+ add needed columns for remaining columns

```
# Authentication w Oliver (React side)
- Package: redux-token-auth
- With this package we need to have redux implemented on our application.
- Is a package built for react and redux with rails backend that uses devise token auth.  
```js
//create cypress test
userCanLogin.spec.js
beforeEach(() => {
  cy.server()
})

it('successfully', (() => {
  cy.route({
    //stub out response
    method: 'POST',
    url: 'http://localhost:3000/v1/auth/sign_in',
    //check path in backend for POST
    //i.e. url to stub out
    response: 'fixture:successful_user_login.json',
    //here we store what we stub out
    status: 200
    //add status for 'happy path'
  })

  cy.visit('http://localhost:3001')
  cy.get('#login-button').click()
  cy.get('#login-form').within(() => {
    cy.get('#email-input').type('user@mail.com')
    cy.get('#password-input').type('password')
  })
  cy.get('#submit-login-form').click()
  cy.get('#welcome-message').should('contain', 'Hello user@mail.com')
}))

//400 non-existing page, 402 non-authorization in general

//Go into component to create btn
<button id="login-button">Login</button>

//need to add event to render loginform
state = {
  renderLoginForm: false
}

renderForm = () => {
  this.setState({
    renderLoginForm: !this.state.renderLoginForm
    //bang means set to the opposite of what it is!
  })
}
//use arrow functions do not need to bind this

render() {
  let loginForm
  
  if (this.state.renderLoginForm) {
    loginForm = (
      <div id="login-form">
        Login Form
      </div>
    )
  }
}

<button onClick={this.renderForm}id="login-button">Login</button>

{loginForm}

//next step, create the actual input fields

  if (this.state.renderLoginForm) {
    loginForm = (
      <div id="login-form">
        <input id="email-input" placeholder="Email"/>
        <input id="password-input" type="password" placeholder="Password" />
        <button id="submit-login-form">Submit</button>
      </div>
    )
  }

//It is now time to install the dependencies...
>$ yarn add redux react-redux redux-logger redux-thunk redux-token-auth

//in order to use the redux-token-auth dev we need to wrap our whole application around redux; which gives us the ability to have an overall state. Every component in the application can push up to the "redux store", which is a global state for the entire application".

//in index.js, configure

import { Provider} from 'react-redux'
import configureStore from './state/store/configureStore'

const store = configureStore

ReactDOM.render(
  <Provider store={store}>
  <App />
  </Provider>
  document.getElementById('root')
);

// create folder and files inside of src folder

>$ mkdir state
>$ mkdir store
>$ touch configureStore.js

// Add to configureStore...a LOT
thunk, logger etc...
//logger shows how redux changes

//in state folder, create new
>$ mkdir reducers
>$ touch rootReducer.js
//import stuff..
//in the redux state there will be a key called reduxtokenauth that will have som initialized values and functionalities that it inherits

//inside of state folder
>$ mkdir actions
>$ touch reduxTokenAuthConfig.js
//validates user and exports functionality
//adds a lot...

//Go back to app.js
//add two new states
email: '',
password: ''

inputChangeHandler = (e) => {
  this.setState({
    [e.target.name]: e.target.value
  })
}

//inside of the loginForm variable, add name="email" and name="password" to the different input fields as well as onChange={this.inputChangeHandler} to each of them

//import to App component:
import {signInUser} from '../state/actions/reduxTokenAuthConfig'
import {connect} from 'react-redux'
//added to add connection to..

//add to bottom of App.js

const maoStateToProps = state => {
  return {
    currentUser: state.reduxTokenAuth.currentUser
    //here we want to use some of the states from redux and put it inside of some of our props for this component
  }
}

const mapDispatchToProps = {
  //we need to tell redux what we want to use inside of this component, that is why we need to map that out
  signInUser
}
export default connect(
  mapStateToProps,
  mapDispatchToProps
)(App);

//go to underneath inputChangeHandler
<button onClick={this.handleLogin} id="submit.."></button>

handleLogin = () => {
  const { signInUser } = this.props
  const { email, password } = this.state
  signInUser({ email, password })
   .then(console.log('woooo'))
   //we do not want to do anything after this...
   .catch(error => {
     console.log(error)
   })
   //once signed it, redux switches the state isUserSignedIn from false to true
}

//add to render
let welcomeMessage
if(this.props.currentUser.isSignedIn) {
  debugger;
}

//stub out fixtue successfull login
{
  "data": {
    "id": 1,
    "email": "user@mail.com"
  }
}

//go to reduxTokenAuth...
//to userAttributes, change credentials to mock response in fixture file;
email: "email" etc..

//inside of app component:
let welcomeMessage
if(this.props.currentUser.isSignedIn) {
  welcomeMessage = <p id="welcome-message">Hello {this.props.currentUser.attributes.email}</p>
}

//+ add the object {welcomeMessage} inside of the return

```

# Serialization (the process of converting objects/datatypes to a format that can be transported across the network or persisted)
```rb
let!(:article) {3.times {FactoryBot.create(:article)}}
#request specs
it 'lists a collection of articles' do 
get '/api/articles'
#Doing get request to specific URL, the RESTful route
json_resp = JSON.parse(response.body)
#grab response body and turn into json response to have something to compare with
expect(json_resp['articles'].count).to eq 3
#check if array returned to us contains 3 objects
end

ArticlesController
articles = Article.all
render json: { articles: articles}
#built in method in Rails to serialize json into objects

#Network calls takes time, they are time consuming and our users want speed.

#gem ActiveModelSerializers is an extension library that allows us to work with serialization in a different way.

# Add gem, then go into configuration file in config/initializers and create new file called eks "ams.rb" (activemodelserializers):
ActiveModelSerializers.config.adapter = :json

#replace render json in controller with:
render json: articles, each_serializer: Articles::IndexSerializer
#will give error, not created yet

$ rails g (generates a list of available commands issued for generators)

$ rails g serializer Articles::Index
#Adds folder etc..
#Add more attributes to it
attributes :id, :title, :published_at
#Adding :published_at returns error b/c no such exists yet
def published_at
  object.created_at
  #the serializer is accessible to us through 'object'
end

#add change to display fornat differently
object.created_at.to_formatted_s(:long)
#You can modify your data on the API instead of doing it on the client side.

#Add to the serializer index
#belongs_to :author or do like with published_at i.e. create new method



```