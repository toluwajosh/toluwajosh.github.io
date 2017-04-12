---
layout: post
title: "Kalman Filter: Predict, Measure, Update, Repeat."
description: 
headline: 
modified: 2017-04-11
category: Projects
tags: [Learning, MOOC]
imagefeature: 
mathjax: true
chart: 
comments: true
featured: false
---

[//]: # (Image References)
[image1]: ./images/lane_lines/dachcam_view.jpg "View from camera mounted in car."

In systems where we need to obtain continuous or dynamic measurements from sensors, there is usually a challenge that the sensors' measurements are uncertian due to reasons which include, but are not limited to, errors from sensor, discrepant measurement from multiple sensors. Kalman filter helps us to obtain more reliable estimates from a sequence observed measurements. This post is meant to give a general idea of the Kalman filter in a simplistic and concise manner. It however requires a little familiarity with the subject, but I will do a little introduction.

Suppose we want to track the position of an obstacle ahead of a robot, we would like to be certain about the measurement obtained from the range sensor on the robot because we would not want the robot to collide into an obstacle while it 'thinks' the obstacle is still far ahead. Depending on the inaccuracy or noise present in our sensor, we might get a reading that looks like this:

<!-- example image display -->
<figure>
<img src="{{ site.url }}/images/kalman_filter/sensor_reading.jpg" width="600" photo_title="Measurement from sensor" alt="Measurement from sensor">
<figcaption>Fig1. - Distance-from-obstacle measurement from a robot sensor.</figcaption>
</figure>

This kind of reading is pretty unreliable, so we need the Kalman filter to give us a better estimate. Another advantage is that we can be able to make our estimate from multiple sensors, further reducing the uncertainty in our estimations.

Kalman filter algorithm can be roughly organised under the following steps:
1. We make a prediction of a state, based on some previous values and model.
2. We obtain the measurement of that state, from sensor.
3. We update our prediction, based on our errors
4. Repeat.

Having given the general introduction, it is good to note that our prediction comes from our knowledge of the system. For example, if we are tracking the position and velocity of an object, we would use a model that follows the equation of motion for prediction. I will use the example of tracking position and velocity to explain the rest of the post. Our model can be represented as follows:

$$
\begin{array}{l}
p'_{x}=p_{x} + v_{x} \Delta t + \frac{a_{x} \Delta t^2 }{2} \\ 
p'_{y}=p_{y} + v_{y} \Delta t + \frac{a_{y} \Delta t^2 }{2} \\
v'_{x}=v_{x} + a_{x} \Delta t \\
v'_{y}=v_{y} + a_{y} \Delta t
\end{array}
$$
 
In matrix form as:

$$
\left( \begin{array}{l}
p'_{x} \\
p'_{y} \\
v'_{x} \\
v'_{y}
\end{array}
\right) = 
\left( \begin{array}{cccc}
1 & 0 & \Delta t & 0 \\
0 & 1 & 0 & \Delta t \\
0 & 0 & 1 & 0 \\
0 & 0 & 0 & 1
\end{array}
\right)
\left( \begin{array}{l}
p_{x} \\
p_{y} \\
v_{x} \\
v_{y}
\end{array}
\right) +
\left( \begin{array}{l}
\frac{a_{x} \Delta t^2 }{2} \\
\frac{a_{y} \Delta t^2 }{2} \\
a_{x} \Delta t \\
a_{y} \Delta t 
\end{array}
\right)
$$

Or:

$$
X' = F'X + U
$$

Where $p$ is the position, $v$ velocity and $a$ acceleration. We call $F$ transition matrix and $U$ control variable matrix. In most typical cases, velocity is assumed to be constant, but $U$ accounts for acceleration when this is not true.
We also need to estimate the uncertainty in our estimation. This can be expressed by the state covariance matrix:

$$
P' = F'PF^T + Q
$$

Where $Q$ is the process noise covariance matrix, which is used to keep the state covariance matrix from becoming too small or going to zero

#### Kalman Gain

An important element of the Kalman filter is the Kalman gain. I like to see it as the regulator between our estimate and the measurement. As you would see in the equation of the gain in the following figure, the Kalman gain 'decides' based on error from previous estimations, which of either the estimate or measurement to give more weight to. Intuitively, if we are making a good prediction, then the Kalman gain works to cancel out the effect of new measurements, but if we are making bad estimates, then it gives weight to the new measurements to make subsequent predictions. The figure below shows the general flow and overview of the Kalman filter.

<figure>
<img src="{{ site.url }}/images/kalman_filter/kf_overview.jpg" width="900" photo_title="overview of the Kalman filte" alt="overview of the Kalman filte">
<figcaption>Source: <a href="https://www.youtube.com/watch?v=CaCcOwJPytQ&list=PLX2gX-ftPVXU3oUFNATxGXY90AULiqnWT">Special Topics - The Kalman Filter</a></figcaption>
</figure>

#### Extended Kalman Filter

The extended Kalman filter (EKF) is a way of incorporating measurements from multiple sensors to make more robust estimations. It is able to deal with sensors presenting measurements in different different dimensions.

In our case of tracking the position and velocity of an object, we could use laser or radar range sensors. However, while laser sensors represent measurements in cartesian coordinate, the radar sensors represent in polar coordinate. A direct conversion of polar coordinate to cartesian coordinate gives nonlinearity and so Kalman filter is no more useful. Hence, we have to be able to linearly map from the polar coordinate to the cartesian coordinate. EKF uses the method called [first order Taylor expansion](http://mathworld.wolfram.com/TaylorSeries.html) to obtain linear approximation of the polar coordinate measurements in the update. In this process, a Jacobian matrix is produced, which represents the linear mapping from polar to cartesian coordinate, applied at the update step. Hence, the conversion matrix $H$ becomes the Jacobian matrix $H_{j}$, while we will use non-linear state transition and measurement functions for both prediction and update respectively. The resulting EKF general flow and overview is shown:

<figure>
<img src="{{ site.url }}/images/kalman_filter/ekf_overview.jpg" width="900" photo_title="overview of the Kalman filte" alt="overview of the Kalman filte">
<figcaption>Extended Kalman Filter</figcaption>
</figure>

<!-- $$\mathbf{X} = \left[\begin{array}
{rrr}
1 & 2 & 3 \\
4 & 5 & 6 \\
7 & 8 & 9
\end{array}\right]
$$ -->


<!-- attempt to use shortcode from afam website -->
<!-- <blog-post-photo photo_url="{{ site.url }}/images/lane_lines/dashcam_view.jpg" photo_title="Cover" photo_title="Pre-trip Orientation" width="700"> -->

<!-- | Colour 		| Threshold Values   										| 
|:-------------:|:--------------------------------------------------------:	| 
| RGB White     | Lower = {100, 100, 200}, Upper = {255, 255, 255}       	| 
| RGB Yellow 	| Lower = {225, 180, 0}, Upper = {255, 255, 170} 			|
| HLS Yellow 	| Lower = {20, 120, 80}, Upper = {45, 200, 255}     		| -->


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

<!-- <iframe width="560" height="315" src="https://www.youtube.com/embed/B16Fb0fPzi8" frameborder="0" allowfullscreen></iframe> -->

---

The EKF is a very broad and useful topic which cannot be done justice to in a single post. I have however highlighted areas which I personally found a bit confusing when working on the algorithm for a project on the SDCND program. Check the following links for more detailed explanation of the subject.

- [The Extended Kalman Filter: An Interactive Tutorial for Non-Experts](https://home.wlu.edu/~levys/kalman_tutorial/)

- [Special Topics - The Kalman Filter (Video Tutorial)](https://www.youtube.com/watch?v=CaCcOwJPytQ&list=PLX2gX-ftPVXU3oUFNATxGXY90AULiqnWT)

If you would like to know about the project I applied this algorithm on, check [the project repository here](https://github.com/toluwajosh/CarND-EKF-Project).

If you find any inconsistency in my post, please feel free to point out in the comments. I'm still a learner.

Thanks for reading.


<!-- Original post for 2 years in ML -->
<!-- I started my journey into Machine Learning (ML) about two years ago when I was a research student getting ready to start a PhD in System Information Science. For me, this was new area since I had a background in Mechanical Engineering, so I had to bring myself up to speed with the skills that I would need during my research. 

A this time, I was an absolute newbie in ML. I was new to python programming, and had very minimal knowledge in computer science. However, I was determined to learn all I needed. 

To quickly introduce the subject of ML. I would like to define ML in my own way


After my first meeting with my supervisor, I knew I would have a lot of learning to do. First I had to take an intensive course in Japanese Language which lasted for 4 months. At this time, I was not able to do many other things, so I actually didn't start learning much about ML till after the Japanese Language course. However, I was able to read parts of the book [Machine Learning with python](). This was my very first introduction ML. After a while into the book and doing some of the practices, I knew I needed to take a course in python for a better knowledge of the language. I took the online [Edx]() course [Introduction to Computer Science with Python](). I soon understood the field of ML was constantly changing so I needed a more robust background. So I took the course [Introduction to ML]() by [Andrew Ng]() which is considered the quintessential course for introduction to ML. 



How do I rate myself now

I wrote a post about 'how to learn something new'. [Check it out here]().

If you would also like to know about how I came to Japan to start a research in ML, [You can the full story here]().  -->
