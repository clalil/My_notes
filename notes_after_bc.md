# Encryption
How to encrypt an API key.

1. Fetch API key.
2. Be sure to have a master key to your repo, if not, delete credentials.yml file and run:  $ EDITOR="code --wait" rails credentials:edit
3. That opens up the VS code, with the secret key inside of it. Edit as follows:
```rb
food_api: 
  	api_key: <enter-your-api-key>
```  
Close the file in VSC, go to terminal, it should say: 
“New credentials encrypted and saved.”
5. Now your module FoodService can look like:
params: {	
	apiKey:  Rails.application.credentials.food_api[:api_key],
	ingredients: query
	}
Voila! Your api key is stored.

# If Semaphore CI fails on API Troubleshoot
- Check if routes has same namespace as folders. I.e. if namespace is :api then the controller must be in api/your_controller.rb if it is not in such a folder, or the namespace and foldernames do not match (case sensitive) it might cause the tests to fail on Semaphore CI.

## Add :key to json output
- Use AMS configuration for the initializer! Projects: foodhub, ADS.
