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

### 1. Description of the pipeline. 

My pipeline consisted of 6 steps. First, I applied color masking scheme to mask white and yello pixels to detect while and yellow lane lines. Then I convereted the colored mask image to grayscale and then applied gaussian filter for smoothening the image with kernel size of 3. After that I applied canny edge detector to get edge lines. Before starting the pipeline, I initialized values to specify a trapezoidal region of interest i.e width of top and bottom and as well as the height. Then by image shape vertices of the trapezoid are calculated and passed as parameter to region_of_interest function to get only the interesting region in the complete image. At the end hough lines are identified in the region of interest and the lines are drawn over the top of the image.


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first identifying points (i.e x, y) that belonged to the left lane and right lane depending on the slope. Any possible lane would have absolute slope more than 0.5. In the case of left lane, slope was found to be negative whereas positive for right lane. After seperating points that would have contibuted to left lane and right lane, I fit a line through these points to get slope and intercept values for left and right lane. Since, we already know region of interest in the entire image i.e top and bottom y values for the trapeziod(ROI), I initialized two y values - one for the top and other for bottom upto which we need to extrapolate the lines and using the slope and intercept values, calculated x values for all the four vertices i.e 2 vertices belong to left lane and the other two to the right lane.
At the end, I receive (x,y) value for starting and end of left lane and right lane.

Another addition to the algorithm used to draw lines is that there were times when all the slope values calculated beloned to either left or right lane. In such cases, previous slope and intercept values were used to represent the lane for which no slope value was detected.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![Color Masked Image][image1]
![Gray Scale Image][image2]
![Blurred image][image3]
![Edge detected Image][image4]
![Region of interest][image5]
![Hough Lines][image6]
![Final result][image7]


### 2. Potential shortcomings with current pipeline


One potential shortcoming would be what would happen when the lanes we see in the video are not staright lines but instead curves of higher order. This alogorithm of fiting a line would fail there.

Another shortcoming is the lanes as seen in the video are very jittery. They are not very smooth.


### 3. Possible improvements to your pipeline

A possible improvement would be to use previously identified lane lines to limit the search process for lane lines in the next frames. This would reduce the exhaustive search through the entire image as is happening now.

Another potential improvement could be to fit higher order curves for lane lines instead of straight lines or any algorithm that would incorporate different degree of lane lines.


The Project - installation guideline
---
**Step 1:** Getting setup with Python

To do this project, you will need Python 3 along with the numpy, matplotlib, and OpenCV libraries, as well as Jupyter Notebook installed. 

We recommend downloading and installing the Anaconda Python 3 distribution from Continuum Analytics because it comes prepackaged with many of the Python dependencies you will need for this and future projects, makes it easy to install OpenCV, and includes Jupyter Notebook.  Beyond that, it is one of the most common Python distributions used in data analytics and machine learning, so a great choice if you're getting started in the field.

Choose the appropriate Python 3 Anaconda install package for your operating system <A HREF="https://www.continuum.io/downloads" target="_blank">here</A>.   Download and install the package.

If you already have Anaconda for Python 2 installed, you can create a separate environment for Python 3 and all the appropriate dependencies with the following command:

`>  conda create --name=yourNewEnvironment python=3 anaconda`

`>  source activate yourNewEnvironment`

**Step 2:** Install OpenCV

**Step 3:** Install moviepy  

**Step 4:** Open the code in a Jupyter Notebook

You will complete this project in a Jupyter notebook.  If you are unfamiliar with Jupyter Notebooks, check out <A HREF="https://www.packtpub.com/books/content/basics-jupyter-notebook-and-python" target="_blank">Cyrille Rossant's Basics of Jupyter Notebook and Python</A> to get started.

Jupyter is an ipython notebook where you can run blocks of code and see results interactively.  All the code for this project is contained in a Jupyter notebook. To start Jupyter in your browser, run the following command at the terminal prompt (be sure you're in your Python 3 environment!):

`> jupyter notebook`

A browser window will appear showing the contents of the current directory.  Click on the file called "P1.ipynb".  Another browser window will appear displaying the notebook.  Follow the instructions in the notebook to complete the project.  