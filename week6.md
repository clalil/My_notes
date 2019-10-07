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