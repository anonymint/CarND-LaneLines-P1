# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps as described in function pipeline_process_image in P1.ipynb file
1. Convert original color image to gray scale
2. Apply guassian blurto smooth the image in order to get rid of noise
3. Apply Canny Edge detection to the image 
4. Define the area of the interest and ignore the rest by defining 4 verticies in the image lower_left, upper_left, upper_right and lower_right positions as some ratio with original image. This way the area of interest can adapt to any size of images.
5. From area we defined, we use this to find the Haugh lines.
6. Draw these Haugh lines on the original image by draw_lines function

I have modified the draw_lines function such that it can draw a straight line on the full extent of the lane (without this modification we will see a cut line)

The idea is to calculate slope value of line `y2-y1/x2-x1` and with slope greater than 0, it's left lane while the others are right lane line. I put those coordinate of x,y in `left_x, left_y, right_x and right_y` accordingly to later on calculate slope and intercept value of equation `y = mx + b` with helper function `np.polyfit(X, Y, 1)`

Now to draw the line is simple as calculate coordinate of x, y from the above equation.

Here is one of picture example of original image compare to image with lane lines drawn.

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the initial implementation is the area of interest is too broad so it detect more Haugh lines than just lanes line so to fix this issue I have play around with ratio of area.

Another issue is when apply this pipeline to optional video, it turns out the lane lines drawn are not accurate enough, we have some noise of similar straight line like lane line hightlight which should not.

Another shortcoming could be that if the road doesn't have a lane line or has been covered with dirt, snow or even grave road, my pipeline won't be able to find a lane line to detect.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to start tracking another objects like road post, adjeacent cars, edge of the road etc. The more meaningful road related the better computer can understand the context around it.

Another potential improvement could be to use deep learning technique to identify objects, analyse surrounding sound or other sensor from around the car.
