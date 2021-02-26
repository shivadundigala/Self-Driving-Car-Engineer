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

My pipeline consisted of following steps. 

a) I converted the images to grayscale for 1-channel image. 
b) Used helper functions canny(threshold are decided by trial & error and also kind getting an idea to guess using the lectures to 50 and 150 for low & high), gaussian_blur to define the threshold and kernel size for edges.
c) Defined the region of interest for detecting the lanes and masking. 
d) Later hough_lines transform for drawing hough lines.
e) Added weights to the transformed lines. 
f) Basically i have calculated slopes for the segrating lines, later classified -ve & +ve slope to decide left & right lanes respectively. Finally, Averaged and extrapolated them.  
g) Implemented the pipeline on test images and later on video and saved them in output directory. 



### 2. Identify potential shortcomings with your current pipeline


One potential concern is it can only work on subset if images assuming the camera is located in front center position.
If the position is changed, it may fail to detect the lines.  

Lastly, it will fail to identity the curvature or S-curve roads efficiently. 

### 3. Suggest possible improvements to your pipeline

A possible improvement would be definitely the detecting the lane lines during brightness of the road during night time.

Another potential improvement is if the lane lines markings are faded or barely seen. 
