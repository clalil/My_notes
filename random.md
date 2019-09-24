# Week 2  

## BDD

BDD
= A set of practices that aim to reduce some common wasteful activities in software development - rework caused by misunderstood or vague requirements
- slow feedback cycles

BDD = working on smaller features. I.e. you are testing and creating the application the way that the user would interact with it.
The main difference between uni test and features (BDD) test = testing a small portion vs testing an entire feature/webpage.

—
How do we test what you should see on a website? Answer: Cucumber is a toolset that helps us tets what we should see on a website or what the result should be when we’re on a loading or landing page. You can actually interact with our application in cucumber.
Cucumber clicks on login for us i.e.
Manual testing: is clicking this, clicking that manually; works fine with very few users. However with many users you cannot; therefore you use automated testing (unit testing like an algorithm or connection to an API) using RSpec and feature testing/acceptance testing is used with Cucumber.

E2E training wheels testing framework run both unit and feature tests for example.

RSpec could do feature testing but then you cannot re-use the same tests as opposed to  cumcumber where you can add a scenario that is unique.

With cucumber we can have several scenario files using the same expect file; divide it up depending on the logical structure. I.e. extract admin and user files.

RSPec on the other hand has one spec for each file.

We develop for how our users are going to behave. 

When should you jump between BDD and TDD? 
Answer:  #You start with the feature tests with Cucumber. You write the entire scenario.
#2: You work on them going green. When you get an error that you cannot handle with a feature test - i.e. an computation - that is when we jump over to Rspec (we will later use this with data bases. We will not write SQL code duing this boot camp (language specifically used for databases). #3 When you run into an error that cannot be fixed with front end; you need to go back end. Then you go into Rspec, get green on those tests, and jump back into feature tests in cucumber until it goes green.

BDD = work from the user perspective. I.e. that you should not be able to click on a button until you fill in a form.
I.e. logic is that you should not be able to click a button until the form has been filled in.
When writing your features: think as a human being; this is how we are supposed to do. Then developer mode: test it and then implement the feature.

RSpec logic: you cannot create a user before you have added a user name.

The client will never know what the code will look like only what they want the code to do; your job as a developer is to translate “we want a login function” to include what you need to have as a user.

Whenever you encounter a point where you need some login: you add unit tests for that logic. Then you continute on with your feature test.

One user story for one feature test but we can have several units test for one single feature test.

—

Cucumber = for BDD we are using this. Cucumber is a way for us to write a feature test scenario and then run that test in our terminalw hich gives us an output which gives us specific steps to take (step definition) to pass.. Once passed, we more on to the next.

Local storage 
= different kind of ways to store information. One way is in the IRB (only stores during the actual session), then we store information using an YAML file (we can add and pull out information). The next logical step is to use local storage = only on the computer, then on a file, then on a browser, then on a database.
Local storage = save the information on your browser (chrome). Basically a built-in JS method which helps us save information in our browser. This also means that if we deploy our site - and another one visits - then they will not have our information because it is stored inside of our browser - he will only see his/her own information.
Local storage = when FB remembers your e-mail etc. like a “box” where the algorithm stores your data.
(Cookies are also stored in your browser)

Application tab in Chrome (session storage) = shows local storage

Before every new feature/etc create a new branch to pull in. Then create a new branch from the master branch where it is time to create a new feature, merge, pull master, new branch etc…


—
The adress book challenge:

installing mocha and chai and cucumber:

yarn add cucumber chai puppeteer superstatic --dev

yarn add cucumber mocha puppeteer superstatic --dev

Error: Cannot find module 'babel-core'
Solve: $ yarn add babel-loader@7

Server side/back-end
- Runs its scripts before the HTML is loaded, e.g. Ruby on Rails/PHP etc.
- The scripts are not run on the user computer, but on the server which hosts the website and sends down the HTML code.

Client side languages
- Runs the scripts on user computer after the page has loaded.
- E.g. when changing the innerHTML of an element, the script dynamically adds it to the HTML through running the JS code by your browser. The HTML source code itself is never changed, since it was never part of the original HTML document that was loaded by your browser.

Headless: Headless browsers are executed in memory and are mostly used in automated test environments where we need to interact with the browser. You can also configure puppeteer to use full (non-headless) chrome browser.

## Debugger    
Console => Inspect

Elements tab = contains all of the HTML that we can see on the page.
We can pick an element and click on the element to see closer.

You can cllick on the border item to add border etc.

Console =
We get all the messages and alerts from e.g. console log,
we can also write JS code and play around with the values that we’re getting.

Clicking clear console deletes everything.

Sources tab =>
Click file we suspect has the issue.
click on the numbers to add a bunch of break codes: fill in the form again to see where the code is passed
Shows scope and breakpoints. More breakpoints can be added. 

debugger
keyword inside of our code will also pause the code for us.

install: debugger for chrome if not present in VSC.

Use the sources/pry as much as possible when you get a new piece of code. 

Always when writing a webpage etc then use the source chrome debugger

Lesson 5/9 - Debugging

$gem install <rspec> (means you do not need a gemfile; i.e. touch gemfile) i.e. every gem can be installed directly from the command line.
!Still needs rspec —init (?)

Ruby
() = to pass in arguments to methods
{} = to pass an object

RSpec
before { command } 
same as 
before do command end

it { expect(described_class).to respond_to :new }

=> :new is a class method!

it { expect(subject).to respond_to :name }
= getter method
it { expect(subject).to respond_to :name= }
= setter method

=> (setter and getter are) instance methods that responds to the subject!!!

debugger gem:
gem ‘pry’
(inside of gemfile)
$ bundle
spec_helper.rb
require ‘pry’
class.rb
=> require ‘pry’

def initialize
	binding.pry
end

the command ‘binding.pry’ is used to stop the specific command in it’s place
= when you want to stop the initialization of your code

subject = self 
inside of pry (returns the very object that was created)

At the top of the 
self.methods (in pry)
it should show the methods that you are using

self.respond_to?()
=> used to test what our class and object responds to what methods

def initialize
	#binding.pry
	self.name = “Thomas”
end

=> responds to test expect(subject.name) to eq “Thomas”

self.name <=> @name

——
in JS the command for debugging is:
debugger


## Asynchronous programming  
Lesson 2 — 9/9

Asynchronous programming in JS introduction

The problem is that when we code; the processor that is responsible for executing our code will be busy. When we have multiple processes that need to be computed at the same time; then our code will stop and wait until the process is complete: kind of like a chain effect.
- Programs will often keep the CPU busy until they’re done with their work.
- Facebook: need to authorize you and bring back the authorized data.

With synchronous programming; it’s like a single chef working in a kitchen. For a single chef: he needs to prepare the starter, as soon as it is done, he starts on the main dish etc…he can’t do anything else while he is preparing one single dish. He needs to have constant control of what is going on and is blocked until he has finished one task.

Synchronous programming:
- Instructions are executed one after the other.
- A function that has a long blocking action will halt the program execution until it’s finished.
- This will stop the duration of your program for the duration of that action.

Asynchronous:
- Allows multiple things to happen at the same time.
Multiple chefs in the kitchen; one for each dish. They can make dishes simultaneously and can send dishes out simultaneously. You can make a better dessert because you are not constrained by the other chefs’ work.

Two functions are basically running; once one is completed the other one will cotinute; allows multiple things to happen at the same time. When you start a blocking action the program will carry on. When the action finishes the program will be notified and will get acess to the results.

Blocking action = means the entire program just stops and waits until the action is completed.

Using asychronous programming:
- functions are run simultaneously compared with synchronous programming where each function waits for the other function (longer running time).
Asynchronous programming => code is faster and cleaner. (the end user will probably not see the real difference, but when dealing with expensive objects that millisecond can create problems; i.e. 4 seconds loading time can piss people off.)

JS has three ways to work with asynchronous functions:
- Callbacks (outdated, not used anymore) Callback is another function that we  passed in as an argument (the raw material that we are passing into a function i.e. ‘Faraz’) to another function: Callback = another function as an argument. callback = ‘Wait until this function completes” “Callback hell” = meaning that once we starts we need to keep putting them back inside. 
- Promises (ES6) A promise is a promise: you ask for something that will be returned to you after a while… let willIgetTreteat = new Promise ( function(resolve, reject) { resolve = fix this (true path) reject = condition is not funfilled, reject this (false) i.e. the true/false is built in into the promise.
- Async/Await (ES7-8) is currently prefferred way of working with asynchronous programming. ‘Syntachtic sugar’ == a cleaner way to write a promise By placing async in front of a function it automatically makes the function asynchronous with a built-in promise. You can nest promises inside of promises. .catch = error handling what happens if all goes to hell.

Explain what asynchronous code is: 

Synchronous code is like babysitting one kid; first it runs off to the playground, then it looks at a butterfly and then it drops its ice cream.

Asynchronous code is like babysitting several kids. One kid is running off to the playground, while another is looking at a butterfly and the third just dropped their ice cream. Hence, all kids are doing separate tasks that drives you insane simultaneously.

And what async is:

An async function is a function that implicitly returns a promise and that can, in its body, await other promises in a way that looks synchronous.

Async is like telling your child that they can have a pet only if they can take care of it - you will always receive that promise.

Await is a keyword that lets you pause and resume the execution of an async function until it receives the results of a promise. Without await, while calling an asynchronous function, the function starts executing. 

Await is like calling the word “Whoever is the quietest will receive ice cream!” to a bunch of loud kids doing different things. It will make them pause for a while, allowing you to give them ice cream one at a time thus deciding when which kid is allowed to continue to do whatever they did beforehand.  

## JavaScript Functions  
Notes about javascript; introduction to ES6
We will currently work with ES5 because it iswhat is currently supported by all browsers.

What is ECMA Script?
It’s a scripting languagare specification standardized by Ecma International
These are all under the JS umbrella; any new version released will be adhereded to their version
ES5 (version) can be handled by all browsers (JS as you know it)
ES6/ES2015 Ecma Script 6 
ES7 + ES8 are new additions

ES6 aka ES2015
New features added were:
classes and modules (previously only prototypes)
constants (previously only var)
iterators and for/of loops
arrow functions
binary data
typed data (this array will only contain strings/integers etc i.e. specific datatypes)
Collections (map, sets etc)
Promises
http://es6-features.org (to find answers to any questions)

Only ES5 is supported by all browsers, ES6 is supported by some browsers (chrome, safari, opera, internet explorer edge, firefox)
Our ES6 code needs to be able to be translated into the older version ES5
In order to use JS in all browsers we need to make sure all browsers can handle it, and in some cases translate our newer code into older versions
Babel is a transpilation tool that does just that!  

## YAML  
—
Simple is better than complicated!!
—

YAML files are basically text files. We can store data in those text files in an organized manner (which is why we mainly use them)
YAML = Yaml Ain’t Markup Language
= it’s a human friendly data serialization standard for all programming languages
i.e. we can use it for any programming language like JS, Python, Ruby etc (however, how the data is accessed/extracted from the YAML file is in different ways/methods depending on the programming language that accesses it)

JSON format is similar to YAML format i.e. formats: data serialization = takes information and stores it/adds it in such a way that we can easily find a structure. Instead of a YAML you’d have to use a hash and store it inside of a logic (but since we do not wish to mix logic and data (or logic and visuals) ; we would not want to do that i.e. separation of concern). Methods would instead be stored in a logic part.

YAML
- syntax matters (A LOT. You cannot use camel case etc)
- Whitespace indentation (indentation sensitive; i.e. the gap between the spaces does matter - you need to have a specific amount)
- used for storing information (whatever that information may be: a list of customers, dishes for a restaurant etc and also needs to follow a specific structure but not like a list of methods; like items in a fridge - all you do is take items from and to the fridge).
- needs to follow a structure.

YAML format:
- :item: :title: Alfons and soldatpappan :available: true

It takes the information from a file and returns it as a (for example) Ruby hash with key/value pairs. It means that we can use different hash methods on the file. the YAML file format is standardized while the different coders/applications will have their own way of accessing it.

Writing and reading YAML
to_yaml needs to be added to a code block to add iteration w. yaml format; like
File.open(‘./lib/data.yml’, ‘w’) { |f| f.write ..}

IRB (how we do in RIB only)
require ‘yaml’
collection = YAML.load(‘./lib/data.yml’)
collection.select { |book| book[:item][:title].include? ‘Pippi’ }
(how to search for a specific title)

Find and modify first object in YAML file:
collection[0][:available] = false
Now we need file.open to save this change to the aqtual YAML file!
File.open(‘./lib/data.yml’,  ‘w’) {|book| book.write collection.to_yaml}
this takes two arguments:
first argument: text file
second argument: what to do with txt file
=> changes the actual file (but result is the characters addition amount that is inside of the yaml file)
Change back to true:
collection[0][:available] = true
=> making the data available to us
File.open(‘./lib/data.yml’,  ‘w’) {|book| book.write collection.to_yaml}
=> actually saving the changes to the data
above we need the ‘w’ and the .to_yaml to change it AND save it  

## Google it - Searching the net

90% of the job as a developer is about googling and finding the right resources.

rubygems.org = the website where you bring home the different gems from. Many people have downloaded rspec = it is a well resourced gem. Clicking on it is a way to find the most recent version. Whenever you hit an error/bug - always start with the documentation for the actual framework m.m. and not google.

ruby-doc.org
= a website for the ruby programming language itself. Look here before gooling. It is hard to read official documentation.- it is not easy!! Problem is that engineers are writing it for other engineers; which we aren’t. The only solution is to read the official documentation on a regular basis.

MDN (mozilla developer network)
= first place to read anything JS related

npmjs.com 
= official documentation/page for all open source packages that are available to us using JS.

StackOverflow
= previously there was a problem with douchebags on SO who were just being obnoxious. When looking for information on SO; ask a really specific question. Look for what date when the question was asked: if too long ago; the framework is probably updated? But if the question was asked a short while ago then it tells you that the question might still be relevant.
Upvoted answers (the answer who helps the most) is often found at the top.
Tip: don’t stop at the first answer but go through them and continute to read.

CraftOverflow
= CraftAcademys own version of SO. 

Cheat sheet
= google for them i.e. rspec matchers etc.
cheatrags.com/rspec-matchers
etc. dsl cheat sheet etc

ELI5 = explain it like I’m five
google “rspec ELI5” etc to make things very clear: for conceptual things

It is normal to forget the basic syntax when you’re not using it.

If you’re logged in when you google then the results will become better and better with time.

## Advanced Rspec

Specification = Example = Test

Spec is a testing framework that is designed specifically for the Ruby programming language. 
Definition of a spec = “An example that proposes certain expectation where Rspec tests whether or not those expectations comes true”.
We want to test a potion of our code rather than all of the connections to it.
“Given some context, when some event occurs then I expect a certain outcome”.

Why tests code: stimulates critical thinking, overcome edge cases (wrong user input; string instead of numbers, time zone, languages etc). Increases confidence during code deployment, upgrading related software, adding new features etc…) => it helps us stay confident that our code will work when we leave it to our clients.
It stimulates critical thinking by forcing you to look at problem from different angles. Also, is a quicker way to find errors/experiments.

We want to test: happy path (how the user is supposed to act), sad path (when the user doesn’t act as you want). edge cases (i.e. uncommon cases: like time zones or other alphabeth instead of default english; how should our code handle that? etc). bug fixes (making sure we get those, and not repeated).

What are expectations?
- the expectations are the heart of Rspec (we expect something to do something or not to do something). We write an expectation and see if it is met or not.
- EX: @name = ‘Hi’ expect(@name).to eq(‘hi’)

A matcher = allows you to compare different datatypes and values (eq = a matcher). The core of the matcheer is that it should match what we have on the other side.
Truthiness matchers (compare true/false values)
Numeric comparison matchers (compare numeric values)
Collection matchers (compare arrays)
Observation matchers (evaluate changes)
Predicate matchers = dynamic matchers, used for methods that return true/false and gives better error messages. can be based on custom messages.
Predicate matchers can be used instead of the built in ruby methods like odd?, nil? or integer? like some_value.to be_odd/nil
(nil? = checks if it is empty or not) These are *not* matchers.
Dynamic matchers in RSpec: expect(some_value).to be_odd/nil/integer. 
Dynamic matchers can be used with built-in ruby methods with a _?

Dynamic matchers for custom methods: def voldemort?(name)
name == ‘Tom Riddle’ ? true : false
end
expect(name).to be_voldemort 
w/o dynamic matcher: expect(name.voldemort?).to be true
Usse dynamc matchers is possible

Hooks
When you are writing unit tests, it is often convenin to run setup and teardown code before and after your tests.
Setup code = sets up or configures code before and after you run a test. It is the code that configures or ‘sets up’ the conditions for a test. Before: Code we want to run before we run our specs. After: Code we want after runnint it.
Around: Code we want during.

A test double = allows you to test your code even when it relies on a class that is undefined or unavilable.: mocks fakes spies stubs
(all above are test doubles)
- Used to make it easier to test: we have the object inside of our test feat already.
- Better to use it when we are dealing with expensive objects (e.g. when you wish to test one user from a huge database; it’s a long and expensive process i.e. an API that requires us to send and retrieve information; which slows our test suite).
- Unpredictable responses: sending emails (different time zones etc), API)

book = doubles(“book”)  = create a test double (a stand-in) account = instance_double(“Accont”, name: “Faraz”) = create an instance double (an instance of a class i.e. one object).  

## Learning statergies

Flash cards = Used to write down concepts. Brainscape etc (flashcards apps) brainscape.com (free) it works like a question: if you flip the card you get the answer.

Solve daily problems: create small applications regularly like a grocery list.

Coding diary: Write down the problems and solutions that you find on a day to day basis. Only works if you regularly read the coding diary; rehersal and follow through is the important one.

Feynman technique = explain aa topic in plain and simle language as to a child. Go over and find gaps in your understanding or explanation. Repeat. 
“If you can’t explain it to someeone then you don’t know it well enough”

Coaching others = Teaching someone that has no idea of what you are doing. Teaching others is a huge part of working as a developer. The knowledge gaps exposed when you explain something is what you need to work on.

Metaphors = Baasicallly a simplified way of explaining a concept. Like in the bible where they make a story to make.a point. Methaphors makes us pull something into the real world and explain what it means.

An instance double is like a stunt double: you want someone less important than the main actor to do the dangerous things; while still wanting the double to have the same attributes as the original version.

Pre-questioning: “what we will say next” or “what will he do next”? i.e. guess what he will do/say neext and question why did he not do/ssay that? It is away of learning and continuosly question your own knowledge.

## About programming  

“A program is a sequence of instructions that can be executed by a computer to solve some problem or perform a specified task”
- Why is our program relevant?
- What problems do we solve and why?

Full stack CA = the entire process of software development including decision making. From defining features and understanding the problem to deploying it.

In order to capture requirements we need to:
- Fully understand the problem we are solving
- Fully understand the scope of the problem (the specific part/task that the piece of code is supposed to do)

What is agile?
- Incrementally deliver working solutions.
- Help the team to step back and identify the true nature of the problem to be solved.
- Ensure that user needs are kept front and center throughout the entire design and development process.
- Support in incrementally build of the solution.
- User needs need to be kept in the center of the design process!!

What is a problem statement?
- An explicit written statement of the problem everyone has to solve.
- Working w/o it leads to a waste of time and effort.
- It is a fundamental step to set the direction of the project.
- Like if you have an elevator ride with a stranger to explain the scope of your program (the wwhy am i builing this and what is it supposed to do)
- Needs to be: written down and shared between all members, explicitly define the current state and desired state, measurable so we know if and when we acheive it, short and not overly constrained.

What are the user stories?
- An informal, natural language description of one or more features.
- The goal with defining user stories is to capture the requirements needed to deliver a solution or a partial solution to the problem definition:
- Explains what to do and sort of how to do it.
- Three components:  Stakeholder (the beneficiary of the feature) 
- Extract information from user stories: find class names, method names and desired state in your user stories.
- Example:
- As a system owner (stakeholder) In order to have visitiors order food (desired outcome) I would like to present them with a list of participating restaurants (passed functionality) system owner => role? Stakeholder/user food => object? Class? restaurants => objects? Users? Relationship with users? participating => state? perscribers of the restuaurants?  As a restaurant owner in order to have visitors order my food i would like to present them with a list of currently available dishes restuarant owner => role? my food => object w. association w a specific role? currently available dishes => object w. state? (Like we also have currently unavailable dishes).
- 
- You need a different user stories for different parts of the project. User stories can be “high level” user stories (describing a part of the entire application that is too big to work on by itself (an ‘epic’). An ‘epic’ can have “lower level” user stories that are smaller pieces of the code.
- 
- Naming is a process: - Naming is not done in a single step
- Don’t be afraid to change your mind about variable names As your system evolves the names of your classes, methods and attributes might prove irrelevant or even illogical. E.g. to name “my food” object “this” and then add “drinks” instead of naming it “a product” which makes it less specific for when you later on add new attributes:
- i.e. choose level of abstraction wise ‘food’, ‘drinks’, ‘coffee’ can just be called ‘product’
- Normalize terminology among team members. 
Further reading:
https://agilemanifesto.org/  

## Organize your code  
How do you organize your code?
- Visual layer (What the user would see; i.e. the interface of the ATM.)
- Logical layer (Conditions for using it; where all the compritations occurrs; is this the right person?)
- Data layer (Where you would get access to like the account information; the code storage where the data is kept. The logical layer needs to go to the data layer to access logical information)

Spaghetti code: “huller om buller”-kod.  

## Ruby rules

Use CamelCase for classes and modules. 

Use snake_case for symbols, methods and variables. Do not separate numbers from letters on symbols, methods and variables.

Use snake_case for naming files, directories, e.g. hello_world.rb.

Use SCREAMING_SNAKE_CASE for other constants.

No for Loops
Do not use for, unless you know exactly why. Most of the time iterators should be used instead. for is implemented in terms of each (so you’re adding a level of indirection), but with a twist - for doesn’t introduce a new scope (unlike each) and variables defined in its block will be visible outside it.

No then
Do not use then for multi-line if/unless/when.

Same Line Condition
Always put the condition on the same line as the if/unless in a multi-line conditional.

Ternary Operator
Prefer the ternary operator(?:) over if/then/else/end constructs. It’s more common and obviously more concise.
# bad
result = if some_condition then something else something_else end
# good
result = some_condition ? something : something_else

No Multi-line Ternary
Avoid multi-line ?: (the ternary operator); use if/unless instead.

No Nested Ternary
Use one expression per branch in a ternary operator. This also means that ternary operators must not be nested. Prefer if/else constructs in these cases.
# good
if some_condition
  nested_condition ? nested_something : nested_something_else
else
  something_else
end
case vs if-else
Prefer case over if-elsif when compared value is same in each clause.
# good
case status
when :active
  perform_action
when :inactive, :hibernating
  check_timeout
else
  final_action
end

Use if/case Returns
Leverage the fact that if and case are expressions which return a result.
# good
result =
  if condition
    x
  else
    y
  end

! vs not
Use ! instead of not.
# good
x = !something

unless for Negatives
Prefer unless over if for negative conditions (or control flow ||).
# good
do_something unless some_condition
# another good option
some_condition || do_something

No Parentheses around Condition
Don’t use parentheses around the condition of a control expression.

while as a Modifier
Prefer modifier while/until usage when you have a single-line body.
# good
do_something while some_condition

No Nested Conditionals
Avoid use of nested conditionals for flow of control.
Prefer a guard clause when you can assert invalid data. A guard clause is a conditional statement at the top of a function that bails out as soon as it can.
# good
def compute_thing(thing)
  return unless thing[:foo]
  update_with_bar(thing[:foo])
  return re_compute(thing) unless thing[:foo][:bar]
  partial_compute(thing)
end

Prefer next in loops instead of conditional blocks.
# good
[0, 1, 2, 3].each do |item|
  next unless item > 1
  puts item
end

No Case Equality
Avoid explicit use of the case equality operator ===. As its name implies it is meant to be used implicitly by caseexpressions and outside of them it yields some pretty confusing code.
# good
something.is_a?(Array)
(1..100).include?(7)
some_string.match?(/something/

Single-action Blocks
Use the Proc invocation shorthand when the invoked method is the only operation of a block.
# bad
names.map { |name| name.upcase }
# good
names.map(&:upcase)

Single-line Blocks
Prefer {… } over do… end for single-line blocks. Avoid using {… } for multi-line blocks (multi-line chaining is always ugly). Always use do… end for "control flow" and "method definitions" (e.g. in Rakefiles and certain DSLs). Avoid do… end when chaining.
# good
names.select { |name| name.start_with?('S') }.map(&:upcase)
# good
names.each { |name| puts name }

Short Methods
Avoid methods longer than 10 LOC (lines of code). Ideally, most methods will be shorter than 5 LOC. Empty lines do not contribute to the relevant LOC.

No Single-line Methods
Avoid single-line methods. 

Method Definition Parentheses
Use def with parentheses when there are parameters. Omit the parentheses when the method doesn’t accept any parameters.

# Week 3  
## React intro  

### React Core Concepts  
MVC model = Model View Controller  
React doesn't dictate how you handle data-related concerns; it focuses on being an easy component library.  
- React can be used for all letters in MVC:  
* React's state handles the Model. 
* Components (can store logic).  

### React intro  
http://www.reddit.com/user/Cody_Chaos  
React makes it easier to interact with the DOM w/o re-rendering the whole application.  
React is a JS library (not a framework) for creating user interfaces. React is owned in the View (We do not send out or store any data in React, this a client and is used to create clients.) We work from the library, not within the library (we do not have it automatically, and need to import React into the files).  

Semantic UI - CSS part of the 3 components of the website. Makes the website pleasing to the eye.   
HTML - The foundation of all websites and main file type loaded in the browser when you visit a website. The minimum needed to build a website.   
JS - Allows us to interact with elements and makes the website more dynamic.  
With React we get all of these three in the same file - no separation of concerns.  

JS frameworks: 
**Pros**: Better app/code structure, common concepts, large communities. (Almost any problem that you have; you will find a solution in the community).  
**Cons**: Learning curve (a specific way of coding/working) can be quite large, setup/infrastructure can be both pro and cons depending on if you do it yourself or not. Frameworks/libraries overall have a generator to schaffold applications quite quickly - less knowledge, but goes quicker to set up.  

### React  
- A JS library. Component based and declarative.  
Declarative = Not how to accomplish, but how the component should look like in it's new state.  
https://codeburst.io/declarative-vs-imperative-programming-a8a7c3d9ad2  
- "If I click on a button - I change the state of that application - if it is in a certain way then the code is rendered."  
- I.e. state before event.  
- i.e. the login form would be an own component, a nav-bar is it's own component etc.  
- Focuses on creating small, self-contained components that can be strung together to build fully-featured user interfaces (UI). 
- Basic concepts are quite easy, to 'think in react' is a special way of thinking (working component based; splitting up the parts of an application into different components).  

### React building blocks  
- 2 main principles: components and states.  
- UI will react to every change of state.  
- Components are state machines. They can also be functions.   
- Update a component's state and render the new UI based on this new state.  

Example:  
A btn can be clicked or not - depending on wheter it's clicked or not we want to show different elements. If not logged in - can't see a btn for logged in functionality.  

Class components and functional components => we can send in arguments to a component, and based on what we give the component, it will give a User Interface output depending on what we give that component.  

**import react:**
import React, {Component} from "react";
=> import component from React  

Functional component:  
- syntaxt lets you use function as component, it's effectively just the render() component.  

**ReactDOM.render {}**

### JSX Syntax  (React Markup)
- "HTML" in Javascript (not HTML but nearly identical in syntax); uses className instead of Class and htmlFor instead of 'for'.  
- A browser cannot understand what to do with JSX, so it has to be complied back to JS.  
- JSX is actually optional (but usually used since it looks like the final HTML, which is easier to read and understand).  
- Preprocessor step that adds XML syntaxt to JS (can be used w/o but makes React more elegant).  
- One of the parts that make React so powerful: how we can use JS inside of our HTML.  
class APP extends Component == class component
const MyComponent == functional component  
- In React we can't say "class" but need to say "className" when using classes.  

Example of JSX:  

```
import React from 'react';
function About() {
  return <h1>About</h1>
}

<h1 color="red">Heading</h1>
```
=> the h1 tag and it's content is JSX, in the above example.  
* Example of the above code transplied through Babel into JS the browser can understand:  
```
//HTML tag
//Null is due to no attribute set (style, eventHandler, class etc)  
//'About' is the child content here.  
function About() {
  return React.createElement('h1', null, 'About');
}

React.createElement("h1", {color: "red"}, "Heading")
```  
**Use babeljs.io to see how React components are defined.**
(create-react-apt automatically transpiles to babeljs for us)  

- React JSX supports inline style. It is done by passing a JS property object: {{}} (outer set means "I'm about to write JS in JSX", inner set means "Declare object literal").  
- Propoerties are camelCased.  
- Height in pixels are deferred (no need to specify, px is automatic).  
- Not recommended to mainly style through inline.  
- JSX tells you what line you made a typo on!  

### Virutal DOM  
- Updating the DOM is slow; hence React compares the DOM with the desired state and decides on the most efficient way to do it.  
- Abstraction of the DOM in React == DOM.  

### Rethinking separation of concerns  
- React puts the HTML into the JS.  
- As opposed to Ember, Vue and Angular.  
- Separating HTML, CSS and JS only separates the technology; not the concern. I.e. the actual concern is if the component works or not.  
- Intergrating intertwined concerns **helps** debugging!  

### Four ways to declare a React component  
1. createClass  
- Original way, works great in ES5. (no longer popular).  
2. ES class  
```
class HelloWorld extends React.Component {
  //construction if you want one
  constructor(props) {
    super(props);
  }
//Telling it which JSX to render
  render() {
    <h1>Hello World</h1>
  }
}
```
3. Function  
```
function HelloWorld(props) {
  return (
    <h1>Hello World</h1>
  )
}
```
- Simpler syntax, return statement is the render function.  

4. Arrow function  
```
const HelloWorld = (props) => <h1>Hello World</h1>
```
- You can omit the __return__ keyword if the right-hand side is a __single expression__.  
- If you have multple lines, you can wrap your JSZ in parenthesis to make it into a single expression. 
- Use __const__ to declare components in arrow functions to make sure that the constant isn't accidentally re-assigned.  

### Function Component Benefits  
- Use function components > class components:
* Easier to understand.  
* Avoid the 'this' keyword.   
* Avoids the need for binding.  
* Transpile smaller than class components.  
* Maximize signal-to-noise ratio.  
* Enhanced code completion when destructuring.  
* Easy to test (straight forward assertions during testing).  
* Increased performance.  
* Classes may be removed in the future...  

### Class or Function Components?  
- If you use React v. <16.8 it is better to use class components for state as functional components lack important features (state, refs and lifecycle methods).   
- Use function components for everything else.  

## Props and State  
- Data for a react component is held in two places: props and state.  

### Passing data as props  
- Short for properties.  
- Data is passed down from parent component to child components.  
```
function Avatar(props) {
  //if this were a class component, it would say this.username
  return <img src={"images/} + props.username} />;
}

<Avatar username="cory" />
//or pass in a variable:
<Avatar username={username} />
```
- Immutable; you can't change props because they are owned by the parent.
* Want to change a prop? Call a function provided by the parent.  
- Props are values passed from values to child (read only).  
- Props are combined into single objects.  
- The only parameter for functional components.  
- Anything can be passed as a prop (objects, arrays, functions, rendered components etc).  
this.props.name == passing props to another component.  

### Using components change  
- The second place that a react component holds data is state.  
- Unlike props, state is mutable. I.e. state is used to hold data that needs to be changed/__mutable__ over time (e.g. form fields).  
- You don't set state directly, instead you set setState via class components (or use hooks via function components).  
- Example: to access username in a state component I would use state.username in a function component, OR this.state in a class.  
- index component == parent component (the component that renders the whole application (the parent of all components)).  
- Difference between state and props (state can be changed). New props can be changed, but you cannot change the props.  
- For ES6, initial state is defined in the Constructor.  
- The state object is available as this.state and can be read from directly.  
- this.setState({someField : someValue}) == this.btnIsClicked({showLoginForm : donotshowloginform})  

Enter the following in the root folder:    
$ npm i npx -g
shows:
```
/usr/local/bin/npx -> /usr/local/lib/node_modules/npx/index.js
+ npx@10.2.0
added 484 packages from 651 contributors in 31.051s
```
==> used to schaffold the react application. NPM = used to install packages/like bundle. Gems == JS packages.  
package: createReactApp (if we do not want to install it, when we only use it to scaffold a react application).
npx => we can run reactApp w/o downloading it to our computer. We do not have to install it locally but instead call it as a command. 
The command scaffolds react-app and creates a new folder for you:  
```
 $ npx create-react-app hello_world
```
=> Should produce:
```

Success! Created hello_world at .../hello_world
Inside that directory, you can run several commands:

  yarn start
    Starts the development server.

  yarn build
    Bundles the app into static files for production.

  yarn test
    Starts the test runner.

  yarn eject
    Removes this tool and copies build dependencies, configuration files
    and scripts into the app directory. If you do this, you can’t go back!

We suggest that you begin by typing:

  cd hello_world
  yarn start

Happy hacking!
```
If any problems?? Run:
```
nvm install 10.16.3
```
VSC: Don't touch/delete the service worker!!!
Important extension to VSC:
ES7 React/Redux/GraphQL/React-Native snippets
dsznajder.es7-react-js-snippets

-----------
```
$ npm run start (starts the app)

message={this.state.message}
=> 'message' is now the 'this'.

npm start
= starts the application
```
Notice! This does not import the component, because this is not a Class component but a functional component
```
import React from 'react';
```
**quit the app**
ctrl+z

- Make a class component to be able to manage state. In a functioncal component we cannot work with state, however we *can* work with props.  

**export default App** inside of the App.js/Message.js etc file is neede in order for the index.js file to be able to render it on the HTML page as such:  
**import App from './App';**. 

```
constructor(props) {
super(props)
this.state = {
}
}
```
a better way to do the above is:
```
state = {
	<objectname>: ‘Hello World’
}
```
calling on a state:
{this.state.<objectname>}

<> is the same as DIV
</> is the same as DIV
in React (called a React fragment)
```
onChange
= used to change the content wheneve the input changes

      <input 
        onChange={this.<functionName>}
      />
= Anytime something changes inside of the <input> field, we want to call on the <functionName>.

  <functionName> = (event) => {
    debugger;
  }

=> in the console, we log: event.target
=> input
(i.e. shows what the placeholder-argument would come from)

event.target.value
=> will highlight the user value of the current input

Change the state:
this.setState({})

**Change the event to whatever the input target is (the user input)**
  inputHandler = (event) => {
    this.setState({
      message: event.target.value
    })
  }

onBlur = Changes the input field once the user clicks outside of the input field, as oppposed to change instantly.  
```
**If you only have ONE element, you do NOT need to have it wrapped within another DIV. However, if you have more elements, you need to wrap it inside of an additional div.**. 
Otherwise REACT will throw you an error inside of the browser!!
```
Parsing error: Adjacent JSX elements must be wrapped in an enclosing tag. ```. 
I.e. every element needs to be wrapped inside of another div (a parent element), hence the use of ‘react/JSX fragments’.   

Creating a new component:  
Message.js. 

The < /> is used to call upon the component f.eks:
<App />  

Yarn security threat when using older packages (eslint-utils error on GitHub):
```
yarn add eslint-utils@^1.4.1:
``
- A package manager lets you install or update third-party packages and dependencies.

- A bundler lets you write modular code and bundle it together into small packages to optimize load time.

- A compiler lets you write modern JavaScript code that will still work in older browsers

--
add node modules to gitignore through command line:  

$ echo -e "node_modules/\n.DS_Store\n.vscode\n"

one line gitlog:  
$ git log --oneline

Please note that npm i -S is the equivalent to npm install --save.  

With JSX you can write HTML code in JavaScript and have Babel transform these expressions into actual JavaScript code.
More specifically, JSX is a shorthand for calling React.createElement function.

Adding Semantic UI for educational purposes:  
—
In this project, we will add Semantic UI to our project by using CDN and referencing the necessary files from our index.html file.
—

### React Router
- React Router is the most popular routing library for React. BrowserRouter is the recommended default, but it may require additional server configuration to handle dynamic requests. HashRouter is not suitable for all situations, but it can be a good solution for static websites.  
- Splitting app into multiple pages with deep linking: use React Router. 
- Declare routes via components, specify component to load for the URL: "Load this component for this url".  
1. **Router**: Wrap app with router component/entry point (For most webapps, you want to use the BrowserRouter.). BrowserRouter uses the HTML5 history API, so that you have clean URLs. There will be no hashes in the URL. This is the recommended approach for modern webapps.  
2. **Route**: "Load this component for this URL".  
3. **Link**: Anchors. JS will capture clicks on these links, and load the requested. (Instant navigation between pages.)  
- MemoryRouter = useful for testing an React Native.  
- HashRouter (may be preferable when supporting old browsers).  
```
//Import the BrowserRouter, alias it as Router (if you want)
import { BrowserRouter as Router } from "react-router-dom";

//Wrap the app component in the router
render(
  <Router>
  //Now we can declare roots in any of this App's components
  <App />
  </Router>
  , document.getElementById("root"));

  //Using Route to declare routes:  
  (app.js file)
  import { Route } from 'react-router-dom';

(..)
<Header />
//The **Route** component takes two props: the URL to look for and the component it will load when the path matches. The HomePage has the path of "/", however this will make all other pages render as well as they start with the "/" too.
  <Route path="/" component={HomePage} />
  <Route path="/courses" component={CoursePage} />

  //Solve the above problem by adding an exact route to the HomePage, saying "This route should only match if the URL is exactly "/"
  <Route path="/" exact component={HomePage} />
```

### Links and NavLinks  
- React router offers an abstraction of anchors called **Link**. The link component creates anchors for you and allows you id:s to link it to. 
Example:  
```
//:userId == placeholder
Route <Route path="/user/:userId" />
//use JSX to create the link
<Link to="/user/1">Boddy Tables</Link>
//Anchor; clicks on the generated anchor will be handled by React Router
<a href="/user/1">Bobby Tables</a>
```
You may also use the NavLink component:  
```
<NavLink to="/users" 
//this class will be applied when the route is/users
activeClassName="active">Users</NavLink>  
```  

Add router :  

$ npm i -S react-router-dom

### Render  
- Runs when state or props change. Can return JSX, arrays, strings, boolean or null.  
- Only needed in class components; on function components whatever you return is rendered.  
--

### ESLint  
- Comes with React  
- Checks the code for issues, and reports them on the command line.  

### Why a Mock API?  
- Mock API can be used for convenience, to avoid assessing other's data.  
- Start before the API exists.  
- Helps you move indenependtly, team does not have to move at the same time.  
- No blocking issue for building UI.  
- Backup plan if API is down/broken; no stopping the development.  
- All responses are ultra-fast; no slow API calls.  
- Mock API lets you control the speed of the process.  
- Helps with automated testing; fast and reliable since API mock is local (local call).  
- Easy to point to real API later using an enivornment reference.  

### Create a mock API  
$ npm install -D... (= put this in dependencies)
JSON Server = stores data, can be changed behind the scemes (a fake data base); each time we start the app the JSON file will be generated.  

```
//React library needs to be imported to enable the JSX
import React from "react"
//ReactDom needs to be imported to be able to use the ReactDOM render method
import ReactDOM from "react-dom"
import { BrowserRouter } from 'react-router-dom'
//When imports don't have a relative path (and aren't installed dependencies/third party modules), they will automatically look for a module with the same name that you're providing, i.e. you need to specify a path to your own files/modules.
import Header from "./Header"
//Imports always assume you're importing a .js file, so the .js extension at the end is not needed, as in all cases below.
import About from "./About"
import Hello from "./Hello"
import Projects from "./Projects"
//When you have a lot of components, it is better to move them into a components folder, however then you need to correct the file path like "./components/Footer"
import Footer from "./Footer"

const App = () => {
    return (
        //JSX has to be wrapped inside of a div
        <div>
        //A component needs to return a single JSX element, to wrap everything inside of a div/other element gets you around this
            <Header />
            <About />
            <Projects />
            <Hello />
            <Footer />
        </div>
    )
};
//Takes two arguments: ("What do I want to render", "where do I want to render it"(needs to point back to the root app containder (div id="app") inside of our index.html))
ReactDOM.render((
    <BrowserRouter> 
    //Creates an instance of our functional component
    //Self-closing components do not accept child elements
    <App /> 
    </BrowserRouter>
), document.getElementById("app"))
```
When we switch between js and jsx we need to use {}:  
contact={{}}  
{Not JSX anymore} = getting into JS from JSX  
{{JS}} = the actual JS  

```
import React from "react"

function Joke(props) {
    return (
        <div>
            <h3 style={{display: !props.question && "none"}}>Question: {props.question}</h3>
            <h3 style={{color: !props.question && "#888888"}}>Answer: {props.punchLine}</h3>
            <hr/>
        </div>
    )
}

export default Joke
```js
import React from "react"
import Joke from "./Joke"

function App() {
    return (
        <div>
            <Joke punchLine="It's hard to explain puns to kleptomaniacs because they always take things literally." />
            <Joke 
                question="What's the best thing about Switzerland?" 
                punchLine="I don't know, but the flag is a big plus!"
            />
        </div>
    )
}
export default App
```
**With arrow functions - if i just have one parameter, i can get rid of the parenthesis:**
```
function App() {
    jokesData.map(joke => {
        
    })

function App() {
    const jokeComponents = jokesData.map(joke => <Joke key question={joke.question} punchLine={joke.punchLine} />)
...)

import React from "react"

import Joke from "./Joke"
import jokesData from "./jokesData"

function App() {
    const jokeComponents = jokesData.map(joke => <Joke key={joke.id} question={joke.question} punchLine={joke.punchLine} />)
    
    
    return (
        <div>
            {jokeComponents}            
        </div>
    )
}

export default App
```
**Useful Function methods**

(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce)
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findindex)  

import React, { Component } from "react"
class App extends Component
OR
import React from “react”
class App extends React.Component

* A class based component needs at least one method; in this case it’s the render() method. 
* Render() needs to return exactly what we would have in our functional component:

```
// function App() {
//     return (
//         <div>
//             <h1>Code goes here</h1>
//         </div>
//     )
// }

class App extends React.Component {
    render() {
        return (
            <div>
                <h1>Code goes here</h1>
            </div>
        )
    }
}

export default App

```
* Logic etc can go straight inside of the render method, before you do the return. i.e.:
```
class App extends React.Component {
    render() {
        const date = new Date();
        return (
            <div>
                <h1>Code goes here</h1>
            </div>
        )
    }
}
```
* Add your method inside of your class:
```
class App extends React.Component {
    
    yourMethodHere() {
        *EnterDisplayLogic*
    }
    
    render() {
*return display logic*
        const style = this.yourMethodHere()
        return (
            <div>
                <h1>Code goes here</h1>
            </div>
        )
    }
}

export default App
```
* Class vs functional components and props:
```
//function App(props) {
//   return (
//       <div>
//            <h1>{props.whatever}</h1>
//       </div>
//     )
// }

class App extends React.Component {
    
    yourMethodHere() {
        
    }
    
    render() {
        return (
            <div>
                <h1>{this.props.whatever}</h1>
            </div>
        )
    }
}
```
**Turning functional components into class componentes**
```
//#1
function App() {
    return (
        <div>
            <Header username=“vschool”/>
            <Greeting />
        </div>
    )
}

//into class components:

class App extends React.Component {
    render() {
        return (
            <div>
                <Header username=“vschool” lastname=“lastname”/>
                <Greeting />
            </div>
        )    
    }
}

//#2

function Header(props) {
    return (
        <header>
            <p>Welcome, {props.username} & {props.lastname}!</p>
        </header>
    )
}

//into class component:

class Header extends React.Component {
    render() {
        return (
            <header>
                <p>Welcome, {this.props.username} & {this.props.lastname}!</p>
            </header>
        )    
    }
}

//#3 

function Greeting() {
    const date = new Date()
    const hours = date.getHours()
    let timeOfDay
    
    if (hours < 12) {
        timeOfDay = "morning"
    } else if (hours >= 12 && hours < 17) {
        timeOfDay = "afternoon"
    } else {
        timeOfDay = "night"
    }
    return (
        <h1>Good {timeOfDay} to you, sir or madam!</h1>
    )
}

//into class compoennts:

class Greeting extends Component {
    render() {
        const date = new Date()
        const hours = date.getHours()
        let timeOfDay
        
        if (hours < 12) {
            timeOfDay = "morning"
        } else if (hours >= 12 && hours < 17) {
            timeOfDay = "afternoon"
        } else {
            timeOfDay = "night"
        }
        return (
            <h1>Good {timeOfDay} to you, sir or madam!</h1>
        )
    }
}

ReactDOM.render(<App />, document.getElementById("root"))
```

* If you want to introduce a state to a component; it has to be a class component. 
* To introduce state to a component, you need to introduce a constructor method to the class component. The constructor is used to initialize some values. 
* The first thing you should always do inside a constructor is to make a call to a global function called super(); it goes to the parent class and brings down its “goodies”. 
* To add a state to the component, you add the property to this called “state” (will always be an object.). You can access that state anywhere else in the component’s code.  
___

## Hooks and stuff  
- Note that using a constructor is optional, and you can initialize your state like so if your Babel setup has support for class fields:
- You may still need a constructor, though, if you need to use a ref. 

- Helps you be able to use functional components for nearly everything.
- Avoiding the ‘this’ confusion. 
- Uses the same react concepts (state and props).
- Tends to make React easier to understand and less likely to make mistakes. 
- Helps you share logic between components.  
- 3 most commonly used hooks: * useState (local state) * useEffect (side effects) This can be thought of as the. componentDidMount + componentDidUpdate + componentWillUnmount It accepts a function as a call. * useContext (access data in context)

Example of array destructuring: 
```
const [email, setEmail] = useState(“”)
//useState returns an array, the first element is the piece of state. The second element is the setter. ```
### Rules of Hooks. 
- You can **only** call in hooks from react function components or your own custom hook.
- Hooks must be declared at the top level (put the condition inside the hook). Because React tracks the order of your hooks.
- Render() is implied in a functional component.
- Remember to declare the dependency array [] as the second argument for useEffect() (where we tell useEffect when it should re-run!), otherwise it will rerun continuously. 

--
## Oliver



