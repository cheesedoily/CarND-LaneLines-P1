**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve.jpg' "solidWhiteCurve"
[image2]: ./test_images_output/solidWhiteRight.jpg' "solidWhiteRight"
[image3]: ./test_images_output/solidYellowCurve.jpg' "solidYellowCurve"
[image4]: ./test_images_output/solidYellowCurve2.jpg' "solidYellowCurve2"
[image5]: ./test_images_output/solidYellowLeft.jpg' "solidYellowLeft"
[image6]: ./test_images_output/whiteCarLaneSwitch.jpg' "whiteCarLaneSwitch"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I converted the images to grayscale. After blurring the image, I use 
the canny detection to create a new image of just edges. From this canny image I create a new image of lines that has been
masked by a region of interest (which in my case is a trapezoid). After limiting the lined image to this region of interest,
I draw hough lines and finally weight them appropriately, before creating one superimposed image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by first splitting the lines according to their slope with the rationale that we should expect one positively sloped line and one negatively, respresenting each side of the lane lines.

Below you can see how the various line segments are merged and extrapolated to create the final two lane lines.

![alt text][image1]
![alt text][image2]
![alt text][image3]
![alt text][image4]
![alt text][image5]
![alt text][image6]

### 2. Identify potential shortcomings with your current pipeline

The largest potential shortcoming of the improved pipeline is that it doesn't do a particularly good job of filtering out
spurious lines. 

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to first split the region of interest into two (left and right), then would ensure any sloped lines that would get batched with the wrong lane line would be ignored appropriately. 

Another potential improvement could be to look for lines of a relatively similar slope only, ignoring ones that are one or two standard deviations away from the norm. That challenge with this approach is that if there are many similarly sloped lines that are not helpful (such as many flat lines), they will influence the mean and variance and not be ejected.

Another potential improvement would be to think of the video as a whole rather than each frame without any state. I'm sure there are a bunch of strategies here worth exploring.
