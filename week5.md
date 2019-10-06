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

# Controller, Router etc. 
* A controller's purpose is to receive specific requests for the application. 
* Routing decides which controller receives which requests. 
* A view's purpose is to display this information in a human readable format. 
* It is the controller, not the view, where information is collected. 
* If you want to create a new HTML form, you use the ERB language which is designed to embed Ruby in HTML, i.e. articles/new.html.erb 

# User stories
A User Story is centered around three important questions:
* Who's using the system?
* What are they doing?
* Why do they care?

# Acitive Record Basics 
- Is a module that is included in Rails.
- Active Record is the layer that represents the business data logic (the M in MVC).
- ORM = Object Relational Mapping.
## Convention vs Configuration
- The core principle is to do by convention rather than having to configure everything yourself. Active Record is a conventional way to do things.
- Naming conventions: 
**Databases**
 should be named using snake case to separate the words.
E.g. people database with order_items (class) 
**Model Class**
Singular with the first letter of each word capitalized (PascalCase).  
E.g. Person, Article...
**Foregin Keys**  
Name following pattern: singularized_table_name_id  
e.g. a blog post reference "user_id"  
**Primnary Keys**  
- AR will use an integer comulmn named id as the primary table key.  
- This column is created automatically; like article id#1, article id#2 etc - it will not replace deleted items but keep on counting.  
## Create Active Record (AR) Models
- A model in RoR is a class that inherits from another class called Application Record.  
- With this inheritance it automatically gets a lot of functionality.  
- You instanitate a new object with the 'new' command i.e. we can later on assign attributes to it (ApplicationRecord gives us both setter and getter methods).  
### CRUD  
- Create, Read, Update, Delete
## Create
- AR brings the create method to us i.e.  
```rb
article = Article.create(title: 'Hello')  
article = Article.new  
article.title = 'Hello'
```  
- It is a compound method that does two things simultaneously for us; instatiate new object and giving it some attributes. 
- Create is a constructor method that creates the object itself and saves/persists the data to the database & gives it an id. 
## Read  
- Access the data from the database.  
```rb
#(queries the database for all instances of the Article class)
articles = Article.all
#Return first id ever created
article = Article.first
#Find a resource
article = Article.find_by(title: 'Hello')
```  
- You can name your variables accordingly to if you are assigning it data in singularis or pluralis.  
http://guides.rubyonrails.org/active_record_querying.html  
## Update  
```rb
# Save command after finding and renaming an instance
article.save
# Find article using 
article = Article.find_by(title: 'Hello') #then update to change AND save the object in the database
article.update(title: 'Goodbye')
# Update and save new property to instance object
object.update email: 'joe@doe.com'
```
## Delete
```rb
#Find object and purge it
object = Object.find_by(title 'Hello')
object.destroy
# destroy all
Object.destroy_all
# Show all
Object.all
```

## Migrations  
- Migrations allow us to alter our database as we move along, after creating it.
- Whatever we are adding to our database like classes etc can be updated using migration.  
- Migrations allow us to continuously update and modify our database w/o breaking our current database.  
- All our migrations are stored in db migrate folder with a time stamp and descriptive snake_case name.
- The timestamp is because it needs to run the migrations in a specific order.
- Schema and chanegs to be DataBase (DB) independent.  
- SQL code = Structured Query Lanugage (no need to write this using migrations).  
### Changing Exisiting migrations
DO NOT DO THAT!!!  
Write a new one instead!!
You would rarely need to do that!  
http://guides.rubyonrails.org/active_record_migrations.html  

```rb
#Can be used to see if your changes were indeed persisted
object.persisted?
#Returns the number of found objects
object.size
#F.eks. there are four id:s in the database, we can access #2 as such:
object.find 2
#Or if we have a user with an email
Object.find_by email: 'joe@doe.com'
Object.find_by_email: 'joe@doe.com'

#.where command always returns a collection even if it only has one item
collection = Object.where email: 'joe@doe.com'

#Find it
collection[0].email
#OR
collection.first.email
```
```rb
#Returns the very same key from the hash
user_1[:emai]
user_1['email']
```
```rb
#reloads the saved object
object.reload
```
# Poetry mode  
- If you can omit the parenthesis; you do it.  

# Relational Databases  
## What is a database
- A place where you store information.
- We use a database because it is much easier to handle things with a database instead of a YAML file etc. We want a database when we know we will have a lot of user input that we need to store/a lot of things going on. If we stored this in a YAML file it would quickly explode in size. I.e. as soon as we know we will store a lot of data we will need a database.  
- A database is a collection of information that is organized so that it can easily be accessed, managed/organized and updated.
### DBMS
- DBMS: Database Managagement system (toolset); a collection of programs that will do certain tasks for us. These systems will allow us to access the database and manioulate the data. It helps us in the represenation of data and helps us control access to the database by various users.
- F.eks: we only want us programmers and admins to be able to access the database; the database management system will help us do just that.
#### Types of DBMS
- Navigational DBMS
- Relational DBMS (the one we are using during this BC)
- SQL DBMS
- NoSQL DBMS

## Relational DBs
- Are a collection of data items organized as a set of formally-described tables from which data can be accessed or reassembled in many different ways w/o having to reorganize the database tables.
- Each table contains data in predefined columns. These columns represents the attributes we create for our Models. Like "title" for our Article Model.
- Each row contains a unique instance of data defined by the columns. The rows represents different/unique instances of our Model. Like "Article title "Hello World".
- I.e. it is essentially a table with columns and rows.
- A way for us to uniquely identify another table instance is to use a **foreign key**; ie a way to connect two different tables/instances of tables with each other. F.eks. We have a DB which is a fridge, the tables are like shelves in the fridge where one is "veggies" and one is "bread"; so we have different tables inside of the same DB.
- Example: a table describes a customer with columns, another table would describe an order.

## Relational DBMS apps
- MySQL
- PostgreSQL (works well w. Rails)
- Microsoft SQL
- MariaDB etc...

## Data Models
- Entity Relationship Diagram (ERD): real-world objects/item with properties/attributes. Every attribute is defined by its set of values called domain.
- Relationship: logical association among entities. "A book has many chapters". These are the different relationship we have with our different models.
**1-1** ("One person has one id card")
**1-many** ("A book has many chapters)
**many-1** ("Many students to go the same classroom")
**many-many** ("Many restaurants have many dishes")
### Entitity relational Diagram
- Used to visualise how our different models are connected, to have a structured approach as programmers.
- A Gem can be downloaded for this.
https://editor.ponyorm.com/user/pony/PhotoSharing/designer
- The arrows in above user table represents the relationship. "One user has many followers and followee", "one user has one image, but the image can have many tags."
### SQL
- Structured Query Language
- Rails takes care of writing SQL code for us.
- The lanaguage we need in order to talk to our database is SQL.
### ORMs
- Object-relational mapping libraries map database tables to classes.
- The attributes we have in our models we directly translate into our database table.
- i.e. our Models (it's essentially a class) "title" etc will translate as "title" as one column etc..
- Example: if a database has a table called customers, our program till have a class named Custromer. Rows corresponds to instances of the class Customer, within the object and attributes are used to get/set each column.
## ActiveRecord
- The M in MVC. 
- IS the way for us to connect to our database using Ruby.
- AR is a core framework of the Rails framework. This is the way that Rails speaks to our database; which is why we only need to learn AR and not SQL.
- AR represents the models and the data.
- Represents the association between our different models.
- Represents inheritance hierarchies throuhg related models.
- Validate models before they get persisted to the DB. (validates the data is real)
- Perform db operations in an object-oriented way.
### Naming conventions
- Database table (plural with underscores separating words). Rails actually looks at the naming and will draw conclusions based on our naming conventions. i.e. order_items, people, articles.
- Model class needs to be singular. e.g. Person, OrderItem, Article. The database will be named automatically for us, we only need to name our Model.
### Schema Conventions
- Foreign keys (a way for us to make a connection to a different model i.e. one model called product and one model called sales). Name following the pattern: singular_snakecase (user_id, order_item). (helps us to identify another table). F.eks. **id** is the primary key and **customer_id** is the foreign key in a Customer Model.
- Primary keys (set automatically by Rails). AR will use an integer column named "id" as table primary key. 
**Summary:**  
- The foreign key has the customer_id in the table; would only mostly be used in connections to other tables.
- The primary id in each table is only referenced when you do something in that table.
- For any table to speak and connect to another table it will always need the foreign key.

# Cartify Gem
- Default is "Add to cart" for clicking in Cartify.
- Background needed is "Given the following products exist: name, description and price. Finding the available attributes in the schema.rb file.
- "resources" keyword in a controller gives us access to all of the paths, but that is bad practice, we should be using the __,only: [:index]__ which gives us only the index action.
- Cartify requires the email in order to login.
## Installing
0. Add the cartify gem in the top of the gemfile because we want it to be available throught the entire application.  
1. $ rails generate cartify: install --scope assets
2. $ rails generate cartify: install --scope routes
3. $ rails generate cartify: install --scope initializer
4. This creates a lot of assets, adding requirements.
5. We will need JS in our application, to test the JS we need to add the @javascript on the very top of our feature file for that particular test (otherwise it renders w/o js).
6. Edit the resources for :products to include both [:index, :show], after cartify has added the show option.
```rb
resources :products, only: [:index, :action]
```
7. Clone the neccessary migrations
$ rails cartify:install:migrations
+ rails db:migrate
8. Add the recommended code to our User Model. 
9. Go to initializers and cartify.rb (modify if different naming conventions were used inside of our own models).
10. Modify feature steps accordingly: "And I click on "Add to cart" on "Pizza"", Then I should see "1 item".
11. Add steps
```rb
Given('I click..') do   
|element, product_name|  
product = Product.find_by_name  (product_name)    
within("#product_#{product.id}") do  
click_on element  
end  
end
```
12. expected_content (between the pipes) when looking for expected_content ist string etc
13. Will give unable to find (capybara), are all fixed inside of the views!! Inside of the Product view, add the id for products using embedded Ruby
tr id= dom_id(product)  
14. New error; 

# Mob session w. O  (re-watch)
- __belongs_to__, means that we can actually create a product from the Category.  
- means Product has an association to Category/owns something, using __has_many__ (gives us ability to call main.products.create) means the opposite: that Category has many products/Category is associated with products.  
- Generated when products_references (at the end of creating a model).
- Use "Associations" for spec for expecting Category to have many :products, and vice versa for belong_to :category for Product spec.
- FactoryBot understands if you just write the name of the model you need. 

## Partials
- Using Partials; Partial templates - usually just called "partials" - are another device for breaking the rendering process into more manageable chunks. With a partial, you can move the code for rendering a particular piece of a response to its own file.  
- Partial; only kept inside of our views. Refactored code like navbar, footer that we would use althrough our pages.
- To render a partial as part of a view, you use the render method within the view: 
```rb
<%= render "menu" %>
```
- This will render a file named _menu.html.erb at that point within the view being rendered. Note the leading underscore character: partials are named with a leading underscore to distinguish them from regular views, even though they are referred to without the underscore. This holds true even when you're pulling in a partial from another folder.  
- 

# Mid-course project
- “To find yourself, think for yourself” - Socrates
- We decide what to code, what to write, what features to implement, how to delegate assignments and which planning tools to use.
- We will start working with APIs (third party services).
- Our job is to pick an API and build an application around it: * build an application in Rails that consumes an external API. * Add authentication and authorization with OAuth like FB or Google. * Add payment gateway like Stripe. * You will design, plan and execute the development together with the group.
- Resources: Weather aAPI, Movie API, Cat API, Chuck Norris API, NASA API, Music API, Sky Scanner API, TV-Guide API.
- The API needs to be restful/have the key restful.
- We need to come up with an idea and start the design sprint during this weekend.  

## Fetch API from Rails
1. Search Chuck Norris API.
2. Copy the random joke url.
3. There are multiple ways to access an API using Rails.
4. Gem rest-client (simple HTTP and Rest client).
5. Gemfile add: ‘gem ‘rest-client’’ in ‘rails etc part’
6. Bundle.
7. Open Rails console (loads entire application for us): $ rails c
8. PRY: resp = RestClient.get(‘https….’)
9. PRY: resp.class (give resp clirent response)
10. PRY: resp.methods (shows all methods)
11. PRY: resp.body (shows the API url response) in JSON (Javascript Object Notation). It is always sent to us as a string, formatted in a specific way.
12. PRY: JSON.parse(resp.body) transforms it into a real JSON object.
13. PRY: joke = JSON.parse(resp.body)
14. PRY: joke[‘value’] can be displayed on the website.
15. PRY: joke = JSON.parse(RestClient.get(‘http’).body)[‘value’]
16. PRY: joke (displays the joke fetched from the API).
17. Outside PRY: config/routes root controller: :application, action: :index
18. app/controllers/application_controller:  (normally we would not do this inside of the application_controller but another controller): def index @joke = JSON.parse(RestClient.get(‘http’).body)[‘value’] render ‘custom_folder_name_whatever’:whatever (if you change folder and files manually) (if you dont do anything your view template needs to be in the same folder where your controller corresponds, if you do sometjng else you cannot have render blank) end
19. views/index.html.erb <%= @joke %>

# Weekend challenge (week 5)
- This weekend we are going to prepare for a “sprint review”; means we are going to finish off as much functionality for our sprint intervire:
- - Finish off as much functionality as possibke,
- Add styling and make the app presentable.
- Prepare a demonstration of the app and its functionality for monday morning.
- Deploy your app.

# Sprint review:
- Held at the end of a sprint to expect the Increment and adapt the Product Backlog if needed.  
- This is an informal metting, and the presentation of the increment is intended to elicit feedback and foster collaboration.  
- Described in the Scrum Guide.  
- The whole reason for the sprint review is to give feedback and understand what we need to do in order to improve our work flow.  
## What do we discuss?  
- The Product Owner explains what BackLog items have been “done” and what has not been done (PivotalTracker = BackLog).  
- The development team discusses what went well, and how the issues were solved. I.e. “we had a Gem that was deprecated and needed to use another Gem.” Differs from case to case basis.  
- Development team develops the changes that have been done and asks about the Increments (why was not this developed? priorities discussion).  
- Discuss the product backlog as it stands and add new targets that we need for the next sprint (revised requirements). Take them to the next design sprint.  
