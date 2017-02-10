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

a. Model has dropuout layers following conv2D to avoid overfitting. Also making sure that data has equal number of left and right turns.
b. Trained the model early on with 3 cameras, and later on with only central camera data.
c. Tried using Y channel of YUV and swapping RGB channels - but didn't provide any improvements, so were aboandoned.
d. Made sure that 0 angles are not at all used to avoid bias towards driving straight.

####3. Model parameter tuning

a. The model used an adam optimizer,
b. batch size of 128,
c. samples per epoch of 15k for single camera and 45k for 3 cameras,
d. trained for 9 epochs - 4 with 3 camera data and 5 wiht only center camera data

####4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road ... 

For details about how I created the training data, see the next section. 

###Model Architecture and Training Strategy

####1. Solution Design Approach

The overall strategy for deriving a model architecture was to ...

My first step was to use a convolution neural network model similar to the ... I thought this model might be appropriate because ...

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting. 

To combat the overfitting, I modified the model so that ...

Then I ... 

The final step was to run the simulator to see how well the car was driving around track one. There were a few spots where the vehicle fell off the track... to improve the driving behavior in these cases, I ....

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

####2. Final Model Architecture

The final model architecture (model.py lines 18-24) consisted of a convolution neural network with the following layers and layer sizes ...

Here is a visualization of the architecture (note: visualizing the architecture is optional according to the project rubric)

![alt text][image1]

####3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Here is an example image of center lane driving:

![alt text][image2]

I then recorded the vehicle recovering from the left side and right sides of the road back to center so that the vehicle would learn to .... These images show what a recovery looks like starting from ... :

![alt text][image3]
![alt text][image4]
![alt text][image5]

Then I repeated this process on track two in order to get more data points.

To augment the data sat, I also flipped images and angles thinking that this would ... For example, here is an image that has then been flipped:

![alt text][image6]
![alt text][image7]

Etc ....

After the collection process, I had X number of data points. I then preprocessed this data by ...


I finally randomly shuffled the data set and put Y% of the data into a validation set. 

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. The ideal number of epochs was Z as evidenced by ... I used an adam optimizer so that manually training the learning rate wasn't necessary.
