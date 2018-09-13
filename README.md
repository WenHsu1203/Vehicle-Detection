# Introduction
In this project I implement a software to identify vehicles in a video from a front-facing camera on a car.
# The goals / steps of this project are the following:
* Perform a Histogram of Oriented Gradients (HOG) feature extraction on a labeled training set of images and train a classifier Linear SVM classifier
* Apply a color transform and append binned color features, as well as histograms of color, to my HOG feature vector. 
* Implement a sliding-window technique and use my trained classifier to search for vehicles in images.
* Run your pipeline on a video stream and create a heat map of recurring detections frame by frame to reject outliers and follow detected vehicles.

### Extract Histogram of Oriented Gradients (HOG) Features From the Training Images

The code for this step is contained in lines 6 through 25 of the file called 'utility.py'. I started by reading in all the `vehicle` and `non-vehicle` images.  Here is an example of one of each of the `vehicle` and `non-vehicle` classes:

![Vehicle verse Non-Vehicle](https://github.com/WenHsu1203/Vehicle-Detection/blob/master/examples/car_not_car.png?raw=true)

I then explored different color spaces and different `skimage.hog()` parameters (`orientations`, `pixels_per_cell`, and `cells_per_block`).  I grabbed random images from each of the two classes and displayed them to get a feel for what the `skimage.hog()` output looks like.

Here is an example using the `YCrCb` color space and HOG parameters of `orientations=8`, `pixels_per_cell=(8, 8)` and `cells_per_block=(2, 2)`:

![HOG](https://github.com/WenHsu1203/Vehicle-Detection/blob/master/examples/HOG_example.jpg?raw=true)

### Train a Classifier Using Selected HOG, Spatial and Histogram Features

I trained a linear SVM using hog, spatial and histogram features. First, extract all the features using function `extract_features` in lines 48 through 96 of `utility.py`, and split the data into training and testing data with test size = 0.2. After that, normalized all the data using StandardScale method from StandardScaler package, and train the classifier. The test accuracy is 0.96. All the color features and parameters are in the code block number 2 in `Vehicle Detection and Tracking.ipynb`

### Sliding Window Search

I used the sliding window formula from the lecture to implement the function, and as for how I chose the scale, I set the scale larger if the value of y is larger since the car seems bigger. As for the overlapping rate, I used try and error method and I found the ratio 0.8 works well. 
![Sliding Window](https://github.com/WenHsu1203/Vehicle-Detection/blob/master/examples/sliding_window.jpg?raw=true)

### False Alarm Filter and Overlapping Bounding Boxes:

I recorded the positions of positive detections in each frame of the video.  From the positive detections I created a heatmap and then thresholded that map to identify vehicle positions.  I then used `scipy.ndimage.measurements.label()` to identify individual blobs in the heatmap.  I then assumed each blob corresponded to a vehicle.  I constructed bounding boxes to cover the area of each blob detected.  

Here's an example result showing the heatmap from a series of frames of video, the result of `scipy.ndimage.measurements.label()` and the bounding boxes then overlaid on the test_image 6:

![Label Map](https://github.com/WenHsu1203/Vehicle-Detection/blob/master/examples/labels_map.png?raw=true)

### Here are six frames and their corresponding heatmaps:

![HeatMap](https://github.com/WenHsu1203/Vehicle-Detection/blob/master/examples/bboxes_and_heat.png?raw=true)

# Result
Check out the video ☟

[![Video](http://img.youtube.com/vi/PQqofy0d-hM/0.jpg)](http://www.youtube.com/watch?v=PQqofy0d-hM "Vehicle Detection")


