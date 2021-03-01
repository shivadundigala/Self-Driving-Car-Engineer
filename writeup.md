**Advanced Lane Finding Project**

The goals / steps of this project are the following:

1. Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
2. Apply a distortion correction to raw images.
3. Use color transforms, gradients, etc., to create a thresholded binary image.
4. Apply a perspective transform to rectify binary image ("birds-eye view").
5. Detect lane pixels and fit to find the lane boundary.
6. Determine the curvature of the lane and vehicle position with respect to center.
7. Warp the detected lane boundaries back onto the original image.
8. Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

[//]: # (Image References)

[image11]: ./examples/undistort_output.png "Undistorted"
[image12]: ./test_images/test1.jpg "Road Transformed"
[image13]: ./examples/binary_combo_example.jpg "Binary Example"
[image14]: ./examples/warped_straight_lines.jpg "Warp Example"
[image15]: ./examples/color_fit_lines.jpg "Fit Visual"
[image16]: ./examples/example_output.jpg "Output"



[image1]: ./output_images/Output_binary_image.jpg
[image2]: ./output_images/Undistorted_Warped_image.jpg
[image3]: ./output_images/Sliding_Window_image.jpg
[image4]: ./output_images/Fit__poly_image.jpg
[image5]: ./output_images/Lane_image.jpg
[image6]: ./test_images/test2.jpg

[image7]: ./camera_cal_output/calibration9.jpg
[video1]: ./project_video.mp4 "Video"


---

### Camera Calibration

#### 1. Briefly state how you computed the camera matrix and distortion coefficients. Provide an example of a distortion corrected calibration image.

The code for this step is contained in the second and third code cell of the notebook in "./P2.ipynb" 

"object points"(x, y, z) coordinates of the chessboard corners in the world. Assuming the chessboard is fixed on the (x, y) plane at z=0, such that the object points are the same for each calibration image.  Thus, `objp` is just a replicated array of coordinates, and `objpoints` will be appended with a copy of it every time I got successfully detect all chessboard corners in a test image.  Later `imgpoints` will be appended with (x, y) pixel position of each of the corners in image plane with each successful detection.  

Finally, used the output `objpoints` and `imgpoints` to compute camera calibration and distortion coefficients using `cv2.calibrateCamera()` function.  Applied distortion correction to test image using the `cv2.undistort()` function and obtained result: 

![alt text][image1]


#### 1. Provide an example of a distortion-corrected image.

To demonstrate this step, I will describe how I apply the distortion correction to one of the test images like this one:
![alt text][image2]

#### 2. Describe how (and identify where in your code) you used color transforms, gradients or other methods to create a thresholded binary image.  Provide an example of a binary image result.

I used a combination of color and gradient thresholds to generate a binary image (thresholding steps at lines #3 in `P2.ipynb`).  Here's an example of my output for this step. 

![alt text][image3]

#### 3. Describe how (and identify where in your code) you performed a perspective transform and provide an example of a transformed image.

Combination of color and gradient threshold to generate binary_image. code for Perspective_transform includes a function 'corners_unwarped' in 'line #6'. This function basically it takes an image, with source and distination points givebn manually
as below:

src = np.float32([[600, 450], [720, 450], [1180, 720], [280, 720]])
dst = np.float32([[200, 0], [1000, 0], [1180, 720], [200, 720]])

Verified that perspective transform was working by drawing the `src` and `dst` points onto a test image and its warped counterpart to verify lines appear parallel in warped image.

![alt text][image4]

#### 4. Describe how (and identify where in your code) you identified lane-line pixels and fit their positions with a polynomial?

Drawn a histogram of bottom half of the image, Created an output image to draw on and plotting the result. It founds peak of the left and right halves of the histogram. They will be the starting point for left and right lines. After analysing visually, I pick the no. of sliding windows, deciding the width of the windows and minimum no. of pixels found to recenter window. Finally, 'fit_polynomial' function extracted left and right line pixel position 

![alt text][image4]

![alt text][image5]

#### 5. Describe how (and identify where in your code) you calculated the radius of curvature of the lane and the position of the vehicle with respect to center.

Took mean of left and right radii. Assuming image centre as centre of the car and later converted pixel value into metres(m). Calculated difference between lane centre and centre of car. For a negative value, taken as left from centre and for positive as right of centre. 

![alt text][image7]

#### 6. Provide an example image of your result plotted back down onto the road such that the lane area is identified clearly.

I implemented this step in lines # through # in my code in `P2.py` in the 'line #21'.  

![alt text][image7]

---

### Pipeline (video)

#### 1. Provide a link to your final video output.  Your pipeline should perform reasonably well on the entire project video (wobbly lines are ok but no catastrophic failures that would cause the car to drive off the road!).

[link to my video result](.output_videos/project_video.mp4)

---

### Discussion

#### 1. Briefly discuss any problems / issues you faced in your implementation of this project.  Where will your pipeline likely fail?  What could you do to make it more robust?

My Pipeline doesn't work on too urvy roads, especially in dark shadows on the road. According to me, this might depends on the color spaces, sobel and threshold combinations.   
