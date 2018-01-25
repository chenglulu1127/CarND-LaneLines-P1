# **Finding Lane Lines on the Road** 

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection

### 1. Describe the pipeline. 

My pipeline consisted of 5 steps. 
1. Use Gaussian kernel for smoothing to reduce noise | 2. Apply canny edge detection using gradients 
:-------------------------:|:-------------------------:
![image1](./test_images_output/for_writeup/solidWhiteCurve_blurred.jpg) | ![image2](./test_images_output/for_writeup/solidWhiteCurve_canny_edges.jpg)

3. Define a four sided polygon to mask<br> 4. Run Hough on edge detected image to find lines | 5. Connect detected lines by applyingn the following steps
:-------------------------:|:-------------------------:
![image3](./test_images_output/for_writeup/solidWhiteCurve_line_img.jpg) |  s1. remove near horizental lines; s2. use position and slope signs to seperate left and right lanes; s3. only consider lines with slope difference <=0.1 from the longest line; s4. calculate weighted average (weighted by line length) slope and intercept of the longest 5 lines; s5. get the coordinates of the final connected line.

6. Draw lines onto image using weighted sum of original image and a blank image with detected lines on it
:-------------------------:
![image4](./test_images_output/for_writeup/solidWhiteCurve_final.jpg)


### 2. Result
Please refer to "test_videos_out/solidWhiteRight.mp4", "test_videos_out/solidYellowLeft.mp4", "test_videos_out/challenge.mp4".

### 3. Identify potential shortcomings with your current pipeline
* There's still some problem for the challenge video. For example:
* It doesn't work well with curve lanes 
* When the lane is not easily detected in some bad weather, the algorithm will not work well
* When it is sparse dotted lanes or the long line is too far away and the car is turning right or left, the prediction will be off
* When the lighting condition changes, it might not work very well

### 4. Suggest possible improvements to your pipeline
* Can develop a function that can memorize the lane in the last clip so that if the if it is not easy to detect lane in current clip, we can use the previous one as a reference or baseline. Also if the slope changes too much, it can also help make modification
* Instead of linear functions, use polynomial?
* Automatically adapt to different lighting conditions 