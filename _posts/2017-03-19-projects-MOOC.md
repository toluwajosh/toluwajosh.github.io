---
layout: post
title: "Finding Lane Lines with Colour Thresholds"
description: Udacity Nanodegree Project 4
headline: 
modified: 2017-03-19
category: Projects
tags: [Projects, MOOC]
imagefeature: 
mathjax: 
chart: 
comments: true
featured: true
---


<!-- **Advanced Lane Finding Project** -->

[//]: # (Image References)

[image1]: ./images/lane_lines/dachcam_view.jpg "View from camera mounted in car."
[image2]: ./images/lane_lines/whitehsl.png "Values for White in RGB and HSL"
[image3]: ./images/lane_lines/yellowhsl.png "Values for Yellow in RGB and HSL"
[image4]: ./images/lane_lines/hls_colourspace.png "Test Image Shown in HLS Colour Space"

[image5]: ./images/lane_lines/rgb_white_threshold.png " "
[image6]: ./images/lane_lines/rgb_yellow_threshold.png " "
[image7]: ./images/lane_lines/hls_yellow_threshold.png " "
[image8]: ./images/lane_lines/warp_verify.png "Perspective Transform Output"
[image9]: ./images/lane_lines/lower_half_n_histogram.png "Lower Half Image and Histogram"
[image10]: ./images/lane_lines/plotlines_on_bin_img.jpg "Lines fitted on lane pixels"
[image11]: ./images/lane_lines/curvature_formula.png "Formula for Radius of Curvature"
[image12]: ./images/lane_lines/final_result.png "Lanes Projected on Original Image"

This post is part of a full project called Advanced Lane Finding. The 4th project of the first term of [Udacity Self-Driving Car Nanodegree](https://www.udacity.com/drive). For self-driving cars, being able to follow a lane is very important. So knowing where the lane lines are is very key.

In this post I will share how I am able to find lane lines from an image that represents a view from one of the cameras mounted on a car. This is perhaps the most important part of the project. A full repository of the project, including this solution can be found [here](https://github.com/toluwajosh/CarND-Advanced-Lane-Lines/blob/master/solution_writeup.md):

Here is a typical image from the camera;

<img src="{{ site.url }}/images/lane_lines/dashcam_view.jpg" alt="View from camera mounted in car.">

Our objective is to be able to effectively find the lane lines in front of the car. A quick observation shows that most lane lines are either yellow or white. So we will use this information to find places in the image that are lane lines.

Images are usually represented in colour spaces, the most popular being RGB. What this means is that every pixel has a Red, Green and Blue value. So, for each pixel in the image we would have a set of numbers e.g. (255,255,255) which signifies the level of each colour component in the pixel. For RBG colour space, white is represented as (255,255,255), while black is (0,0,0).

We also have other colour spaces such as HSV, HSL, YUV. I used RGB and HSL in this project, so I will be using them to explain.

We know that white is represented by (255,255,255) in both RGB and HSL colour space, but we have to ascertain the values for the yellow lane colour. To do this, I pulled out colour picker from the Inkscape software, just to have a visual representation.

<img src="{{ site.url }}/images/lane_lines/whitehsl.png" alt="Values for White in RGB and HSL.">

Playing around with the values we can find the values that corresponds to the yellow we are looking for. You can ignore the A (Alpha) value, its not necessary here.

<img src="{{ site.url }}/images/lane_lines/yellowhsl.png" alt="Values for yellow in RGB and HSL.">

The idea, however is to use a range that covers the yellow colour spectrum and also cover the white colour spectrum. So I chose the following values after experimenting with the ranges.


| Colour 		| Threshold Values   										| 
|:-------------:|:--------------------------------------------------------:	| 
| RGB White     | Lower = {100, 100, 200}, Upper = {255, 255, 255}       	| 
| RGB Yellow 	| Lower = {225, 180, 0}, Upper = {255, 255, 170} 			|
| HLS Yellow 	| Lower = {20, 120, 80}, Upper = {45, 200, 255}     		|


<!-- <div class="row">
    <div class="large-12 columns">
        <table>
  <thead>
    <tr>
      <th width="200">Colour</th>
      <th width="150">Threshold Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>RGB White</td>
      <td>Lower = {100, 100, 200}, Upper = {255, 255, 255}</td>
    </tr>
    <tr>
      <td>RGB Yellow</td>
      <td>Lower = {100, 100, 200}, Upper = {255, 255, 255}</td>
    </tr>
    <tr>
      <td>HLS Yellow</td>
      <td>Lower = {20, 120, 80}, Upper = {45, 200, 255}</td>
    </tr>
  </tbody>
</table>
    </div>
</div>
 -->

<strong>Next</strong> is to implement this with python and some opencv functions. Below is the snippet of the function that performs this operation.


```python
		def thresh_bin_im(self, image):
		    """
		    Return the colour thresholds binary for L, S and R channels in an image
		    img: RGB image
		    """
		    def bin_it(image, threshold):
		        output_bin = np.zeros_like(image)
		        output_bin[(image >= threshold[0]) & (image <= threshold[1])]=1
		        return output_bin

		    # convert image to hls colour space
		    hls = cv2.cvtColor(image, cv2.COLOR_RGB2HLS).astype(np.float)
		    
		    # binary threshold values
		    bin_thresh = [20, 255]
		    
		    # rgb thresholding for yellow
		    lower = np.array([225,180,0],dtype = "uint8")
		    upper = np.array([255, 255, 170],dtype = "uint8")
		    mask = cv2.inRange(image, lower, upper)
		    rgb_y = cv2.bitwise_and(image, image, mask = mask).astype(np.uint8)
		    rgb_y = cv2.cvtColor(rgb_y, cv2.COLOR_RGB2GRAY)
		    rgb_y = bin_it(rgb_y, bin_thresh)
		    
		    
		    # rgb thresholding for white (best)
		    lower = np.array([100,100,200],dtype = "uint8")
		    upper = np.array([255, 255, 255],dtype = "uint8")
		    mask = cv2.inRange(image, lower, upper)
		    rgb_w = cv2.bitwise_and(image, image, mask = mask).astype(np.uint8)
		    rgb_w = cv2.cvtColor(rgb_w, cv2.COLOR_RGB2GRAY)
		    rgb_w = bin_it(rgb_w, bin_thresh)
		    
		    
		    # hls thresholding for yellow
		    lower = np.array([20,120,80],dtype = "uint8")
		    upper = np.array([45, 200, 255],dtype = "uint8")
		    mask = cv2.inRange(hls, lower, upper)
		    hls_y = cv2.bitwise_and(image, image, mask = mask).astype(np.uint8)
		    hls_y = cv2.cvtColor(hls_y, cv2.COLOR_HLS2RGB)
		    hls_y = cv2.cvtColor(hls_y, cv2.COLOR_RGB2GRAY)
		    hls_y = bin_it(hls_y, bin_thresh)
		    
		    im_bin = np.zeros_like(hls_y)
		    im_bin [(hls_y == 1)|(rgb_y==1)|(rgb_w==1)]= 1
		        
		return im_bin
```

Taking RGB threshold as an example. We define lower and upper threshold values, then we create a mask using opencv cv2.inRange() function. Next, we remove pixels that are not in the range using cv2.bitwise_and() function. At this point the image is still in RGB or HLS colour space, so we convert to grayscales and then change all the remaining pixels to binary value of 1 (bin_it() function). Find below result for each colour thresholds.

<img src="{{ site.url }}/images/lane_lines/rgb_white_threshold.png" alt="">
<img src="{{ site.url }}/images/lane_lines/rgb_yellow_threshold.png" alt="">
<img src="{{ site.url }}/images/lane_lines/hls_yellow_threshold.png" alt="">

Lastly, we combine these individual results into one for a more robust solution.

<img src="{{ site.url }}/images/lane_lines/combined_thresholded.png" alt="">

The rest of the project involves using this result to plot and fit lane lines onto the road. Find below a video of the final result.

<iframe width="560" height="315" src="https://www.youtube.com/embed/B16Fb0fPzi8" frameborder="0" allowfullscreen></iframe>

---

If you have any better ideas, please share in the comment below.

Thanks for reading.