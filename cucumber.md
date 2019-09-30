# Cucumber and Webpack  
## Getting started  
A quick note on version control: **before** you start working on an important piece of functionality for this application, you must always create a **new branch** from master and work from that "feature" branch. Once you have completed the feature and are happy with the changes, you may merge those changes back to master and repeat this process for the next feature.  

### [Yarn](https://yarnpkg.com/en/docs/install)  
Yarn is a package manager for your code. Code is shared through a 'package' (a module). Once installed, initializing yarn it creates a package that contains all the code being shared as well as create a package.json file which will be used to manage all our project's dependencies and hence describe the 'package'.  
* A package.json file is a file that lists the packages your project depends on.  
* A dependency is when a piece of software relies on another one. Example of dependecies for Cucumber are:  
[Chai](https://www.chaijs.com/), which is an assertion library for Node that provides interfaces to express assertions in tests, like the __expect__ syntax.  
[Puppeteer](https://github.com/GoogleChrome/puppeteer), which is a Node library that can perform tasks like creating an automated testing environment using Chrome, JS and browser features. It provides a high-level Puppeteer [API](https://www.reddit.com/r/learnprogramming/comments/1xvm9l/can_some_eli5_what_an_api_is/) to control headless Chrome/Chromium over the DevTools Protocol. Example of when the Puppeteer comes to play is when using the openHomePage() helper method; its [API](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md) is needed to create a browser page object and navigate to it. [It has a lot of useful helper methods](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pagewaitforselectorselector-options).  Every promise that is returned from Puppeteer will timeout after 5000 milliseconds by default if they can't be resolved.

[Superstatic](https://github.com/firebase/superstatic), is a static web server that can be used during development of applications.  

Installing packages with yarn using the --dev option saves packages as [devDependecies](https://medium.com/@stalonadsl948/dependencies-vs-devdependencies-926e096a3dee), instead of usual dependencies, which tells the npm that these packages are needed during development and not for production.

## About Cucumber  
[Cucumber](https://github.com/cucumber/cucumber-js) is a tool for running automated acceptance tests written in plain language that can be read by anyone.   

Cucumber is a toolset that helps you test what you should see on a website or what the result should be when youʼre on a loading or landing page. Cucmber is interactive: for example it clicks on a login button for us so that we don't have to rely on manual testing. We use automated testing (unit testing like an algorithm or connection to an API) using RSpec and feature testing/acceptance testing is used with Cucumber.  

Cucumber assists the programmer in working in a Behaviour Driven Development (BDD) way where work from the user perspective.  

### Cucumber uses gherkin  
[Gherkin](https://cucumber.io/docs/gherkin/reference/) is a simple set of grammar rules that makes plain text structured enough for Cucumber to understand. It is also a Domain Specific Language (DSL) that allows expected software behaviors to be specified in a logical language that customers can understand.  

* Comment lines are allowed anywhere in the file using the #-symbol.  
* The recommended indentation level is two spaces.  
* Each line that isn’t a blank line has to start with a Gherkin keyword followed by your text of choice.  
* The first primary keyword in a Gherkin document must **always** be Feature, followed by a **:** and **a short text** that describes the feature. The purpose of the Feature keyword is to provide a high-level description of a software feature, and to group related scenarios. 

```
The primary keywords are:

- Feature
- Rule (as of Gherkin 6)
- Example (or Scenario)
- Given, When, Then, And, But (steps)
- Background
- Scenario Outline (or Scenario Template)
- Examples
There are a few secondary keywords as well:

""" (Doc Strings)
| (Data Tables)
@ (Tags)
# (Comments)
``` 

**STEPS**  
Each step starts with: 
**Given** = describes the scene of the scenario, typically a past event.  
*When* = used to describe an event or action; like a person interaction with a system.  
*Then* = are used to describe the expected outcome or result.  
*And, But* = can be used when there are several __Given's, When's or Then's__.

Cucumber executes each step in a scenario one at a time, in the sequence you’ve written them in. When Cucumber tries to execute a step, it looks for a matching step definition to execute. You *cannot* have different steps with the same line of **short text**.  

### Helper methods and Tips  
__openHomePage()__ == navigate to the home page of the app after opening a browser.

__world__ == a concept in Cucumber that is used to represent the application under test. It is an isolated context for each scenario, exposed to the hooks and steps as the keyword __this__. You can create and use a custom cucumber __world__ object with the module and constructor  __setWorldConstructur__.  

__this.browser = await puppeteer.launch()__ == creates a browser object using puppeteer.  

__this.browser = await puppeteer.launch()__ == creates a new webpage, using the puppeteer.  

__await__ == using this keyword before every call to the puppeteer's objects will wait for the Promise objects to be resolved before assigning the response to each variable involved in the Promise. The __await__ keyword can only be used inside of the [async function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function). 

__Opening and closing pages when using Puppeteer__: When working with puppeteer's page object, you should always close the page when you finish working with it, or your Cucumber will stay idle. Adding the keyword __After__ to the initial require 'cucumber' steps will close the page after every scenario.  
```
const { After, Given... } = require('cucumber')

After(async function() {
  return...
})
```
__content()__: Puppeteer's helper method returns the HTML content of the page object as a String. May be combined with the JS helper metod [String.match()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/match), which retrieves the result of matching a string against a regular expression.

__waitForSelector()__ == receives a selector as an argument and waits for it to appear on the page. Can be combined with the [__click()__](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/click) method. This function resolves when the specified element is added to the DOM. 

[__page.$(selector)__](https://github.com/GoogleChrome/puppeteer/blob/master/docs/api.md#pageselector) == The method runs document.querySelector within the page. If no element matches the selector, the return value resolves to null. The (selector) here is a <String> and it returns a Promise.  

__type()__ == the ES6 version of typeOf()

__DOMContentLoaded__ == 
[List of DOM events](https://developer.mozilla.org/en-US/docs/Web/Events)  
[List of event targets](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget). 
DOMContentLoaded, when used together with addEventListener(); it will fire up and execute the defined callback function when the page loads and every element is drawn on the page.  

__document.querySelector()__ == takes a CSS Selectors as arugments

__inputSelector__ == holds the selector of an input field  

__btnSelectorFromName()__ == returns the proper selector for a button based on the name provided.  



### Capybara 
Capybara is the syntax you have to use in order to write the cucumber tests. The user stories are written using gherkin syntax and then Cucumber will automatically translate them into tests. The methods you need to use in the test use Capybara. Cucumber can be connected with RSpec and Capybara and used to write integration tests.  

Capybara provides helper methods for when testing is done in the browser (high-level tests like clicking links, filling out form fields etc).  

[Capybara cheatsheet](https://devhints.io/capybara).  

## Webpack  
[Webpack](https://webpack.js.org/) is a module bundler with the main purpose to compile JS modules into a bundle.js to be loaded in a index.html. Every time you make changes to a JS file, you need to run the **yarn build command** to genereate a new bundle.js file.  
```
$ yarn run build
```
To avoid having to remember to run build every time you make a change, the watch command can be used instead as it restarts and generates a build every time you make any changes in the current directory.  
```
$ yarn run watch
```

If using ES6, the code also needs to be transplied using a transplier like [babeljs](https://babeljs.io/).  

### Local Storage
[LocalStorage](https://developer.mozilla.org/en-US/docs/Web/API/Window/localStorage) is a type of [web storage API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API/Using_the_Web_Storage_API) that allows Javascript websites and apps to store and access data right in the browser with no expiration date. This means the data stored in the browser will persist even after the browser window has been closed. Local storage also allow us to store key/value pairs that are saved across browser sessions, using methods like [setItem() and getItem()](https://blog.logrocket.com/the-complete-guide-to-using-localstorage-in-javascript-apps-ba44edb53a36/).  

### Node JS  
[Node.js](https://www.reddit.com/r/javascript/comments/oq4p2/nodejs_can_anyone_eli5/)  

# About the step defintions 
- Features share the same step definitions. Hence, if we have the same step defintions for different feature tests, they will cause an unaumbigious match. That is why it is important to reuse our steps as much as possible, since Cucumber is very sensitive to commas etc.  
- Basic steps should contain common steps that are shared by all of the functionality of our app like clicking on buttons, deleting forms etc.  
- Assertion steps are the "Then I should see"/"And I should see", and is identified by an "expect". These are also, in many cases, shared between step defititions. These assertions should have a specific file for each feature where the functionality would be specific for that special feature, the rest can go into basic steps.  
- Background is used when something is needed to exist in order for our assertions to work when we test the specific functionality. I.e. we need to be logged in in order to send email. The background "sets the table we eat from".  

# Capybara Cheatsheet
## Matchers
expect(page).to have_content("Some Content")
expect(page).to have_no_content("Some Content")

# True if there is a anchor tag with text matching regex
expect(page).to have_xpath("//a")
expect(page).to have_xpath("//a",:href => "google.com")
expect(page).to have_xpath("//a[@href => 'google.com']")
expect(page).to have_xpath("//a[contains(.,'some string')]")
expect(page).to have_xpath("//p//a", :text => /re[dab]i/i, :count => 1)

 # can take both xpath and css as input and can take arguments similar to both have_css and have_xpath
 expect(page).to have_selector(:xpath, "//p/h1")
 expect(page).to have_selector(:css, "p a#post_edit_path")

 expect(page).to have_css("input#post_title")
 expect(page).to have_css("input#post_title", :value => "Capybara cheatsheet")

 # True if there are 3 input tags in response
 expect(page).to have_css("input", :count => 3)

 # True if there or fewer or equal to 3 input tags
 expect(page).to have_css("input", :maximum => 3)

 # True if there are minimum of 3 input tags
 expect(page).to have_css("input", :minimum => 3)

 # True if there 1 to 3 input tags
 expect(page).to have_css("input", :between => 1..3)

 # True if there is a anchor tag with text hello
 expect(page).to have_css("p a", :text => "hello")
 expect(page).to have_css("p a", :text => /[hH]ello(.+)/i)

# For making capybara to take css as default selector
Capybara.default_selector = :css

# checks for the presence of the input tag
expect(page).to have_selector("input")

# checks for input tag with value
expect(page).to have_selector("input", :value =>"Post Title")

expect(page).to have_no_selector("input")

# For making capybara to take css as default selector
Capybara.default_selector = :xpath
# checks for the presence of the input tag
expect(page).to have_selector("//input")

# checks for input tag with value
expect(page).to have_selector("//input", :value =>"Post Title")

# checks for presence of a input field named FirstName in a form
expect(page).to have_field("FirstName")

expect(page).to have_field("FirstName", :value => "Rambo")
expect(page).to have_field("FirstName", :with => "Rambo")

expect(page).to have_link("Foo")
expect(page).to have_link("Foo", :href=>"googl.com")
expect(page).to have_no_link("Foo", :href=>"google.com")
## Actions
click_link 'Save'

# Button
click_button 'awesome'

# Both above
click_link_or_button 'Save'

# Text (area) field
fill_in 'Name', with: 'Content'

# Checkbox
check 'Content'
uncheck 'Content'

# Radio button
choose 'Content'

# Select option from select tag
select 'Option', from: 'Label'

# File input
attach_file Rails.root.join('spec/fixture/some_file.png')
## Finders
page.all(:xpath, '//a')

page.first(:xpath, '//a')

page.find('//textarea[@id="additional_newline"]')

page.find(:xpath, "//input[@id='form_pets_dog']")['checked']
# => true

page.find(:css, '#with_focus_event').trigger(:focus)

page.find(:css,'.wrapper').hover

page.find_field("test_field").value
# => 'blah'

page.find_by_id('red').tag_name
# => 'a'

# finds invisible elements when false
page.find_by_id("hidden_via_ancestor", visible: false)

page.find_button('What an Awesome')[:value]
# => 'awesome'

page.find_link('abo').text
# => 'labore'

page.find_link('other')[:href]
# => '/some_uri'
## Scoped Finder
 within 
within(search_form) do
  fill_in 'Name', with: 'iOS 7'
  click_button 'Search'
end

def search_form
  '.search_form'
end

within_fieldset("villain_fieldset") do
  # ...
end

within_table("some_table") do
  # ...
end

# Execute the given block within the given iframe using given frame name or index.
#
within_frame('some_frame') do
end

save_page

# You need to install launchy gem.
save_and_open_page





