# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)

<img src="examples/laneLines_thirdPass.jpg" width="480" alt="Combined Image" />

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road


[//]: # (Image References)

[image1]: ./examples/masked_img.jpg "masked_img"
[image2]: ./examples/gray.jpg "gray"
[image3]: ./examples/blur.jpg "blur"
[image4]: ./examples/edge.jpg "edge"
[image5]: ./examples/roi.jpg "roi"
[image6]: ./examples/lines.jpg "lines"
[image7]: ./examples/result.jpg "result"


---

Overview
---
### Reflection

### 1. Description your pipeline. 

My pipeline consisted of 5 steps. First, I applied color masking scheme to mask white and yello pixels to detect while and yellow lane lines. Then I convereted the colored mask image to grayscale and then applied gaussian filter for smoothening the image with kernel size of 3. After that I applied canny edge detector to get edge lines. Before starting the pipeline, I initialized values to specify a trapezoidal region of interest i.e width of top and bottom and as well as the height. Then by image shape vertices of the trapezoid are calculated and passed as parameter to region_of_interest function to get only the interesting region in the complete image. At the end hough lines are identified in the region of interest and the lines are drawn over the top of the image.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first identifying points (i.e x, y) that belonged to the left lane and right lane depending on the slope. Any possible lane would have absolute slope more than 0.5. In the case of left lane, slope was found to be negative whereas positive for right lane. After seperating points that would have contibuted to left lane and right lane, I fit a line through these points to get slope and intercept values for left and right lane. Since, we already know region of interest in the entire image i.e top and bottom y values for the trapeziod(ROI), I initialized two y values - one for the top and other for bottom upto which we need to extrapolate the lines and using the slope and intercept values, calculated x values for all the four vertices i.e 2 vertices belong to left lane and the other two to the right lane.
At the end, I receive (x,y) value for starting and end of left lane and right lane.

Another addition to the algorithm used to draw lines is that there were times when all the slope values calculated beloned to either left or right lane. In such cases, previous slope and intercept values were used to represent the lane for which no slope value was detected.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]
![alt text][image7]


### 2. Potential shortcomings with current pipeline


One potential shortcoming would be what would happen when the lanes we see in the video are not staright lines but instead curves of higher order. This alogorithm of fiting a line would fail there.

Another shortcoming is the lanes as seen in the video are very jittery. They are not very smooth.


### 3. Possible improvements to your pipeline

A possible improvement would be to use previously identified lane lines to limit the search process for lane lines in the next frames. This would reduce the exhaustive search through the entire image as is happening now.

Another potential improvement could be to fit higher order curves for lane lines instead of straight lines or any algorithm that would incorporate different degree of lane lines.

Creating a Great Writeup
---
For this project, a great writeup should provide a detailed response to the "Reflection" section of the [project rubric](https://review.udacity.com/#!/rubrics/322/view). There are three parts to the reflection:

1. Describe the pipeline

2. Identify any shortcomings

3. Suggest possible improvements

We encourage using images in your writeup to demonstrate how your pipeline works.  

All that said, please be concise!  We're not looking for you to write a book here: just a brief description.

You're not required to use markdown for your writeup.  If you use another method please just submit a pdf of your writeup. Here is a link to a [writeup template file](https://github.com/udacity/CarND-LaneLines-P1/blob/master/writeup_template.md). 


The Project
---

## If you have already installed the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) you should be good to go!   If not, you should install the starter kit to get started on this project. ##

**Step 1:** Set up the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) if you haven't already.

**Step 2:** Open the code in a Jupyter Notebook

You will complete the project code in a Jupyter notebook.  If you are unfamiliar with Jupyter Notebooks, check out [Udacity's free course on Anaconda and Jupyter Notebooks](https://classroom.udacity.com/courses/ud1111) to get started.

Jupyter is an Ipython notebook where you can run blocks of code and see results interactively.  All the code for this project is contained in a Jupyter notebook. To start Jupyter in your browser, use terminal to navigate to your project directory and then run the following command at the terminal prompt (be sure you've activated your Python 3 carnd-term1 environment as described in the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) installation instructions!):

`> jupyter notebook`

A browser window will appear showing the contents of the current directory.  Click on the file called "P1.ipynb".  Another browser window will appear displaying the notebook.  Follow the instructions in the notebook to complete the project.  

**Step 3:** Complete the project and submit both the Ipython notebook and the project writeup

## How to write a README
A well written README file can enhance your project and portfolio.  Develop your abilities to create professional README files by completing [this free course](https://www.udacity.com/course/writing-readmes--ud777).

