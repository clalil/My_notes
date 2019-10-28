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