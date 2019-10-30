# File attachment continued (client side, React)
```js
//add feature test
>$ touch cypress/integration/UserCanCreateAnArticle.spec.js  

describe('User can create article', () => {
  it('successfully', () => {
      cy.server()
  cy.route({
    method: 'POST',
    url: http://localhost:3000/v1/articles,
    response: 'fixture:successfully_created_article.json',
    status: 200
  })
  cy.visit('http...')

    cy.get('#write-article').click()
    cy.get('#article-form').within(() => {
      cy.get('#title-input').type('Crazy things are going on atm omg!')
      cy.get('#content-input').type('YEAH!')
      cy.get('#submit-article').click()
    })

    cy.get('#response-message').should('contain', 'Article was successfully created')
  })
})

//configure fixture file
{
  "message": "Article was successfully created"
}

//go to app.js
import and render component:
import CreateArticle from '/Components/CreateArticle'
<CreateArticle />

//create CreateArticle component
import ImageUploader from 'react-images-upload' 

class CreateArticle extends Component {

  state = {
    renderArticleForm: false,
    title: '',
    content: '',
    image: ''
  }

  renderForm = () => {
    this.setState({renderArticleForm: !this.state.renderArticleForm
  })
  }

  inputHandler = (e) => {
    this.setState({
     [e.target.name]: e.target.value 
    })
  }

  submitArticleHandler = async() => {
    const { title, content, image } = this.state
    let response = await submitArticle(title, content, image)

    if(response.status === 200) {
      this.setState({
        responseMessage: response.data.message
      })
    } else {
      this.setState({
        responseMessage: response
      })
    }
  }
    onAvatarDropHandler = (pictureFiles, pictureDataURLs) => {
      this.setState({
        image: pictureDataURLs
      })
    }

  render() {
    let articleForm
    let responseMessage

    if (this.state.responseMessage) {
     responseMessage = <p id="response-message">{this.state.responseMessage}</p>
    }

    if (this.state.renderArticleForm) {
      articleForm = (
        <div id="article-form">
          <input name="title" id="title-input" onBlur={this.inputHandler}/>
          <input name="content" id="content-input" onBlur={this.inputHandler} />
          <ImageUploader
            buttonText={"Upload your article image"}
            withPreview
            withIcon
            withLabel={false}
            onChange={this.onavatarDropHandler}
            ...
          />
          <button id="submit-article" onClick={this.submitArticleHandler}>Submit Article</button>
        </div>
      )
    }

    return(
      <>
      <button onClick={this.renderForm}id="write-article">Write Article</button>

      {articleForm}
      {responseMessage}
      </>
    )
  }
}

export CreateArticle

//create module inside of ArticlesData.js

const submitArticle = async (title, content, image) => {
  try {
    let response = await axios.post(apiUrl + 'articles', 
    {
      title: title,
      content: content,
      image: image
    })

   return response
   //b/c we want the entire response, not just a single thing 
  } catch(error) {
    return error.message
  }
}

export { submitArticle }
```

* onChange = changes state for every letter that you add  
* onBlur = if you click somewhere else on the screen, the input field is not in focus, then it is blurred out and changes the state.  

## Image upload
```js
//install the package
>$ yarn add react-images-upload
```

# Continuation Redux
```js

<Provider store={store}>
<App/>
</Provider>
//the redux wrapper around the app co,poment
//Reducer (only does one single thing for us): only returns the initial state!

window.store.getState() //returns the initial state from the store that we get from Redux.

//App component
import { connect } from 'react-redux'

class App... {
  state = {
    greeting: 'Hello World form Component State'
  }

  render() {
    <>
    <h1>{this.state.greeting}</h1>
    <!--The one we set int he component-->
    <h1>{this.props.greeting}
    <!--
    The actual redux state-->
    </h1>
    </>
  }
}

const mapStateToProps = (state) => {
  //this function call happens before the component is even mounted
  return {
    state: state
  }
  //we want it to return the state object, i.e. we could say:
  greeting: state.greeting
}
//here state has an attribute of greeting

export default connect(mapStateToProps)(App);

//connects the component to the redux store. We want to pass in a function to the connect, by convention it is called mapStateToProps; it will be called every time the redux store changes. It receives the entire store state.

//the connect function takrs a  few arguments, the firsy one is mapStateToProps

//create a completely new component

class AppNew... {
  render() {
    <>
  <Greeting {`${this.props.from} to {this.props.to}: {this.props.content}`}/>
    </>
  }
}

const mapStateToProps = (state) => {
  return {
   from: state.anotherGreeting.from,
   to: state.anotherGreeting.to,
   greeting: state.anotherGreeting.content
  }
}

//another component

import { connect } from 'react-redux'

const Greeting = (props) => {
  return (
    <>
<h2>{props.greeting}</h2>
    </>
  )
}

//we can connect whatever component we want to state

export default connect(mapStateToProps)(Greeting)

//new component
import {connect} from 'react-redux'

const Form = () => {
  return(
    <>
    <button onClick={() => props.dispatch({
      type: 'CHANGE_GREETING', payload: 'Hello!'
    })}>Change greeting
    </button>
    </>
  )
  //dispatch an object with two properties, type and a payload (second argument; could be "greeting"). Type is obligatory. It dispatches an action. Now we need to modify our reducer to accept this argument.
}

export default connect()(Form);

//only dispatches an action hence do not need mapStateToProps here.

//go to root reducer, allow it to take another argument called "action" (naming convention for second argument)
//(first argument is currently initialState)

const rootReducer = (state = initialState, action => {
  return state
})
//here the action would be the object we sent off from Form component

if (action.type === 'CHANGE_GREETING') {
  return {
    ...state, greeting: action.payload
  }
} else {
  return state
}
//we are not modifying the state itself but instead create a new object with its greeting modified. The state is immutable hence we cannot change it inside of the rootReducer.

//mapStateToProps can be thought of as compared with the setState function when we set state to the components.

//multiple reducers in your applications where the root reducer imports your secondary reducers (combinedReducers function) and combine them into one; is to deal with more complex state and actions i.e. if we had a simple reducer as well as one for redux token auth.

//You can also wrap your dispatches in functions so that you can re-use them to keep your code DRY.

//asynchronous calls on reducers and extend using 'func' is a more advanced concept but can be used f.eks. when incorporating fetching data from external APIs.

//navigator = the browser; you're navigator object. it has an attribute called geolocation
//navigator.geolocation
//we can call on this in our browser using:
navigator.geolocation.getCurrentPosition(location => {
  console.log(location.coords)
})

```

# Amazon Webservices (Image attachment part 3)
```js
//Heroku does not give us the functionality to store images, that is why we need to store them on the cloud service (Amazon webservice bucket)

>$ 
```

```rb
#Add gem
gem 'aws-sdk-s3'

#Go into config, development.rb för from local: config.active_storage.service = :amazon

#Go into production.rb:
config.active_storage.service = :amazon

#Add credentials to amazon through storage.yaml, uncomment amazon:
amazon:
#Copy and add exact but header
#(amazon_production and development are only used if you actually go to production)

EDITOR="code --wait"...
#Add to credentials:
aws:
 access_key_id: fwawhahw
 secret_access_key: shakfja
(we get keys)

#AWS console is hard to set up...but you can host a lot of SaaS services. We will only use storage services, called S3. They use a concept of "buckets", which is basically a container.

#every item using active storage as a hash..usually the images are not public but accessed through a publication.

#we get a bucket name
#region: eu-north-1 (region)
#bucket: fake-news-development

#in storage, change to
..aws[:access_key_id]
..aws[:secret_access_key]

>PRY: @article.image.service_url
should in PRY show us the actual url to our amazon picture

#index serialiser:
attr: , :image

def image
if Rails.env.test?
 rails_blob_url(object.image)
 else
 object&.image&.service_url(expires_in: 1.hour, disposition: 'inline')
end

#destroy Articles w/o images in rails c it also deletes amazon webbucket as well


```
```js
//Heroku does not give us the functionality to store images, that is why we need to store them on the cloud service (Amazon webservice bucket)

//src ListArtciles
//debugging the response now contains an image to our url on amazon

//Add:
<img src={article.image}/>
//Ta-da!
//We need to refresh the page as the "indexupdated" just like in cooper challenge, otherwise you need to reload the page.
```
