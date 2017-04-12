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

My pipeline has 3 major steps that it does twice for each vertical split of an image.

1. Preprocessing
2. Lane line detection
3. Drawing onto original image

A basic verision of my pipeline was achievable by performing these three actions only once on the entire image with a change in how lanes are drawn. The basic version processed each image individually and drew what it believed to be the lane for that frame. This caused flickering lanes as lane markings entered and exited the scene. To mitigate this, I used an average of the detected lane lines over several frames. The average is more fitting since frames of a driving video are not unrelated but continue in sequence. This worked well but the averaging functionality required that I process and record the right and left lane lines individually. 


###2. Identify potential shortcomings with your current pipeline


A major potential shortcoming with this method is that it doesn't respond well to curves in the road. By averaging the lane lines over time, a previous straight lane line can override a upcoming curve.


###3. Suggest possible improvements to your pipeline

Potential improvements are:
  1) Have a configurable lane cache size. 
  2) Project the road segment of the image to a new coordinate space so the camera would seem to be right above the road. Then run the hough line transform over this image and project the detected lane lines back onto the original image. I've had pretty decent results with this in another repo [here](https://github.com/WarrenGreen/LaneDetection).
  3) Stack several frames onto eachother with a low opacity and run the Hough Transform on this composition. Perhaps this would allow you to draw lines using the data from several frames.