# Styling with CSS  
## Semantic UI tools  
Go to the website [semantic-ui.com](semantic-ui.com) can be installed through node (when using React we need node to help us download the stylesheet into the right folder), a CDN (content delivery network, which is used for smaller projects) or download and host the stylesheet directly to our local computer (this method is used for larger projects). However, to download the stylesheet takes up a lot of memory space.    

The stylesheet is hosted on different servers, it's the content delivery network sharing the same style sheet for us. However, this needs a working internet connection.  

### Installing the semantic UI using CDN  
1. Go to [Semantic-Ui](https://cdnjs.com/libraries/semantic-ui) and [copy the link](https://cdnjs.cloudflare.com/ajax/libs/semantic-ui/2.4.1/semantic.min.css) into the HTML head tag as: 
4. <link rel="stylesheet" href="link_to_stylesheet"> 
5. Go back to semantic-UI main website and look for something to add in the tabs like 'button'. 
6. Click on the item of choice and add the source code to your HTML file.  
7. Since all of Semantic UIs uses classes, we need to change the class selector to an id-selector for all of our JS code.  
8. Whenever you change your style using Semantic UI to your HTML document, you need to run __$ yarn run build__ or all your tests will fail!  

There are more tools like Semantic UI that works the exact same way, however Semantic UI is the most React Friendly Semantic UI that is out there.  

Semantic UI use JQuery a lot (which is an older Library that is not as compatible/needed anymore) you should rather use vanilla JS to create animations etc.  

Avoid JQuery and any dependencies related to it.  

In an application the Semantic UI in the app.js will add the styling between the backticks ``.



