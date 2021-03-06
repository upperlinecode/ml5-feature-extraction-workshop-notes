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
3. Using the feature extractor, we now need to create a new classifier - this is where we're going to be sending the pictures we take with labels so that the model can get trained. (also makes sure to declare the classifier and featureExtractor variables up top. Notice that there is a callback here to `videoReady`, which we also have to declare.

```
  classifier = featureExtractor.classification(video, videoReady)
```
```
function videoReady(){
   console.log("video ready")
}
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
let trainAndPredictButton;
let countA, countB;
```

6. Let's populate these variables in the `buttonSetup` function:

```
function buttonSetup(){
  //We start our counters of training images at 0
  countA = 0
  countB = 0
  
  // Set the input DOM elements to the variables created.
  inputA = select('#inputA')
  inputB = select('#inputB')
  
  // Set the capture buttons to the variables created
  
  buttonA = select('#buttonA')
  buttonB = select('#buttonB')
  
  // Select the train+predict button
  trainAndPredictButton = select('#train');
   
}
```

7. Ok, now for the fun stuff. When we click on the training buttons, we want the classifier to take a snapshot of the video at that time and label it with the name we've put in in the input. Let's do that for the A button and input. First make sure that you can see the button get clicked

```
buttonA.mousePressed(function(){
  console.log("the button was clicked")
})
```

8. Now let's feed the value of `inputA` to our classifier when the button is clicked. We do this with the addImage() method.

```
//remember that this is inside of buttonSetup

buttonA.mousePressed(function(){
    console.log("the A button was clicked")
    classifier.addImage(inputA.value())
  })
```

9. We also want to increment our image counter for that variant by 1, and update the HTML containing that number.

```
  buttonA.mousePressed(function(){
    console.log("the A button was clicked")
    classifier.addImage(inputA.value())
    countA++;
    select('#countA').html(countA)
  })
 ```

10. Do the same thing for button and input B!

11. Now let's turn to training and prediction. We want this to happen when we click the train and predict button. Also in buttonSetup, when the trainAndPredictButton is pressed we want to start training using `classifier.train()`. We also will want to show the loss as the model is getting trained.

```
 trainAndPredictButton.mousePressed(function() {
    classifier.train(function(lossValue) {
      if (lossValue) {
        loss = lossValue;
        console.log(lossValue)
      } else {
        console.log('Done Training! Final Loss: ' + loss);
        classifier.classify(gotResults)
      }
    });
  });
}
```

12. The last line of the else statement above calls the `.classify` method, which then runs a callback method that we'll call `gotResults`. This is an error first callback that looks like this:

```
function gotResults(err, data){
 if(err){
   console.log(err)
 }else{
   console.log(data)
 } 
}
```
We log the error if the result is the error. Otherwise we print out the result (labeled data). If we stop here and run this you will only get one prediction... If you want it to be continuous, then you need to re-call the classify method which takes us back to gotResults, in a continuous loop. Here's how to do that:

```
function reclassify(){
   classifier.classify(gotResults)
}

function gotResults(err, data){
 if(err){
   console.log(err)
 }else{
   console.log(data)
   reclassify()
 }
  
}
```

13. Use that data variable however you want in your P5 Sketch.. FINISH...
