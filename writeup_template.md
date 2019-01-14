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

My pipeline consisted of 5 steps. First, I applied a gaussian blur to the image with a value of 5. Gaussian blur assists in reducing noise in the image. Next I grayscaled the image as color does not assist in line detection and may add to poor edge designation. A canny threshold was then applied to the image in order to catch all edges in the image. The image was then masked in order to focus in on the region of interest: the lines on the highway. Finally, a hough line transform was applied to the image which detects all straight edges within the region of interest.  

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by separating the left and right lines based on the slope of the line. Next I used numpy.polyfit in order to get the slope and y-intersect of the lines found. From there I was able to extrapolate the appropriate x values for both the top and bottom, left and right, extents of the lines based on hardcoded values of y found by the known size of the image.

This website's explanation of the draw_lines() function was very helpful in developing my understanding: https://peteris.rocks/blog/extrapolate-lines-with-numpy-polyfit/

### 2. Identify potential shortcomings with your current pipeline

One shortcoming of this pipeline is that it deals with straight lines. As soon as a curve is introduced, the lines will not fit quite right. Extreme curves would introduce danger as the hardcoded y points would be well outside of the actual lane.

Another immediate shortcoming is that there are frames where noise is introduced and the lines jump away from the lane line momentarily.

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to filter out the lines which are obviously not on the traffic lanes. I tried many different approaches to accomplish this but have so far been unable to prevent this bug.

Another potential improvement could be to leverage numpy.polyfit to draw more complex lines and begin to handle curves in the road.
