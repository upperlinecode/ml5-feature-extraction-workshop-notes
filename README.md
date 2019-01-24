# ml5-feature-extraction-workshop-notes
Teacher Notes for Using Feature Extraction with ML5

Start off by talking about what machine learning is. How do we train them? In this workshop we'll be using a a pre-trained model called MobileNet that can classify objects. We're going to peel away the classification piece and instead build our own classifier by adding our own training images to the model and using the feature extractor functionaliy (discuss features as abstracting or boiling down images to their essence). 

Head to our starter code, [found here](https://glitch.com/edit/#!/feature-extraction-starter-code).

We've built out HTML and CSS, and started us off with capturing the video and displaying it on the canvas. We also have inputs, buttons, and a status bar. Notice that the video is saved to the variable `video` for use later.

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
3. Using the feature extractor, we now need to create a new classifier - this is where we're going to be sending the pictures we take with labels so that the model can get trained. (also makes sure to declare the classifier and featureExtractor variables up top.

```
  classifier = featureExtractor.classification(video, videoReady)
```

4. Let's set up all of the functionality of the buttons and the inputs. This is the core of the coding, and we could do it in the setup since it only needs to run once. But that will get messy, so I'm going to create a new function called `buttonSetup` and call it from the setup function.

```
function buttonSetup(){

}
```

5. So let's think about the variables we need and start declaring them up top: variables to hold the inputs, variables to hold the buttons, a variable to hold the prediction, variables to keep track of the counts of trained images (optional).

```
//variable declaration space
let video;
let inputA, inputB;
let buttonA, buttonB;
let trainButton;
let countA, countB;
```
