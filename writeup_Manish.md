#**Traffic Sign Recognition** 

##Writeup

---

**Traffic Sign Recognition Project**

[//]: # "Image References"

[image1]: ./WriteupSupport/explore.png "Visualization"
[image2]: ./WriteupSupport/sample.png "Sample"
[image3]: ./WriteupSupport/processed.png "Processed"
[image4]: ./WriteupSupport/download.png "Traffic Sign"
## Rubric Points
###Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
###Writeup

###Data Set Summary & Exploration

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is **34799**
* The size of the validation set is **4410**
* The size of test set is **12630**
* The shape of a traffic sign image is **32x32**
* The number of unique classes/labels in the data set is **43**

####2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the complete data set. It is a bar chart showing how the Training, Validation and Testing data is divided.

![alt text][image1]

#### Sample of data Images:

![alt text][image2]

###Design and Test a Model Architecture

####1. Preprocessing Data:

As a first step, I decided to convert the images to grayscale because it helps to normalize the input image. Next step was to normalize the image *histogram*, as different images were with different exposure. I used CLAHE method, as the different portion of image could be at different exposure.

Here is an example of a traffic sign image before and after grayscaling.

![alt text][image2]

As a last step, I normalized the image data to generate a dataset with equal mean and variance.

Here are some image after preprocessing.

![alt text][image3]

The difference between the original data set and the augmented data set is the following:

- [ ] Signs in the images are evenly visible 

- [ ] Darker images from Training set can be seen lighter



####2. Mode Architecture:

My final model consisted of the following layers:

|      Layer      |               Description                |
| :-------------: | :--------------------------------------: |
|      Input      |            32x32x1 Gray Image            |
|   Convolution   | 1x1 stride, same padding, outputs 28x28x6 |
|      RELU       |                                          |
|   Max pooling   |      2x2 stride,  outputs 14x14x16       |
|   Convolution   | 1x1 stride, same padding, outputs 10x10x16 |
|      RELU       |                                          |
|   Max pooling   |       2x2 stride,  outputs 5x5x16        |
|     Flatten     |               outputs 400                |
| Fully Connected |        Input = 400. Output = 200.        |
|      Relu       |                                          |
| Fully Connected |        Input = 200. Output = 100.        |
|      Relu       |                                          |
| Fully Connected |        Input = 100. Output = 70.         |
|      Relu       |                                          |
| Fully Connected |         Input = 70. Output = 43          |



####3. Model Parameters:

- EPCOHS **80** 

- Batch Size **128**

- Learning Rate **.001**

  ​

####4. Approach

My final model results were:
* Training set accuracy of **1.00**
* Validation set accuracy of **0.935**
* Test set accuracy of **0.908**

The first model that I started with was LeNet. The main reason to use it was that its only Model that was known to me. The reason to modify was the accuracy wasn't met and there was a scope of improving it. The first addition to the model was adding preprocessing which resulted in slight increase in accuracy, though it did not result in good enough accuracy.  

Adding a new fully connected layer helped tune weights better and improved the accuracy.

If an iterative approach was chosen:

* Being new to CNN, I started with LeNet architecture with default parameters. I could hardly get accuracy of 0.86. 

* With preprocessing steps, I could get an accuracy of ~ 0.91

* By increasing the EPOCHS and adding histrogram equalization I could get accuracy for validation data ~0.94

  ​

###Test a Model on New Images

####1. Downloaded German Traffic Signs

Here are eight German traffic signs that I found on the web:

![alt text][image4] 

The only difficulty to read the images in the correct format.

####2. Model Performace

Here are the results of the prediction:

|      Image      |   Prediction    |
| :-------------: | :-------------: |
| Animal Crossing | Animal Crossing |
|    No Entry     |    No Entry     |
|    Priority     |    Priority     |
|   Right Turn    |   Right Turn    |
|    Road Work    |    Road Work    |
| Speed Limit 30  | Speed Limit 30  |
| Speed Limit 70  | Speed Limit 70  |
|    Stop Sign    |    Stop Sign    |

The model was able to correctly guess 6 of the 8 traffic signs, which gives an accuracy of 87.5%.

The model accuracy for these images are 87.5% and all the signs are predicted correctly.This seems to be a case of good fit.

####3. Model Probability

For the first image, the model is relatively sure that this is a Animal Crossing (probability of 0.55). The top five soft max probabilities were

```
Original Labels:   [31 17 11 33 25  1  4 14]
Predicted Labels:  [31 17 11 33 18  1  4 14]
**********************************************************
Image animalcrossing.png 
 Probabilities: [  9.99987483e-01   1.24074231e-05   1.38629218e-07   1.24707397e-10
   4.14036132e-11] 
 Predicted classes: ['Wild animals crossing' 'Road narrows on the right' 'Bicycles crossing'
 'Traffic signals' 'Double curve']
Image NoEntry.png 
 Probabilities: [  1.00000000e+00   3.38176415e-18   2.14889746e-20   2.99200477e-22
   4.38144517e-23] 
 Predicted classes: ['No entry' 'Yield' 'Priority road' 'Traffic signals' 'Turn left ahead']
Image Priority.png 
 Probabilities: [  1.00000000e+00   3.28755187e-12   4.02074931e-22   1.11580415e-26
   1.74778732e-28] 
 Predicted classes: ['Right-of-way at the next intersection' 'Traffic signals'
 'Beware of ice/snow' 'Turn left ahead' 'Double curve']
Image rightturn.png 
 Probabilities: [  1.00000000e+00   3.18094075e-15   9.86552826e-16   5.43141243e-16
   4.92860927e-18] 
 Predicted classes: ['Turn right ahead' 'Go straight or left' 'Keep left'
 'Speed limit (30km/h)' 'Ahead only']
Image roadwork.png 
 Probabilities: [  9.99918938e-01   8.08613695e-05   1.88248634e-07   1.85206417e-09
   5.63126212e-11] 
 Predicted classes: ['General caution' 'Road work' 'Go straight or left' 'Turn right ahead'
 'Speed limit (30km/h)']
Image speedLimit30.png 
 Probabilities: [  1.00000000e+00   3.82060739e-09   7.92127058e-11   1.49314437e-12
   8.61772459e-13] 
 Predicted classes: ['Speed limit (30km/h)' 'Speed limit (70km/h)' 'Speed limit (50km/h)'
 'Speed limit (20km/h)' 'Roundabout mandatory']
Image speedLimit70.png 
 Probabilities: [  9.99943972e-01   5.59704677e-05   1.08710889e-08   5.06101932e-15
   1.41458036e-16] 
 Predicted classes: ['Speed limit (70km/h)' 'Speed limit (20km/h)' 'Speed limit (30km/h)'
 'Speed limit (80km/h)' 'Turn right ahead']
Image stop.png 
 Probabilities: [  9.99850273e-01   1.00861886e-04   4.29821921e-05   4.73250930e-06
   1.08571726e-06] 
 Predicted classes: ['Stop' 'No vehicles' 'Keep right' 'Speed limit (120km/h)'
 'Turn left ahead']
```

####Gaps and Improvements

- The Network needs to evolve 
- Use better backpropogation and loss calculation 
- Use dropout 
- With reduced EPOCHs, try to achieve the accuracy