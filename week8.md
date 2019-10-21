# NewsRoom Challenge (building an SaaS application)  
- Produce a digital newspaper.
- News is defined in the first room here.
- Build a fully featured news platform.
- Project time is 3 weeks.
- Sprint lenght is 7 days.
- Practice more advanced strategies with continuous deployment, and more advanced Rails concepts like Action Mailer, Active Storage and ActiveJob. 
- Make use of Geolocation and analytics.
- Build more engaging user interfaces.
## Definition of an MVP
- A version of a new service or product which allows a team to collect the maximum amount of validated learning about customers with the least possible effort.
- The MVP (Minimum Viable Product - the minimal to make the application going) can be further developed to a complete web application w/o having to design it from scratch.
- For us, RoR is suitable both for low cost prototype development and for developing fully featured web applications.
## Core principles of Agile
- Working software is the primary measure of progress.
- Deliver working software frequently, from a couple of weeks to a couple of months, with a preference to the shorter timescale.
- Our highest priority is to satisfy the customer.
- An approach that embraces change; welcoming changing requirements even late in the development. Agile process harness change for the customer's competitive advantage.
- Develop a business oriented approach. Business people and developers must work together daily throguhtout the project.
- The project must make sense from a business perspective; that we are focusing on the right things at the right time.
- "Don't think as developers first-hand, think of people who are building an application for the first time".
## Cross functional teams
- Groups people with different functional specialities or multidisciplinary skills, responsible for carrying out all phases of a project from start to finish.
- Cross-functional: representatives from the various functions in a development team. As opposed to functional expertise (system analytics, developers, testers...). Nowadays, everyone is part of the team with their expertise like UX Designer, TDD expert, programmer etc...
- We are going to work with project management tool Pivotal tracker again.
- We will work with the user stories again.
- We will build this with an API and React Client. The current stories, these are "pointers" at the moment to set the direction to move towards.
- First challenge: rewrite the stories to represent both the backend and the client side. 
- All of the stories are important and should be implemented first.
- Further on we can add more stories, but these ones are the most important part of the MVP. "Implemented at the very least, a scoped version of the feature."
- One PR per chore!!!!
## Engaging user interfaces - going mobile
- Make sure to consider all of the options on the client side.
- We can either build our mobile application into an Ionic App (we wrap the application inside of the framework Ionic that will help us build applications that will be hosted both by macos and android), React framework will build native applications for android and apple.
- Mobile application != responsive website.
### Challenge: build an end-to-end news creation, production, curation, distribution and publishing platform for localized news.
- Create news, display and delete them.
- Location; if in Sweden see swedish news, not from Ukrain or China and view them in my own language. I.e. relevant news and correct language.
- Different categories; i.e. today I want sports and not politics. Be able to filter or see news in a good way.
- Monetization; how do we make money from this application?
- Multiple language support.
- Administration/moderation; someone needs to be able to check the articles our before publication. 
#### The Paywall
- A big part of the NewsRoom Challenge is about monetization. As developers, we need to understand the underlyng business the applications we build support. This challenge is about that.
- As you browse around the various publishing sites, you'll notice that there are many different wats to implement a paywall solution (f.eks on aftonbladet you have to pay for a subscription to extra content), as well as how to build a user interface that is inclusive and provides a good user experience (UX). Another experience is WallStreet where you pay after a certain amount of free articles.
- The monetary stratergy depends on the market.
- Make sure to research before deciding on a specific stratergy. Hybrid model? A pwaywall is a requirement.
## Deployment
- Deploy to Heroku and use that servering during development (staging).
- For production, we will create and deploy to Digital Ocean (www.digitalocean.com).
- Challenge time: week 8, 9 and 10.
- Coach support: the coach is supposed to be a team member and treated as such.
- Coach meetings: at least 1 during the project and a final delivery meeting. But form your own stratergy.
- Deploy the final application individually from your own repos.
- Sprints: if you follow Scrum; 7 days.
- Deliveries: Depending on the project managements method you choose. Form your own strategy.
- Requirements: meet them in a creative way. If a client has asked you to do certain things; they need to get what they want. You need to be mindful that you have the user perspective and the perspective of the client.
- Always be able to answer why you have prioritized in a certain way. 