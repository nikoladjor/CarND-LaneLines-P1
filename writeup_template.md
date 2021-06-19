# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

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

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...


Result on the test images:
![alt text][test_images]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
