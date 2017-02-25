#**Finding Lane Lines on the Road** 
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
First, I converted the images to grayscale, then I do gaussian blur on it with kernel size 5;
And then I apply Canny edge detection on blurred image, with low threashold 30 and high threashold 60;
After edge detection step, I use an interest region to crop out the detected edges out side.
At final step, I use Hough transform to find the lines.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by:
1. classify the detected lines to left and right group, by calculating it's slop;
2. for each line, extend it to the top and bottom line of interest region, discard the lines which have ending points out of visible region;
3. average left and right group's ending points, then draw the lane lines.


###2. Identify potential shortcomings with your current pipeline


There are many possible shortcommings:

1. when the car is in large degree depart the lane, which will make the predefined ROI less effective;
2. when the car/road is heading upwards or downwards, ROI setting and line detection would be less effective too;
3. when the lane lines' marks are not in good visible condition, the Canny edge detection maybe not so effective;
4. the final lines are not so steady


###3. Suggest possible improvements to your pipeline
Possible improvements:

1. Try use and find some camera/geometry information, for example, vanishing points, to help set and update ROI, which will lead line detection more effective;
2. Use color information to help edge detection more precise;
3. Use temperal relationship on video processing to make result more stable
