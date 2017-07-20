# Finding Lane Lines on the Road

# Reflection

## Description
My pipeline consisted of 5 steps. 

1. I converted the images to grayscale.

2. Apply Guassian Smoothing to blur the grayscale image.

3. Apply thresholding using a low threshold and a high threshold by Canny.

4. Define the vertices of a trapezium to apply an image mask, to ignore the area outside the considered area.

5. Do Hough Transform on the image from step 4. Get the lines/edges after the transformation. 

6. In order to get one single line for the left edge and one single line for the right edge:

  * Consider the slope for all the lines from step 5.
  * If the slope is positive, the line needs to be on the right.
  * Hence both endpoints of the line need to be on the right side of the whole image.
  *  Note that the line that is too steep or too flatten would not be part of the lane line. Hence, we consider only the line with slope in range 0.5 to 1.5 as potential right line.
  *  If we extend the line such that it reaches the bottom of the image. If the x-value of the bottom endpoint of the line is out of the image, i.e., out of range, the line would not be part of the lane line. Hence, we do not include these lines in potential right lines. 
  * Take an average on the endpoints of the potential right lines, such that we would have the endpoints for only one line. Extend the line to the bottom.

  * Do the similar to lines on the left. 

7. Draw the lines on the original image. 

## Potential Shortcomings
As in the video challenge.mp4, there are a few images which the left yellow solid line was not identified when the line was under the sun and hence faded. 

When the color of the line on the road does not significantly differ from the background color of the road, the line would not be identified. 

## Possible Improvements
1. In the grayscale step, improve the weight the red and green which makes yellow.

2. In the Canny step, modify the thresholds to be more adequate numbers. 

3. In the drawing line step, modify the order of extending the length of lines and averaging the vertices of the line. Such that each line would have the same weight. 
