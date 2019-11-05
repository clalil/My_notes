# React Native (Building mobile apps)
- This is an individual challenge; eveyone needs to build a mobile client as well.
## Background
- Android or IOS? Image that we're running a SaaS business; this means we are going to need a mobile app for our services so we can easily take advantage of the growing monbile market.
- There are a lot of people using Android and IOS. Both are popular devices. We need to hire developers that know both java and kotlin (a version of java) and know how to make mobile apps (android) on swift for IOS.
## React Native
- Is an open source mobile application framework. This framework uses JS to create native mobile applications for both IOS and Android. This means that our developers only need to know React and JS in order to build applications both for Android and IOS. This means we can extract our existing code base into a mobile application.
- React Native born from a hackathon. The problem was that the user base was huge. They realised that hybrid applications did not give them the user experience that they wanted. The native experience means that the code is built on native code, which gives a better flow and UX.
### Why React Native?
- Uses native components and APIs; this means that it will use native componentens in spite of us using JS. A native component is "stuff that already comes with it" i.e. already written in swift or kotlin. I.e. we can use that code that already exists.
- Open source: a huge community where the FB core team always works on improvements.
- Reusable code; basically we only need to write it once and it will work both in android and IOS devices, more or less. However, when using the camera feature etc (xtreme things) you need to write the actual native code.
- Simplified UI; less response time.
- Third party plugin support (like google maps etc)
- Ready made solutions and libraries (like chat functionality and calendars etc). 
- Drawbacks are: It's still being developed and not as stable as we would like it to be. It has occurred that some previous releases have broken the active the application. Also, when we use our components we need to tinker with the native components (for camera experience) might cause issues i.e. with a recent change in IOS for camera upgrade etc.
### Why called React Native?
- First of all; React is a library while React Native is a framework.
- This has implications: React Native has a set table and tools on how we are working. But the library is designed as you can pick and choose the tools that you want.
- I.e. While React Native has built-in tools that we use directly in the application. React does not. 
- React Native does not use HTML to render the application. While React is built for the web; React Native does not as it is built for mobile devices and not the web.
- We need to use a simulator to pre-view our application instead of viewing in in localhost. We have two simulators we use Android Studio (linux) and for Mac we use (X-code) to view our rEact Native apps. I.e. it gives you not only how it will look nbut also how it will behave.

## Alternatives to react native
- Ionic; similar to React Native that it builds apps for both android and ios. The difference is that ionic creates hybrid applications. Hybrid applications is created with HTML, CSS and JS and then creates a **wrapper** which runs your regular html etc inside of a mobile application. This makes developing easier however the wrapper slows down the performance of the application. Howeverm, it is always better to have native components that work directly with your devices.
- Flutter; a framework backed by Google. The main difference is that Flutter uses a programming language called "Dart". While React Native creates/translates into native components; flutter translates your entire code into native code.

## Expo CLI
- React Native is huge, but the problem with that is that is can quickly become too much to handle. Like how Rails is good but there are so many things you can do.
- In order to minimize the things we can do with React Native we use something called Expo; it's a framework within a framework with tools built around React Native. It hinders you from a lot of configuration, built everything from scratch etc. Set up is quite easy as well as sharing the app. You do not have to create builds and basic tools are already added. You can always eject your Native application from Expo to work with React Native. I.e. it does not hinder you to stay always in the framework.

```js
import { View, Text} from 'react-native'
<View style={styles.container}>
<Text style={styles.intro}>Hello World!</Text>
</View>
//instead of using <div> etc
//styling is also different; we cannot use stylesheets in React Native
const styles = StyleSheet.create({
  bigBlue: {
    color: 'blue'
  }
  }
})
```

# Mobile implementation (React Native)
```js
>$ npm install expo-cli --global
>$ expo init native_demo
//Choose blank application, use yarn, add name

//yarn start gets the expo start commands on yarn install

//Open up app.js to start working on app!

//We have a stylesheet for every component and create a hash and a key to use it. To find out what you can use to style, visit React Native homepage.

//New folder called Screens
//Inside of that folder called Home
//Inside of that HomeScreen.js

//Services folder (same folder as Moduels folder inside of ours)

//Use backend w(o image attachment to avoid complicating)

//yarn add axios

//Avoid constructor/props from course material. Just use state.

//display in a list, use flatlist, it is basically a list element to use.
<FlatList 
data={this.state.articles}
renderItem={this.renderArticles}
//renderItem is a type of iterator that will call upon it X times depending on the # of articles we have
keyExtractor={item => {item.id.toString()}}
//we do not want it as an integer "for some reason"
/>

renderArticles = ({ item }) => {
  const article = item
  return(
    <View>
    <Text>{article.title}</Text>
    <Text>{article.content}</Text>
    </View>
    //view tag is similar to a div tag
  )
}


```