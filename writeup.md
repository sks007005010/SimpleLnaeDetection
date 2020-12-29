# **Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* **Make a pipeline that finds lane lines on the road
* **Reflect on your work in a written report


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 4 steps.

**Step 1:-**
    Read the image and convert to grayscale, making sure that use we read it in BGR or RGB.As canny edge detection require 
    graysacle image
    
**Step 2:-**
    Applying Gaussian smoothness to remove unwanted noise, and apply canny edge detection on the smoothned image
    **edges = cv2.Canny(gray, low_threshold, high_threshold)**
    canny edge detection is algorithm to find the edges in the given image, it is done by taking the derivative of contrast 
    between two adjacent pixel

**Step 3:-**
    We extract only the area which is useful to us and remove other unneccesary area from image
    
**Step 4:-**
    Output of canny edge detection is a series of dots which needs to be connected in line to make a lane, but what kind will
    be based the parameter given to hough transform parameters
    **cv2.HoughLinesP(masked_edges, rho, theta, threshold, np.array([]),min_line_length, max_line_gap)**
    rho and theta will define the size of one pixel in our new hough space.
    threshold defines minimun no of dots in the given pixel should be to make it to output
    min_line_length, max_line_gap are self explanatory where min_line_length defines minimu length of line in pixel to make it to output
    and max line gap is the maximum distance (again, in pixels) between segments that you will allow to be connected into a single line.

**In order to draw a single line on the left and right lanes, modification in draw_lines() function are as follows**
    First seperate the co-ordinates of left lane and right lane by finding the slope of the line, as in image space origin isnon the 
    top   left corner -ve and +ve slope as we see in x-y cordinate will be different, I have taken a note of it.
    Now fit the co-ordinates of left lane and right lane in a line using numpy polyfit function
    from poly fit we will get line in mx+c form hence to convert the co-ordinates in two point form do some processing 
    i.e we have Slope(m) and (c) by fixing one point we can get the othewr points.
    Now we have to point for each lane we can plot a line to form a lane.
    
### 2. Identify potential shortcomings with your current pipeline

One of the potential shortcoming is it doesnot work for curved line, and also I found that when there is change in the road from
shadow to bright spot algorithm fails. 


### 3. Suggest possible improvements to your pipeline

We can fit the curved line with polyfit function to identify the curved lanes.
Also there are some instance where right_lane or left_lane array in draw_line() is a null array, and it throws and exception hence 
handling these type of condition can be included in improvements of my code.
















    
    
    