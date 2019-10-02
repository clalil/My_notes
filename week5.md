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
