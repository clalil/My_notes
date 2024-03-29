# Rails & Ruby  
## Web application development with Rails
- There are best practices to follow; you do not need to re-invent code.  
- 99% of all web development could be done in R&R.  
### What is Rails    
- A full stack web application framework: which means you can deal both with the client side (what user will see), the logic, and the database. RoR helps us with all three layers of web development.  
Example: React is only front end (the view, it has no logic in that sense that Rails has i.e. Rails can create a user in a database - but in React you need an external database and an API to tap into and the logic is limited etc.) RoR is a framework (like something you bought from ikea - you have the tools and building blocks and instructions you need, i.e. you get everything you need in a package with clear instructions on how to use it), React is a library (a bag of tools w/o instructions on how to use them).  
- Written in Ruby; a lot of the philosophies from Ruby.   
- It is based on the MVC pattern: Model, View (what you can see), Controller (logic) pattern - the three layers.  
- Opinionated frameworks: the community believes there are best practices, although we can get the result in different ways. I.e. how we develop, in what order, how we name our variables etc. Some rules we need to follow!  
## What companies use RoR?  
- GitHub  
- Hemnet  
- Airbnb  
- Soundcloud  
- Shopify  
## History  
- Created 2003.  
- Created to rapidly create web applications within a few hours.  
- Rails v 6.0 is planned to be released by 2019.  
- Some issues with security.  
## Rails philosophy (read docs)  
- Dont repeat yourself (every piece of code should have a single, unambigious & authorative representation in the system)!  
- Convention of configuration (only unconventional aspects should be documented a lot; otherwise there should be no questions as how to things should be done).  
- Agile Methodologies.  
## The Rails Doctrine  
- 9 pillars!  
- No one paradigm (multiple ways of doing things - do what we all should do).  
- Provide sharp knives: every toolset we use should be good!  
## Core parts of Rails  
- The model: handles the business logic (database management), is handled by a framework named ActiveRecord.  
- The view: handles by ActionView (like React); i.e. the framework that helps us with the view (what the user will see).  
- The controller: handles by ActionController i.e. where our logic is - how our application is supposed to communicate.  
- Action Pack: the actionview & actioncontroller combined together.  
- Action mailer: another core framework built into Rails for sending plain text HTML and emails.  
- Action cable: another core framework built into Rails for live updates to page.  
- Active support: another core framework built into Rails for Ruby language extensions (seldom used).   
## What will Rails do?  
- Creates full stack web application.  
- Generates a lot of code for you.  
- A fixed folder structure; this is how it is supposed to be!  
- Super easy routing (a way to navigate between different pages in your web application and incoming traffic).  
- Database access through terminal.  
- Easy way to manage database tables.  
- Gives a lot of helper methods (i.e. a small single command to use inside of our code to comprise a lot of code/logic).  
- Allows you to use Gems! Like admin interface, shopping functionality etc. 
- Makes testing really easy; a core principle of the Rails community; the way we test is built in w/o configuration other than Gems.  
- Gives really helpful error messages. 
**Potential downsides:** 
- Slow framework? Matters for google, but not for general web developers.  
- Difficult with live updates?  
- RoR sometimes has too many ways of doing things; general issue for both Ruby & Python though.  
## RoR general  
- App folder is most important: this is where we write our code.  
- Controllers, Models and Views are the main three folders we will work with.  
- Methods are called "Actions" in RoR. 
- index.html.erb (erb stands for EmbeddedRuby, which means we can add Ruby code inside of our HTML page), is what the users will actually see.  
- layouts (application.html.erb) i.e. the basic html structure, where using 'yield' like react renders the <App /> component. Same functionality, different names.  
- schema.rb is a file representation of how your database looks (never ever touch the file manually!!!); this file is generated automatically when we run our migration.  
- feature folder: where we write our feature code.  
- step definitions: similar to cucumber's basic_steps.  
- spec folder; just like in Ruby, however a different way of writing the specs. Gem: shouldamatchers is used.  
- Gemfile: Rails itself is actually a ruby Gem; i.e. the entire framework is a Ruby Gem, which means you can get a lot of functionality from a single Gem.  
## Creating a project in RoR  
- Use Rails v 5.2.3 currently due to it is more stable, has more documentation and has more bug fixes.  
- Use install command for correct Gemfile.  
- Scaffold an entire new Rails application:
```
$ rails new rails_demo 5.2.3 --database=postgresql --skip-test --skip-bundle
```
--skip-test command skips Rails testing framework 'mini-tests'.
--skip-bundle because we want to add a couple of Gems before bundling.  

- Above command initialized git by default for us!  

# What to do?
Create an application which will dislplay a list of articles on the landing page.  
- Test drive  
- Feature tests  
- Unit tests  
- Gemfile should be as clean as possible: delete 'coffe-rails' (Gem for coffescript subbranch for javascript, not needed when using pure JS), 'tzinfo-data' (for developing in windows environment) and 'bye-bug'.  
- Testing gems are added to :development
```rb
group :development, :test do
    gem 'rspec-rails'
    gem 'shoulda-matchers'
    gem 'factory_bot_rails'
end
```
**shoulda-matchers: helps us write our RSpecs in an easier way!**
**factory_** = creates fake objects in the database so you do not have to create it everytime you run; helps with instance doubles.  

Now bundle!!!

- Then; 
```
$ bundle exec rails generate rspec:install
```
=> should be done every time.  

- We can have generators for basically everything in Rails. We also need to specify we want to use them install Rails.  
**Bundle exec means: 'use this version of RSpec'.**

- .gitignore was added by default when creating the app.  
- Next: configure shoulda-matchers. Go to folder called 'spec' and to the 'rails helper'; delete comments. 
- Add the shoulda:matchers configure.  

Now final configure should matchers:  
```
$bundle exec rspec
```

- Turn off unneccessary generators:  
=> go to config folder, application.rb, delete comments, add a snippet of code to turn off spec generators we do not want.  
**Run Rspec to make sure all is working!**  
- Add the 'format documentation' line to Rspec file!  

Start a server to view application:  
```
$ rails server OR rails -s
```
Exit server: Ctrl + C

!!Time to create a new branch!  

### Cucumber time!  
- Add cucumber Gem for feature test;
go to gem file and add the testing gem below grouo :test method;
```rb
gem 'cucumber-rails', require: false
gem 'database_cleaner'
```
database_cleaner: make sure tests do not remain after testing purposes are done!
the false prevents error messages!

Bundle!!!  

- Install cucumber gem:
```
$bundle exec rails generate cucumber:install
```

Next: create a database
```
$ rails db:create
$ rails db:migrate
bundle exec cucumber
```
```
$ rake 
```
= is a command that runs both Cucumber and Rspec for us!  

### Create new feature  
- Create feature file (be very specific!):  
```rb
list_articles_of_.feature
```
Install VSC: gherkin

**Feature:** what the test is about  
**Test descriptions:** use the user stories  
**Scenario**: i.e. 'view a list of articles on the landing page' (can be multiple scenarios like happy path, sad path etc). Ex:
'when I am on the landing page...' 

Note on Cucumber:  
W/o 'pending' in the tests before finalized, you will get a false positive!!!

**Run Cucumber:**
```
bundle exec cucumber <folder_filename>
```

**root_path** naming for first page we want to visit/landing page.  
We set the root_path in our **config folder** in **routes.rb**  
i.e. 
```rb
Rails...
root controller :landing, action: index:
end
```
action: == an action method
```
$ rails generate controller landing index
```
#### What is a controller?  
creates controller (a controller is like a traffic cop when there are no traffic lights; the one who decides where the data should go), controller name and action method  
- Every controller will have a separate folder, and every action will have a separate index file.  

Run Cucumber!!  
(remove generated stuff...)  

=> We need to avoid the hardcorded values! I.e. become false positives, as we want to bring the data from our database!!  

**Background** scenario: Given the following articles exist  
(i.e. we add a cross check).  
|title|content|
|News:....|The worlds....|

etc 

=> The above information would only run in the test, being created for the test environment. Just like the instance doubles.  

**When we are moving towards the Models, it is a perfect time to start with our unit tests; Rspec!**  

### Spec files  
Normally we would create a model that generates our specs for us.  

```rb
require 'rails_helper'
```
```
bundle exec rspec folder_name
```
**bundle exec** is always used because we need to specify that in this case we are working with a version that is older than the most current one (6.0.0).  

RSpec.describe Article type: :model do
end  
=> Article (tells RSpec its a module due to its capitalization), but we also show it using type: :model in addition. Models are ALWAYS Singular (product, user). Controllers though are MULTIPLES (products, users).  
== incorrect naming convention for models and controllers will cause bugs!! In general, you should create the model before the specs - however, during the camp it is simpler to create the specs first and then the model.     

**Everytime we create something in a database, we expect it to have an id; this is default for RSpec.**  

When we work with any type of application where the user/we ourself are going to create content to a database; we need to make sure that we cannot create empty rows accidentally. Also, this can be used by hackers to add content to our website which is empty. Therefore; we need to validate that whatever we put in actually has some content.  

### {} vs () in it blocks:  
- When we use the {} we start a code block to write any type of Ruby code.  
```
$ rails generate model Article title:string content:text
```

### Factory Bot  

### Migrations  
- A way for us to update the database with new information.  
- It takes the code that someone else has written and updates your local database. This information is only contained in the migration file.  
- You have to migrate when getting someone else's pull code, we bundle (make sure added gems are added to local computer) and do a migration (to make sure our data is in the same state as the other persons).  

**<% %> = embedded ruby code (index.html.erb)**  

<% = does not print it out on the screen  
<%= = does print it out to the screen/page  

- The page will not display 'mock' data we use in our tests.
To make it appear on the page:
```rb
$ rails c

article = Article.create(title: "Yield seems to be a problem", content: "Have you looked inside the routes?")

=> shows the sql code

To show the website content:  
$ rails s
```  
To make it prettier:  
<h1><%= article.title%></h1>  

# Introduction to Legacy Code Challenge 
## What is Legacy Code & How to work with it  
Legacy code is source code inherited from someone else : source code inherited from an older version of the software.  
Legacy code is difficult to work with in part due to a lack of automated tests.  

To read code without proper documentation is an aquired skill.  

## 7 techniques to unravel legacy code  
* Rubber ducking  
A well-known technique. Take a plastic rubber duck, place it next to the computer, and read the code out load to the duck. You're reading it to the duck because the duck will be there to listen without giving judgement. When you have to vocalize the code; you will see flaws and see where the code is breaking.  
The rubber ducking is similar to having a pair programmer to discuss things with.  

* Testing the software with Acceptance and Unit tests  
An AUT cycle; add feature, add functionality, add feature etc. 
Decide what to refactor => test the current code => perform refactoring => test the rewritten code => perform a regression test =>

* Following the dataflow  
Dataflows can be used to understand how the codebase works. By clicking around in the application to change the variable names slightly to see how the data flows, how the gems are being invoked etc. This can sometimes be the only way to really understand the code base.  

* Reading the commit messages  
Go to the different commits, click on the different commits to see what was added during that time. There are tools inside of Github to find a specific variable and see how it has changed over time.  

* Changing the code  
Change some bits and pieces to understand the dataflow. For example during CSS or similar.  

* Debuggers  
A good way to change a value, add a value and see what it does. Like debugger or PRY.  

* Refactor code  
An advanced technique; you take a bit of the functionality to make it even better: make change => refactor it => test fail : test pass etc is used to make a choice about wheter or not to refactor.  

# Web architecture  
## What is web architecture  
- Layer describe logical groupings of the functionality and components in an application.  
- Tiers describe physical distribution of the functionality and components on separate servers, computers, networrks or remote locations.  
- Only tiers imply a REAL separation.  
- AUT cycle RoR dealt with all three things.  
- You need to have the model, which is connected to the database while the database itself is a separate entitiy on the computer. The views are also separated.  

We decide the layer (files and naming), the tier we do not decide: it is decided for us.  

## Three Tier architcture vs Three layers  

Layers: we can change as we like, unlike the tiers.  

## The 3 tiers  
- Presentation tier: the user's interface (what theya ctually see), it displays informatiomn related to different services that we have.
It communicates with the other tiers by connection and displaying the result to the client. 
- Logical tier: coordinates the application "spindeln i nätet" that makes logical decisions, process commands, evaluates and performs calculations. 
- Data tier: the persistence layer, the place where information is stored and retrieved from the database system. It saves information from a database and save it to another database.  

## MVC  
Browser: the webpage/like Chrome, takes the user input => webserver => routes => dispatcher => controller (decides what to do with the information, and sends information back and forth depending on what the model deciees).  

Example of how things are run:  
Customer = The user input/sees from the view  
Fridge = Database
Products = View
Waiter = Controller
Kitchen = Model  

There are some instances/an exception where the waiter would create the food in front of the user/customer.  

In which part of the application am I inside at the moment? Should I be there? Should I be doing these things inside of the model or inside of the controller? Some heavy calculations would the model do due to higher processing power, not the controller.  

Fat Models ? Skinny Controllers  

## Useful concepts  
HTTP Protocol: foundation of data communcation for the internet.  
Functions as a request-response protocol in the client-server computing model (entering password on fb (client) sends request to the fb server (their server sends response back to the client side)). A client is whatever the user is holding in this/her hands in order to communicate with the internet.  

URL (Uniform REsource Locator): a reference to a web resource that specifices it's on a  comp network and mechanisms for retrieveing it.  

Request methods: 
GET, POST, DELETE, PUT/PATCH
**REmeber in and out by the end of the boot camp**  
GET = asking for the server to give you some kind of information ie give me this user name, give me this form so I can log in, give me my image.  
POST = save it to your database, create a new username, create something for me, take my image and save it for me (saving and creating are POST requests)  
DELETE = Please delete my information on your system (blog post etc).  
PUT/PATCH = please update the information from me that is already on your sever; my profile image etc  
**Patch is getting out of style - mostly use Puts**  

A sevrver: a computer programme or device that provides functionality for other programs or devices (clients).  
E.g. web server, file server, mail server  

# The magical params hash
## What is the Params Hash?
Parameter hash = a hash that stores informationed passed from the users browser. 

Gives us the ability to use the user input in our application. i.e. When I send my login details it is sent to the paramters hash. It is a hash which job is to take user information and send it to the server.

Main different three types:
Query string params OR Route params OR Post params

###Query string Params:
This param is sent to the URL.
When you google - the information is sent to this param. You can see it in the url as:
…com/over/there?key=value
=> a query string param is when we search for something!!
- The query param always starts with a questionmark in the URL (/?q=hello/) i.e. (/?key=value/)

### Route params
- Links to a specific object (blog post, article) and uses the id of the object.
- A URL with a number in the end is indicating a route param.
- Objects will always have the same id and we can use this id to navigate between pages we want.

### Post Params
- Sends information in order to create an object. I.e. sends information from a form; stored in a params hash => creates/saves a new/existing object in our database. Most often done through a form.

Params = a way to send specific information from the user to our application!!

# Heroku  
- Used to deploy our rails applications.  
- Heroku is a cload platform where you can deploy applications and modify them.  
- Heroku is different from Netlify, as we use this for Rails.  
- Heroku is an easy platform for new developers, works well with Rails applications, good easy terminal CLI (work from your terminal/Computer Client Interface?).  
- It's free to deploy small applications; not files stored in database etc.  

AUT = Acceptance Unit Test Cycle  

## Challenge - deploy your application to Heroku  
- Download/Install Heroku  
- SignUp on Heroku.com  
- Deploy your application to Heroku  
- Push up code to Heroku  
- Migrate the database up on Heroku  

1. Login Heroku
2. If there is already an existing database: rake db:drop rake db:create
3. $ heroku create <myname-rails-demo> 
4. Gives you a URL for app
5. Now you need to push the application to Heroku, so that it can access it.
6. git remote -v (should should heroku remote)
7. git push heroku master (I want to push my master branch to their master)
8. Bundle with 2.0 and above, you will run into problems! There is a package for Heroku to fix that.
9. Gives Rails error window.
10. (heroku crates a database for us - do not need to create one) 
$ heroku run rails db:migrate
11. (To add articles) 
$ heroku run rails c
12. Getting into the environment/irb: Article.create(title: 'Hello', content: 'How are you?')
(if it has an id - it persisted!!)

!!!Whenever we do a change - we need to do git push heroku master!!!
It is NOT like netlify for this!

### Warden  
- Is a production Gem that helps us login and logout inside of the testing environment. "Given I am logged in" - shortens the steps for us.  
- find_by == Active Record helper method. 
- F.eks. Cucumber does not know where to start - it only goes where we tell it to, that's why we need Warden to "make it stop". 


# Validations in Rails.  
## What are validations  
- A way for us to make sure that the information that is being saved into our database contains all the relevant data. Ensuring that no malicious data or harmful data is added to our database is very important, especially when handling user data.  
- We use validations for safety, performance and user experience. Because we only want to add valid data; the most common cases are so that no-one can fill the dstabase with bad data. Performance reasons: less false data entries, fewer empty rows -> more concise database and helps us find our information more quickly and improves informance.  
- We give error messages to the user when they pass in wrong data; this also reduces empty rows.

## How Rails uses validation  
- Sign-up button sends information to the Controller, which looks at what we want to do (create/save data), it sends it to the model (this is where the validation is done, might return an error to the user if the data is wrong), THEN it sends the data to the database! I.e, the MODEL has the security checks.  
- create, create!, save, save!, update, update! When these methods are run, we can use validations on them, because these method sends data to our database.  
- Validations are used in the model because they will then be closer to the database (due to the nature of the validation, it makes more sense to have this process as close to the database as possible i.e. the model). Validations inside of the database would call problems when testing and maintinging the database. 
- Client side can use validations (inside of the browser), but it is often not enought - we have to use JS in order to validate on the client side. However, since JS can be turned off in the browser - which overrides that functionality.  
- Controller validation are hard to maintain. The controller handles multiple functionalities (saving/creating/deleting etc) and we want to minimize this! I.e. the waiter should not need to consider more tasks that he actually has to i.e. his core functionality.  

## How to add validations?  
- We add a keyword called validate/validates to :name, presence :true.  
- We add an attribute to what we want to happen.  
- When we are creating an object in our database, it will check if .valid is true and not false before saving it to the database.  
- Confirmation validator; (validates :email, confirmation: true). Validates that both fields contain the same information.  
### Validator helpers:
- Acceptance validation (validates checkbox on the UI, "confirm terms & conditions on a website").
- Inclusion; validates that attribute's values are included in a given set. I.e. that the attributes we are passing in are relevant to what we want to create like "is not included in the list".    
- Length validator; validates length of attribute values like postcode length, pincode length etc.  
- Presence; validates the specified attributes are not empty, like "mandatory filling ins on a website".  
**Rails Guide has all the validations**  

# Rails & Routing  
- Routing creates pathways inside of our application so that we end up in the right controller and the right action.  
- Resource routing:
* GET = asks server for information (to read an article)  
* POST = save some kind of information to the database (written an article and want to save it)  
* PUT = helps us to update the entirety of an article (update everything inside of it)
* PATCH = update a part of information (update a title of an article)
* DELETE = deletes the entire article from the database  

## CRUD, verbs and Actions  
* CRUD = Create, Return, Update & Delete  
* resources :articles (adding the keyword resources to a route file  and the controller of choice we get access to the data that responds with these).  
* the #index actions job is to display a list of all articles/products etc    
* this also means we will have a folder called articles inside of the view for our index file.  
* HTTP verb (GET/POST), Path(/articles), Controller#Action(articles#index), Used for(Display an list of all articles) etc

## Path and URL Helpers  
* article_path returns /articles  
* i.e. we add the word _path to whatever controller we are using, we can access it inside of our code. Like new_article_path returns /articles/new.  
* edith_article_path(:id) returns a speicific article using an ID, e.g. article_path(11) returns /articles/11  
* article_url returns http://domain.tld/articles  
* set up root controller (action specifies where this goes to, in this case the root is index page): 
```rb
root controller: :posts, action :index
```
Acess the routes using:
```rb
rails routes
```
Use the only keyword to specify what we only want to access to (USE THIS):  
```rb
resources :articles, only [:index, :show, :edit]
```

## Non-resourceful routing  
* Old way of writing routes: get '/articles/new, controller: :articles, action: :new', nowadays we just use the resource. Old ways can be used for API, but not writing for the actual new code. DO NOT USE!!!

## Namespace (put inside of the routes.rb, NOT about functionality)   
* When you have multiple controllers that deals with similar things, we can to organize it in a specific way.  
```rb
namespace :author do
    resources :dramas, :magazines, :thrillers
end
```
* Only helps us organize our controllers (admin interface). 
This is a cleaner way than to write 'resources' for each one on one row.  

## Nested routes  (Regards TO functionality)
```rb
resources :magazines do
    resources :articles
end
```
We need to be able to associate different models with each other. 
http://guides.rubyonrails.org/routing.html (Routing from the outside in)

# Controller, Router etc. 
* A controller's purpose is to receive specific requests for the application. 
* Routing decides which controller receives which requests. 
* A view's purpose is to display this information in a human readable format. 
* It is the controller, not the view, where information is collected. 
* If you want to create a new HTML form, you use the ERB language which is designed to embed Ruby in HTML, i.e. articles/new.html.erb 

# HAML. 
Online translators can translate erb into HAML. (Avoid the hash rockets!)
HAML is like YAML: very sensitive and unneccessary spaces will have dire consequenses! Tabs or spaces need to be the very same inside of VSC.

VSCO set up specific tab or space setting.

## Semantic UI GEM
- Rather than using a CDN.  
- Only works with JQuery, i.e. may not work in other projects where we do not use JQuery.

# Design sprint
## Spend time preparing what to build
- Less issues down the road.

## Basics of a design sprint
- Design sprint is a time constraint five-phase process (i.e. in our development process we talk about sprints. One week is often considered a part of a sprint (one week, two week or a month sprint). The design sprint is when we go over the features we need to have.) to reduce the risk when bringing a new product, service or feature to market.
- We want to create a bunch of user stories that go over the features we want to add. A bunch so that we can pick and choose what we want to create in a specific order.
- As a group; everyone sits down and discusses what a user story does. We assess it as a team so everyone knows how and what and why.
### Purpose
- MVP = Minimum Viable Product. A product with just enought features so satisfy a customer; to provide feedback for future product develpment. We use our user stories to create our MVP.
- We always want to have a functioning product at each step of the way.
* Example: LinkedIn MVP core is basically a site where you display your CV to others. One layer is security so only one person can change its own CV, another layer is the networking part, another layer is the chat functionality etc...
* Example: a car's main purpose is to move a person from plance A to place B; the first core functionality could be a skateboard, then a kick bike, then a bicycle (more distance covered), motorcycle (more speed) and car (more security). etc.

## Lo-Fi's ("a white board")
- A tiny representation of a concept, a use flow, or an information structure created for getting quick feedback and improving the product.
- We use a Lo-Fi to make sure that everyone in the group understand what we are trying to build.
- E.g. we create a Lo-Fi for a login page. By adding these small things there will be no confusion as to what everything is and why.)

## Wireframes
- Often done with collaboration with a UX designer.
- Very time consuming and should only be done once you know what you are going to develop.
- Used to provide a visual understanding of a page early in a project to get stakeholders to become interested.

## Checklist DEsign sprint
- Start with the idea and lo-fis
- Decide what flow you will work on first, how will it interact with the application step by step.
- Cross check if the wireframes meet the requirements of the client/user.
- Create acceptance criterias to each story (go into each User story and add acceptance criteria (tasks). Once all tasks are checked off - the user story is completed.). Approx 4-5 tasks per User Story. If you have more tasks than that - you probably need to split your user story into several.
- Create ERD (optional) is basically a way to illustrate how your database looks; how is all connected?
- Prioritize stories (in what order should we build these different features? Remeber the MVP! Does it make sense to build a login functionality if we do not have any products on our website yet?)
I.e. products, login, payment etc; add complexity!
- Do a dry-run with the team memebers (time consuming and tiresome process but needs to be done, not uncommon further down that there is a big difference between team members how an application should be). I.e. everyone should know where the graphics and functionality are supposed to go so that every team member is on the same page.
- Add chores ().
- Add a few stories on the backlog and vote on these.

# User stories
A User Story is centered around three important questions:
* Who's using the system?
* What are they doing?
* Why do they care?

# Continous integration & Deployment
## Continuos integration
- Makes sure everything we add is compatible and integrated with our exisiting code base.
- Software development practice where each developer is required to integrate code into a shared repository (upstream) several times a day.
- Each check-in is then verified by an automated build, which allows teams to detect problems early. This is gonna be semiphore: it runs all of our tests and makes sure that what we want to add is compatible and works with our already built in code.
- CI catches issues early, less time spent debugging, no more time to wait if code will work and reduce integration problems allowing you to deliver software more rapidly.
## Practices
- Maintain a single source repo.
- Automate the build (Semiphore).
- Make your build self-testing.
- Every commit has to build on an integration machine.
- Test in a clone of the production of the environment.
- Make it easy for anyone to get the latest executable version.
- Automate ddeployment.
## How it works
- Developers check out code into their private workspaces.
- When done, commit the changes to the repository.
- Then CI server monitors the repo and checks out changes when they occur.
- The CI server builds the system and runs unit and integration/acceptance tests,
- The CI server releases deployable artefacts for testing.
- The CI server informs the team of the successful build.
- If the build or test fails, the team will be notified immediately.
## Continious deployment
- To make sure everything we add to the code base actually gets deployed.
- Everytime something passes the test we will push up.
- Travis/Semaphore are equal.
- Circleci is compatible with client applications like react (what sempahore is for rails applications)
- How it works: CI goes green and application gets deployed, it goes red it goes back to the developer.
## Test coverage metrics
- Checks how much of the code has actually been tested.  
1. Create an account.
2. Log in (check out repos).
3. Choose CA.
4. Click "on" on the application.  
5. Press "details"; shows what you need to do inside of the terminal.  
6. Go to terminal and be on the "development" branch.
7. Pull latest version; git pull upstream development.
8. git checkout -b coveralls
9. Open code base.
10. Go to Gem-file, add **gem 'coveralls', require: false'** under development, test
11. bundle!
12. Go back to code base.
13. Go to "features", to the "env.rb"-file. Enter (on top of the file to make all lines aware of it):
```rb
require 'coveralls'
Coveralls_wear!('rails')
```
14. Go to spec folder and rails helper, add the same things there (at the top!!)
15. Go to Semaphore, use Semaphore classic link (login) and then login with github.
16. Authorize render text on Semaphore. Press "start project" using GitHub. Only public repos.
17. Authorize again. Important you see organization craft academy.
(If you cannot see the upstream repo then you need CA to set you as an admin!!)
18. Press 'slowfood-june-2019_team_1" under CA.
19. Select branch => select development. Wait for analyzing.
20. Check language, version, database.yml (sometimes Semaphre gets this wrong and you need to make sure it is 'pg' for postgresql).
21. Before we can merge anything; every test should go green through Semaphore. 
```rb
bundle exect rake db:setup
```
...Is ususally not needed if we already have db:create and db:migrate.
22. Remove the setup commands that you do in one single command list. 
23. Edit job under setup:
```
  bundle install --deployment --path vendor/bundle  
  bundle exec rake db:setup  
  bundle exec rake   db:test:prepare  
  COVERALLS_REPO_TOKEN=your_coveralls_token   bundle exec rake ci:tests
  ```
24. Copy repo token you have on Coveralls replace with **you_coveralls_token** to tell coveralls where to save it.  
25. Press "build with these settings".
26. Press "Add collaborators and build".
27. Everytime we push up to a branch that is part of our PR it will run whatever that we're trying to add using the code above.
## Push to Heroku
1. Open terminal (right folder!).
2. Run **heroku create your-name** + enter
3. Go to Heroku in the browser (dashboard).
4. Go to the app you just created.
5. Go to "deploy".
6. Press "github" for deployment method.
7. Connect to Github (only one person per team).
8. Search for repositories to connect to; CA slow-food.
9. Connect.
10. Choose "wait for CI",  "enable automatic deploy" for the right git branch.
11. Done!
12. Deploy branch (manual deploy). 
13. If application error; view logs, go to the terminal and run heroku logs. 
14. Read error, check bundle in Gem-lock.
15. Go to "more", run console "heroku run"....ask coach!!
16. run **bundle version**
check if incorrect or not.
If needed, remove Gemfile-lock as it is automatically generated when we "bundle".
17. Run bundle.
18. Gemfile should not have the right version.

# HAML
## Introducing a faster better way of writing HTML
- A pre-processor of HTML, whatever we write in HAML will be parsed to our HTML.
- Reduces code due to no closing tags, uses indentation for nesting markup, a more concise syntax which makes coding your View layer faster.
- It doesn’t affect render time or client side performance, but simply reduces coding efforts and makes the development more efficient.
- It can be used in many Ruby frameworks such as RoR, and Middlemans Rails and Sinatra, but also in Node.JS, Net etc
- Usage; use it as a replacement for ERB files. If you use bundler, add this to your gemfile: ``` gem ‘haml’ ```
- Files named filename.html.haml will be interpreted by HAML instead of ERB.
```rb
%body  
 #wrapper   
  .stuff
    %a{href: “#”} Top
=> body tag, div, div, link named “Top”.
```
### Tag names
Use % and then the name of the tag.
e.g. 
><body_></body_> == %body
- id:s are referenced the same way as in CSS i.e. 
><div_ id=“my id”>
#my-id
><h1_ id=“article”>
>%h1#article
- HAML assumes you want a DIV unless you say something else.
- Classes:
```rb
<div class=“wrapper”>
.wrapper
<h1 class=“content”>
%h1.content
%div.wrapper.container.row#my-id
is a div, with two classes, inside of a row with a id-tag my-id
IS THE SAME AS
div.wrapper.container.row#my-id
```
- If you leave out the %tag and only include the .class or #id a div tag will still be created for you!!!
## Nesting
- Is important as there are no closing tags in HAML.
- Tags are nestbed by indentation only.
- Text can go at the end of the line if there’s no other content ot nest. Can also be nested itself(required with other nested content).

### Craft Academy website GitHub
%h1
 = “Tech ba <br> bla”.html_safe
(html_safe makes it possible to enbed real html tags inside of the haml text
OR
%h1= “Tech ba <br> bla”.html_safe

**Inline style:**
%p{style: ‘max-width: 29em;’}
 %strong
  With Craft…

### NewsFlash
= partial :’new_flash_en’

extracting other files into one file.
```rb
Intake.future_dates(0..2).each do |intake|
 %h4. leader
  = intake.course_name
  = ‘-‘
  = intake.start_date.strftile(‘%-d %b %Y’)
```
# Rails Recap
## App folder
- Use to store all of our code.
- Assets folder holds all of our CSS/Stylesheets and images folder/files.
* Config folder is used for out JS.
//= link_tree ../images
//=link_directory ...stylesheets .css
- Channels (where we have anything used for push notifications or chat functionality). Works similar to controller functionality.
- Controller folder always has an application controller (takes in all of the code and functionality from the ActionController core frame).
* Concerns folder contains our refactored code/extracts functions to keep our code DRY. I.e. the place where the store our refactored code. A partial is only used for the views; could be a navbar. I.e. in the FizzBuzz challenge our refactored piece of code would be put inside of the concerns folder (HAS_ZERO_REMAINDER). However, it should just be the code that is used throughout the application and our controllers.
* Helpers folder: when we want to create helper methods for ourselves like form helpers. We can add these to our application helper.
* Javascript folder; adding initializers and js code we wrote ourselves.
* Jobs folder (ActiveJob::Base), could be used for trash collection etc.
* Mailers is a folder that deals with any eamils being send from/to our application (ActionMailer::Base).
* Models stores our business logic that we creates as classes.
* Concerns folder inside of Models folder; where we keep our refactored code for our different models.
* Views has different templates for layouts etc. Post folder contains the different views for our different pages.
* Bin folder (seldom tocuh this file, has setup files).
- Config folder
* Environments (same as in Gemfile); i.e. when we are for example in the development environment that will only trigger certain Gems. If we are testing or having real server; we will need to change the environments.
* Initializers: contains files that will kick in when our server starts. Can be start a webserver, create a welcome message etc. Anything we need to initialize before our app starts running. I.e. if a Gem requires us to create an initializer, then we would put it here.
* Locales is a folder where we store all of our translation files.
* Webpack is used for JS and when we want to make different configurations for different environments.
* Application.rb is where we turn off the generators when we are using Rails. When we run a generator (f.eks. new controller), a generator is a method for scaffolding code. A generator will set up the correct name etc and will also create the connected files. Apart from creating the views it also creates stylesheets; which can bloat our application with all files. That is why we configure our generators to only create what we need and not to create unneccessary files.
* Cable: where we set up our different servers that we will use for Action Cable.
* Credentions.yml.enc; credentials is a file that holds all the credentials that we use (like encrypted password, API keys or information for user account). To keep our information safe; we store it inside of our credentials file. We can unlock this information with the help of our **master.key**. If all developers has thay key inside of their system then they can access it. The master.key is never uploaded to GitHub since it is by default added to .gitignore.
* database.yml is a configuration file for our different environments.
* puma.rb is a webserver we use and we can configure it in there.
* routes.rb is where we keep all of our routes like 'root controller: :posts...'
* spring.rb is used to upload the right ruby version from our computer.
* storage.yml is used to upload things to amazon etc; where me make the configurations and pulls in the credentials from our credentials file.
 - db folder
 * schema.rb is a representation of how our database should look.
 * seeds.rb file; is used to save us from having to manually create page content each time we run the server. It goes into a rails console and rails pulls things out from our database to rails. 
 ```rb
 rails db:seed
#seeds the database.
```
* lib folder; here we can also use assets that are stored..
* log folder is interesting when we are debugging because it shows all the entries we did in our server. It shows all the different errors. This does not that that much space. Videos etc are what takes space.
* node_modules
* public folder (the static pages that are displayed when your server is done, these are cached by google and other search engines).
* storage (information about Active:Storage)
* test folder (Rails has a built in test framework called mini-test; that's why we do 'skip test' when we create our application because we use other frameworks like Cucumber).
* tmp (database settings)
* vender (where we store static, third party code that we cannot add in any of our other folders).

# Factory Bot
Configs included if: FactoryBot::Syntax::Method you may use (:create) and not (FactoryBot:create) in the test environment, because it is already in the environment.
