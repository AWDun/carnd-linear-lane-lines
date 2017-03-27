#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

###1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. 
	1. Convert images to grayscale
	2. Use Gaussian smoothing to remove irregular gradients in the image
	3. Defined the parameter for canny filter, which finds the pixels with highest gradient within the threasholds, creating a image of edges
	4. I created a polygon to mask the image so the Hough transform only looks for the lane markers in the polygon
	5. Run Hough transform to look for lines in the masked edges image
	6. Filter the line segments by slope to find segments for the left and right lane markers respectively
	7. Fit a line to the vertices of the line segments to find a slope and a intercept for the left and right lane markers
	8. Find the end points from the fitted line y=mx+b, where y1 is the bottom of the image or max(y), y2 is 0.6*max(y)
	9. Plot the line to the image starting from the bottom of the image using cv2.line
	10. Overlay the lines onto the colored image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...
	1.Filter the line segments by slope to find segments for the left and right lane markers respectively
	2. Fit a line to the vertices of the line segments to find a slope and a intercept for the left and right lane markers
	3. Find the end points from the fitted line y=mx+b, where y1 is the bottom of the image or max(y), y2 is 0.6*max(y)
	4. Plot the line to the image starting from the bottom of the image using cv2.line

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the road curves, because it still fits a linear line. 

Another shortcoming could be that many reflectors and bott's dots create edges that mess up the lane marker detection, and ignores lane markers far in the distance. 

A third shortcoming is that the end points of the lines do not change with the horizon. 


###3. Suggest possible improvements to your pipeline

For the first shortcoming, I can add degrees when doing polyfit, but since cv2 did not include a way to plot a polynomial, I did not find a easy way to plot it

For the second shortcoming, an improvement could be to have different min line length and other parameters for different parts of the image

For the third shortcoming, ene way to improve it is to find the horizon using hough transform and change the end points using that value

I can also use some filtering to smooth out the lane lines between frames in the video
