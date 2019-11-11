# Testing in Enzyme

## Rules for final project  
* components and reducers subfolders in __tests__ folder
* our folders to user snake_case
* folder name lower-case lettering
* components always named PascalCase with suffix .jsx
* specs are written in camelCase.spec.js
* if it is pre JS (modules, not returning jsx) add .js suffix and naming is done with camelCase.
* css-files use kebab-case i.e. list-recipes.css

```js
>$ yarn run eject
//Leave React create app safetly to run the code outside

//in enzyme we have to mount the component when using Redux, if we do not isolate our unit test it becomes an integration test i.e. if we import the actual store

//if we mount redux it will return an array hence we need to look for the .first() one otherwise the test will return two versions; one from redux and one from the html

//simulate click; .simulate('click') and .simulate('blur')

//Run a specific test in Enzyme: press 'p' and write first letter of component to test + 'enter' to run one
// Press 'w' to open menue "Watch Usage"
//If going by test name it is the name inside of the it blocks; "changes" will show the options to navigate between. If inside of a component, run 'w' again to find the actual test based on its name.

//We want to use a library when testing to avoid using out real store "redux-mock-store"
//import configureStore form 'redux-mock-store'

//console.table(action) inside of greetingsReducer.js in the case statements, we can see in the enzyme tests what the type and payload are. or console.table(state)
//console.warn('i am in the greetings reducer') then the output is yellow in the terminal or console.error shows it as red
```

## Meeting with Oliver (Day 1)
1. Create a recipe and list all of the recipes
2. Edit their own recipe.
3. Show page for a specific recipe.
4. Functionality of forking (copy existing) a recipe and make changes to it. (We need a user model first when we need to fork a recipe).
6. Generating of a PDF (important!)
7. Search for recipes (elastic search)
8. Add Oath with Facebook
8. (Not AS important; comment on recipe or rate them)