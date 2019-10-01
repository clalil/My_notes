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
