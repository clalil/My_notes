# API  
## How to consume an API  

```rb
#Add rest client Gem
require 'rest-client'
# We can call upon a model in our controller (recipes_controller.rb) to keep it skinny
def index
 @recipes = FoodService.get_cheese
end

# Create 'services' folder inside of controller folder
# Add food_service.rb file
#Inside of that file, add: 
require 'rest-client'
require 'json'

module FoodService
def self.get_cheese
  #You can use binding pry here to see how the module goes to the controller to check the class method
  response = RestClient.get('url#PassAPIKEyHere')
  recipes = JSON.parse(response)
# Above used to fetch the API data
# call on the array:
  recipes['recipes']
end

#index.html.haml
- @recipes each do |recipe|
  %h2= recipe['title']
```
## Gem webmock
- An API can be expensive to use and therefore we might want to stub our API response instead.
- 'webmock gem'
- 'gem install webmock'
- Add to development/test as 'gem webmock'
- require it under cucumber/rails in the cucumber main file (env.rb)
- Before '@get_cheese' do (disable webmock).
- Add @get_cheese above feature test line (means the feature will look inside of the env.rb file to check what we want it to do before it runs the test).
- Webmock.allow_net_connect! (allows webnet calls for the actual api and is disabled by default.). 

# Authentication & Authorization  
## Who is using the system and what are they allowed to do?  
- Login (default state is to come in and bring authorization documentation to prove who you are, using login credentials).  
## Authentication
- A process that helps us to verify the identity of someone who uses our system.
- OAuth providers (facebook, google, bank-id etc) helps us delegate authorization decisions across a network of web-enabled applications and APIs.
- Answers the question: "who is our user?".
- In Rails "cancan" and "pundit" are used for user authentication. None of them contains error handling.  
## Authorization
- A process to help us specify access rights/priviliges to resources related to information security in general. I.e. who is allowed to edit/create/delete? Who is only allowed to read?
### Devise
- A complete MVC solution based on Rails engines.
- Allows multiple models.
- Modular elaborate: only use what you really need.
- Extendible with many models.
- Well documented.
- One of many other user authentication gems, can sometimes be overkill if too simple of an app.
- "One of the most idiotic things to do is to store passwords in plain text and not encrypted."
- Warden is an underlying library that Devise builds upon. With this helper we bypass the entire user interface which is logging us directly into our application.  
```rb
#When you have a possible ambigious match, i.e. you add the 'on' as optional
Given("I click {on}{string}") do 
  |element_text|  
if @article
  within("#article_#{@article.id}") do  
  click_on element_text
  end
else 
  click_on element_text
  end
end

Then("I should not see {string}") do |expected_outcome|  
if @article.nil?
expect(page).not_to have_text expected_content
else 
  within("#article_#{@article.id}") do  
  expect(page).not_to have_text expected_content
  end
end
end
```  

Helper method,; if you want to get errors that are on the specific object you can call to_sentence on it to create a string with those errors messages.
```rb
comment = Comment.find(:params[:id])
redirect_to root_path, notice: comment.errors.full_messages.to_sentence
```
- If you have flash messages; running "Then show me the page" in cucumber can be used to view flash message..
- "Given I'm/I logged/log in as..." to use the same steps.
**Adding authentication right to comments**:
'rails g migration AddUserToComments user:references'
__generates__ 
(reference user to comments table) 
__add_reference :comments, :user, foreign_key: true  
**Then you need:**
(Business rule now is to be logged in before leaving a comment)
__rails db:migrate__
class User: has_many :comments
class Comments: belongs_to :users + :articles
! Requires you to add the before_action :authenticate_user
```rb
def create
  article = Article.find(params[:article_id])
  Comment.create(comment_params.merge!(article: article, user: current_user))
  redirect_to root_path
end

def destroy
  comment = Comment.find(params[:id])
  if comment.destroy
  #if comment.user == current_user && comment.destroy
    redirect_to root_path, notice: 'Your comment has been deleted'
  else
    redirect_to root_path, notice: comment.errors.full_messages.to_sentence
  #redirect_to root_path, notice: 'You are not allowed to perform this action'
  end  
end
```
- "A check before the action"; if the comment is destroyed and that action is taken by the actual creator of the comment, the first path is true.
- 'if comment.user == current_user && comment.destroy' is the actual authorization.

## CanCanCan
- Restricts what resources a given user is allowed to access.
- Build around the idea of assigning abilites.
## Pundit
- Minimal authorization through OO design.
- Provides a lot of helpers and methods.
- Add a role to our users in cucumber; visitor and moderator.
- 'rails g migration AddRoleToUsers role:integer' produces:
```rb
add_column :users, :role, :integer
#in the new class AddRoleToUsers
```
- Add to User model: 
```rb
after_initialize :set_default_role, if: :new_record?
enum role: [:visitor, :moderator]
#enum role: %[visitor moderator] also works, a different way of getting an array
```
- Now the if statement for destroy action needs to be altered as well:
```rb
def destroy
  comment = Comment.find(params[:id])
  if (comment.user == current_user || current_user.moderator?) && comment.destroy
    redirect_to root_path, notice: 'Your comment has been deleted'
  else
  redirect_to root_path, notice: 'You are not allowed to perform this action'
  end  
end
```
- The above code snippet will eventually become very hard to maintain, therefore we need to refactor it:
```rb
def destroy
  comment = Comment.find(params[:id])
  if can_perform_destroy?(comment) && comment.destroy
    redirect_to root_path, notice: 'Your comment has been deleted'
  else
  redirect_to root_path, notice: 'You are not allowed to perform this action'
  end  
end

def can_perform_destroy?(comment)
  (commen.user == current_user || current_user.moderator?)
end
```
- The above is still not an optimal solution, which is where __Pundit__ comes into play.
1. Add the gem to our dependency list inside of our Gemfile:
```rb
...
gem 'devise'
gem 'pundit'
...:test
```
2. Bundle!
3. rails g pundit:install
4. rails g pundit:policy comment
5. Go into created file and remove the policy (not needed at this stage). 
6. Cd into the CommentPolicy and add our method:
```rb
def destroy?
  @record.user == @user || @user.moderator?
end  
#Equivalent to the destroy method in the control action
```
7. Update the application controller to include Pundit by adding the line __include Pundit__ inside of it.
8. Update our CommentsController again:
```rb
def destroy
  comment = Comment.find(params[:id])
  authorize comment, :destroy?
  if comment.destroy
    redirect_to root_path, notice: 'Your comment has been deleted'
  else
  redirect_to root_path, notice: 'You are not allowed to perform this action'
  end  
end
```
9. Tell the application controller to rescue the error when a user tries to do something he/she is not allowed to do. Hence, add the following lines to the ApplicationController:
```rb
include Pundit
rescue_from Pundit::NotAuthorizedError, with: :user_not_authorized
private
def user_not_authorized
  redirect_to rooth_path, notice: "You are not allowed to perform this action"
end
```
- 

## OAuth
- A provider cares for the actual authentication.
- Smoother UX (especially for mobiles).
- Fairly well documented (omniauth).  

# [Params](https://www.youtube.com/watch?v=y57OnWV6dRE)
- The params hash is a collection of data that comes through your application in that request (from a form submit, a chunk of the url might contain some data or contain get request parameters); common ways to get data into the params hash.  
## GET
- create a simple route, controller (that inherits from ApplicationController) and give it an index.
- Add %blog to index page to view the blog path.
- A GET request query parameter; ?test=1 ("Here's some extra data, you can use it or choose to ignore it).
- @test = params[:test] would be the test variable from the query request and could be showed in the index.html file using @test variable as a params key.
- REally good for filters like blog posts.
- Putting things into a URL is basically how we get a GET request.  
# #Route PARAMs
- Using :id is telling Rails that the part that is typed into the URL should be taken in and saved to the id key inside the params hash.
```rb
'get '/blog/:id', to: 'blog#show' is telling rails
```
- The '/' is telling the search engine that the content is related to a different page on the same blog; completely different. While using the query it is telling the search engine that it is content from the page.
```rb
get "/blog/", to: 'blog#index'
get "/blog/":id, to: 'blog#show'
def show
  @id = params[:id]
  @test = params[:test]
end

<%= @id %>
<%= @test %>
localhost:3000/blog/asdf?test=1
#shows both id as 'asfd' and test as '1'
```
- Both filtering in from a query paramter. 
## POST/PATCH/UPDATE/DELETE
- Third way to get data into our params hash.
- Are all designed so you submit data into the server, that is immediately taken into the params hash.
```rb
<%= text_field_tag :title %>
#The params value of :title is made by yourself and Rails matches them up, the values affect how they are shown in the params hash in the log for rails server.
```

# OAuth
```rb
#feature/usr_can_log_in_fb.feature

Feature: User can log in using their FB credentials
  As a user
  In order to simplify the sign up/sign in processs
  I would like to be able to authenticate myself using fb

Scenario: Visitor clicks on 'Login with FB' and gets authenticated
  Given I visit the landing page
  When I click on 'Login with fb'
  Then I should be on the home page
  #expect(current_path).to eq root_path
  And I should see 'Successfully authenticated from fb account'

#index.html.erb
<% if user_signed_in? %>
<%= link_to `Logged in as: #{current_user.email}`, root_path%>
<%= link_to 'Sign out', destroy_user_session_path, method: delete %>
<% else %>
<%= link_to 'Login with FB', #link is given in rails routes after installing gem
'user_facebook_omniauth_authorize_path' %>
<% end %>

#Go to the User model, add:
:omniauthable, omniauthproviders: [:facebook#, :google, :github]
#Gives us extra routes in our rails routes

#Go to routes to tell devise we want to handle the call backs
devise_for :users, controllers: {
  omniauth_callbacks: :omniauth_callbacks
}
#Any callbacks will be handled by omniauth
#Create new controller: omniauth_callbacks_controller.rb and enter the manual information needed accordingly:

class OmniauthCallbacksController *<* Devise::OmniauthCallbacksController

def facebook
 @user = User.from_omniauth(request.env['omniauth.auth'])
 #a model we need to create ourselves. Inside of the request..is everything that we are getting from facebook about the user. the request.env we're calling on the env method/@env inside.

 if @user...
 #devise method 
 else session..
 #redirects us to user registration path

#Snapshot #1 insert

#We inherit all of the functionality from the DeviseController itself, that is why we should *not* generate views with DEvise, as we get them automatically. We only would like these files if we would like to modify them in any way.

#Now go to config/initializers/devise.rb, configure the omniauth for devise:
Devise.setup...
#connecting routes
config.omniauth :facebook
...
#How to use fb as a developer; on your own account you need to specify yourself as a developer and add a bunch of stuff..but omniauth has some methods to help us test this.

#Go to feature folder, env.rb file, add:
Before do
  OmniAuth.config.test_mode = true
  OmniAuth.config.mock_auth[:facebook] = OmniAuth:AuthHash.new(OmniAuthFixtures.facebook_mock)
  #A module we will add, like "Cocktailservice"
end

#In support-folder: add new file called omni_auth_fixtures.rb
module OmniAuthFixtures
#A module is basically a class with methods, where we can extract functions/objects from it.
  def self.facebook_mock
    {
      ...
    }
  end
end
#we will go into tokens later down the line, overkill now. 

#Time to define from_omniauth inside of our User Model

def self.new_with_session...
#error handler
def self.from_omniauth...
#pass in omniauth.auth as the 'auth' argument.
# finds or creates the user
#devise generates a random password for the user
#Atm the only information we use from fb is the user email.

#Need to add the provider from omnioath fb to our user model (uid is sort of an advanced id, provider is how the user got created basically; email is the first one and facebook can be another, as in this case)
$ rails g migration AddOmniAuthToUsers provider:string uid:string
$ rails db:migrate

# Go into FB as developer

#Go into master.key
facebook:
  app_id: 2426..
  app_secret: ''

#Reference keys in devise.rb
Rails.application.credentials.facebook[:app_id],  
Rails.application.credentials.facebook[:app_secret]

# Will be blocked, needs to be pushed to Heroku. The app needs to be added as a valid url to fb.

#$git push heroku oauth:master (pushes the entire oauth (any named branch, in this case "oauth") into the master branch)



```
- When using OAth we get redirected and give permission to use the application. 
- The Gem **gem 'omniauth-facebook'** is used in production as well as for this purpose. This only gives us facebook; google etc has its own omniauth gem. However, devise is always needed.