## Project: Search and Sample Return
### Writeup Template: You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

---


**The goals / steps of this project are the following:**

**Training / Calibration**

* Download the simulator and take data in "Training Mode"
* Test out the functions in the Jupyter Notebook provided
* Add functions to detect obstacles and samples of interest (golden rocks)
* Fill in the `process_image()` function with the appropriate image processing steps (perspective transform, color threshold etc.) to get from raw images to a map.  The `output_image` you create in this step should demonstrate that your mapping pipeline works.
* Use `moviepy` to process the images in your saved dataset with the `process_image()` function.  Include the video you produce as part of your submission.

**Autonomous Navigation / Mapping**

* Fill in the `perception_step()` function within the `perception.py` script with the appropriate image processing functions to create a map and update `Rover()` data (similar to what you did with `process_image()` in the notebook).
* Fill in the `decision_step()` function within the `decision.py` script with conditional statements that take into consideration the outputs of the `perception_step()` in deciding how to issue throttle, brake and steering commands.
* Iterate on your perception and decision function until your rover does a reasonable (need to define metric) job of navigating and mapping.

[//]: # (Image References)

[image1]: ./misc/rover_image.jpg
[image2]: ./calibration_images/example_grid1.jpg
[image3]: ./calibration_images/example_rock1.jpg

## [Rubric](https://review.udacity.com/#!/rubrics/916/view) Points
### Here I will consider the rubric points individually and describe how I addressed each point in my implementation.

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one.  You can submit your writeup as markdown or pdf.

You're reading it!

### Notebook Analysis
#### 1. Run the functions provided in the notebook on test images (first with the test data provided, next on data you have recorded). Add/modify functions to allow for color selection of obstacles and rock samples.

Both provided test images and my recorded images can be run on the notebook.

Since the obstacle and navigable terrain are just opposite to each other, I add a boolean to the `color_thresh()` function to control whether or not the input is for navigable terrain. Then I add a similar function called `color_thresh_rocks()` to identify the rock samples. Inside the `color_thresh_rocks()` function, I set the lower bound and uppper bound for each of the RGB channels.

#### 1. Populate the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Run `process_image()` on your test data using the `moviepy` functions provided to create video output of your result.

I modified the `process_image()` function step by step according to the comment:
a. define source and destination points for perspective transform
b. apply perspective transform
c. apply color threshold to identify navigable terrain/obstacles/rock samples
d. convert thresholded image pixel values to rover-centric coords
e. update world map for navigable terrain/obstacles/rock samples
f. append output images

My modified `process_image()` function can map pixels identifying navigable terrain, obstacles and rock samples into a worldmap. I also generated 2 output videos to represent my results. The output videos can be found in my submission attachment.

### Autonomous Navigation and Mapping

#### 1. Fill in the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.

I modified the `perception_step()` at the botoom of the `perception.py` script, using the same steps that can be found in the jupyter notebook. When updating the `Rover.vision_image`, I multiply the binary image with 255 for each RGB channel so that it's visible from the video.

I didn't modify the `decision_step()` function since it's already capable to navigate the map autonomously.

#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.

My results show that my autonomous rover can map 80% of the environment and 65% fidelity and locate 2 of the rock samples. I think I can improve the results by making the "decision" more accurate. For example, maybe I can add a feature to avoid duplicate routes or to avoid obstables.

**Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines!  Make a note of your simulator settings (resolution and graphics quality set on launch) and frames per second (FPS output to terminal by `drive_rover.py`) in your writeup when you submit the project so your reviewer can reproduce your results.**

My resolution is 1024 x 768 and "Fantastic" graphic quality in Mac environment. The FPS is 28.

Here I'll talk about the approach I took, what techniques I used, what worked and why, where the pipeline might fail and how I might improve it if I were going to pursue this project further.

The techniques I used are from the lecture contents and Slack community. If I were going to puruse this project further, I think I can let the rover collect all the rock samples and return to the starting point.

![alt text][image3]


