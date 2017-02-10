#**Behavioral Cloning** 

## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
###Files Submitted & Code Quality

####1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.py containing the script to create and train the model
* ymodel.py the actual convnet model used by model.py
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* writeup_report.md summarizing the results

####2. Submssion includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
```sh
python drive.py model.h5
```

####3. Submssion code is usable and readable

The model.py file contains the code for training and saving the convolution neural network. ymodel.py shows the pipeline that was used for training and validating the model.

###Model Architecture and Training Strategy

####1. An appropriate model arcthiecture has been employed

Ymodel is a model used by Vivek Yadav, which consists of 4 2D convolution layers with 3x3 filter sizes and feature size of 3, 32, 64 and 128 respectively. Conv2D layers is follower up by 3 fully connected layers of output size 512, 64, and 16 in that order.

Conv2D layers are followed by dropuout layers, whereas fully connected don't.
All layers have RELU activation applier to their outputs.

####2. Attempts to reduce overfitting in the model

* Model has dropuout layers following conv2D to avoid overfitting. Also making sure that data has equal number of left and right turns.
* Trained the model early on with 3 cameras, and later on with only central camera data.
* Tried using Y channel of YUV and swapping RGB channels - but didn't provide any improvements, so were aboandoned.
* Made sure that 0 angles are not at all used to avoid bias towards driving straight.

####3. Model parameter tuning

* The model used an adam optimizer,
* batch size of 128,
* samples per epoch of 15k for single camera and 45k for 3 cameras,
* trained for 9 epochs - 4 with 3 camera data and 5 wiht only center camera data

####4. Appropriate training data

Used udacity provided 3 camera data.

###Model Architecture and Training Strategy

####1. Solution Design Approach

* First thing was to great a generator that could provided data indefinitely for training
* Then created a basic convnet model to train on non-augmented data to see the intial behavior of the trained model output
* At this time also deployed Nvidia model, and the result was that the car would early on drive of the track
* Also found a model used by Vivek Yadav and used it as well - 
* Got the suggestion of using 3 cameras from slack channel and used it. This turned out to be much better but car would still wonder off.
* Adjusting batch size and epochs resulted in a much better driving, but the car won't make past the curve after the bridge, as the curve is a sharp right turn.
* On looking at a video of the udacity data on youtube it was obvious that there are more left turns than right turns to train on. Which was solved by flipping the images to generate equal number of left and right turns.
* On training on flipped data car was able to drive much better but would still jump into the lake.

####2. Final Model Architecture


