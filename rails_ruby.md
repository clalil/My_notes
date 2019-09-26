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



