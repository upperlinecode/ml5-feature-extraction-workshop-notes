# ml5-feature-extraction-workshop-notes
Teacher Notes for Using Feature Extraction with ML5

Start off by talking about what machine learning is. How do we train them? In this workshop we'll be using a a pre-trained model called MobileNet that can classify objects. We're going to peel away the classification piece and instead build our own classifier by adding our own training images to the model and using the feature extractor functionaliy (discuss features as abstracting or boiling down images to their essence). 

Head to our starter code, [found here](https://glitch.com/edit/#!/feature-extraction-starter-code).

We've built out HTML and CSS, and started us off with capturing the video and displaying it on the canvas. We also have inputs, buttons, and a status bar.

Where we go from here:

1. Let's load in the feature extractor model from mobileNet.

```js
  featureExtractor = ml5.featureExtractor('MobileNet', modelReady);
```

2. Now we need to create a callback function `modelReady` that gets called when this has been loaded (lot's of callback functions in this project so things happen in the right order!). In the function, console.log a message, and also update the status from the status span.

```
function modelReady(){
 status = select('#status')
 status.html("Feature Extractor Loaded")
 console.log("loaded feature extractor")
}
```


