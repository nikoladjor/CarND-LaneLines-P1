# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[test_images]: ./test_images_writeup.png "Test images"
[test_mask]: ./test_images_masked.png "Test region of interest"
---

## Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 
* First, I converted the images to grayscale using `cv2.cvtColor` function.
* Next, to reduce the noise, Gaussian blur was done.
* Next, I performed edge detection using Canny algorithm.
* The edge-detected image was then masked to isolate region of interest. This was done with the following piece of code:\
    ``` python
    # Store image dims
    X = image.shape[1]
    Y = image.shape[0]

    vertices = np.array(
        [[
            (X//7,Y),
            (8.5*X//9,Y),
            (2.35*X//4,3.8*Y//6),
            (1.7*X//4,3.8*Y//6)
        ]], 
        dtype= np.int32
    )
    ```
    In order to test the region of interest, I plotted all test images with the mask applied:\
    ![alt text][test_mask]
* Finally, on masked edge-detected images, line segments were isolated using `cv2.HoughLinesP` function. 

In order to draw a single line on the left and right lanes, I modified the original `draw_lines()` function by dividing the line segments based on the sign of its slope, which was calculated as `slope=(y2-y1)/(x2-x1)`. In addition the line segments with shallow angles (`angle = np.degrees(np.arctan(slope))`) were also filtered out. Although this was not needed for test images and the Video#1, I used it so that some of the bumps on the road in Video#2 (for example, segment between 10-12s in the Video#2) would not be detected as line segments. With such line segments filtered between right and left lane segments, I used `cv2.fitLine` function which uses points given by filtering to fit a single line for both of the lanes. Start and end points were deterimened based on detected line segment points and image dimensions.


Result on the test images:
![alt text][test_images]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when sharp curved lines need to be detected. In my current implementation, I am fitting a straight line for both right and left lanes. This is evident when I try to apply the pipeline on the challenge video, for example.

Another shortcoming could be that region of interest is done by trial and error, which can be automated based on some camera calibration/previous knowledge.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to have segmentation of the images (and frames later on), to change region of interest on-the-fly, so that it can be more robust.

Another potential improvement could be to use `np.polyfit` to try and fit more complex lines, in case where curves need to be detected.

### 4. IMPORTANT INFO
I was not able to install the starter kit from the git repo, so I followed the packages listed and created my onw Anaconda environment. (with python=3.9 and up-to-date packages)