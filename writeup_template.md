# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

[//]: # (Image References)
[image1]: ./test_images_output/sample_images.png "Original_vs_Process"
	
---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps as described in function pipeline_process_image in P1.ipynb file
1. Convert original color image to grayscale
2. Apply gaussian blur to smooth the image in order to get rid of noise
3. Apply Canny Edge detection to the image 
4. Define the area of the interest and ignore the rest by defining 4 vertices in the image lower_left, upper_left, upper_right and lower_right positions as some ratio with the original image. This way the area of interest can adapt to any size of images.
5. From area we defined, we use this to find the Haugh lines.
6. Draw these Haugh lines on the original image by draw_lines function

I have modified the draw_lines function such that it can draw a straight line on the full extent of the lane (without this modification we will see a cut line)

The idea is to calculate slope value of line `y2-y1/x2-x1` and with a slope greater than 0, it's left lane while the others are right lane line. I put those coordinate of x,y in `left_x, left_y, right_x and right_y` accordingly to later on calculate slope and intercept value of equation `y = mx + b` with helper function `np.polyfit(X, Y, 1)`

Now to draw the line is simple as calculating coordinate of x, y from the above equation.

Here is one of picture example of original image compare to image with lane lines drawn.

![Original vs Process][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the initial implementation is the area of interest is too broad so it detects more Haugh lines than just lanes line so to fix this issue I have played around with the ratio of area.

Another issue is when applying this pipeline to optional video, it turns out the lane lines drawn are not accurate enough, we have some noise of similar straight line like lane line highlight which should not.

Another shortcoming could be that if the road doesn't have a street lane line or has been covered with dirt, snow or even gravel road, my pipeline won't be able to find a lane line to detect.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to start tracking other objects like road posts, adjacent cars, the edge of the road etc. The more meaningful road related the better computer can understand the context around it.

Another potential improvement could be to use deep learning technique to identify objects, analyze surrounding sound or other sensors from around the car.