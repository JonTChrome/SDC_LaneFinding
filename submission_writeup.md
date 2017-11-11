# **Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

### Implemented Pipeline
I started implementing the pipeline using the the code given to us directly in the writeup and the process shown in the lessons:
1: convert image to grayscale
2: Gaussian blurr the image to reduce noise
3: Use the canny algorithm to detect edges
4: mask a sub-region of the image
5: Detect line segments using the Hough Space transforms with the parameters tuned for selecting lane lines
* this is where the modifications to the pipeline begin
6: Given the segments from the Hough transform, seperate them to left/right based on the slope and find the minimum/maximum points in the region
7: Using these min/max points, calculate the slope and midpoint and use these values to calculate a new line to be drawn across the entire region of interest.  Using y = mx + b calculate b, then calculate the x coordinates where y is the top and bottom of the region of interest.  
8: I attempted to keep a memory of the previous slopes and define a tolerance where if the new calculated slope wasnt within the tolerance, discard it and use the mean slope


### 2. Identify potential shortcomings with your current pipeline
1: This pipeline didnt detect proper hough lines in some of the frames of the videos and the pipeline doesnt have a failsafe for that case resulting in skipped frames with no lines
2: When detecting the left and right slopes it doesnt immediately throw away slopes that are outside the tolerance/mean, so it lets a lot of noise through and this is extremely evident when running the challenge video
3: Finding the min/max points for each side might not be the best way to extrapolate lines, im imaging averaging all slopes within a tolerance and averaging all b values perhaps, id have to implement and test it to find out


### 3. Suggest possible improvements to your pipeline
One thing that I wanted to move around was the slope tolerance calculation right after finding the hough lines to minimize the noise getting through my line-extrapolation routines.  If i apply the averaging method to the slope and constant calculation up-front I think would be a lot more accurate and resilient algorithm

Like I said above, Im sure there is a better way to average the lines than finding the min max, it just wasnt obvious to me but I think I would get far better results if I did the filtering up-front