# **Finding Lane Lines on the Road** 

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. 

First, I change the image to hsv color format. Then I used yellow mask and white
mask to mask out the interested color regions. 

Second, I change the masked image into grayscale. 

Third, I applied gaussian blur to grayscaled image.

Fourth, I used Canny edge detection. Where I set low threshold as 0 and high
threshold as 200.

Fifth, masking interesting area applied. Which I set four vertices as
[[(0,y),(x*0.475, 0.555*y),(x*0.525,0.555*y),(x,y)]], where x=image.shape[0] and
y=iamge.shape[1].

Next, Hough transormation applied. where my settings are
```python
    rho = 1 # distance resolution in pixels of the Hough grid
    theta = np.pi/180   # angular resolution in radians of the Hough grid
    threshold = 10     # minimum number of votes (intersections in Hough grid cell)
    min_line_length = 2 #minimum number of pixels making up a line
    max_line_gap = 10  # maximum gap in pixels between connectable line segments
```

I also change the function that drawing the lines. First, I caculate the slope
of each line. And only remain the line with absolute value of slope larger than
0.4. Then I classified the line into left line and right line base the sign of
their slope. 

Then I apply the function **np.polyfit** to fitting the Lane. Then using
cv2.line to draw it.


![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

- The interesting area might not accurate since once car changing the lane,
  lane might not in same place of the image.
- It can only identify the straight lane. Cannot classify the curve line, like
  what happened in challenge part.
- Color masking might not very accurate.


### 3. Suggest possible improvements to your pipeline

- Change the color threshold to make it more accurate.
- Change the region mask to make it more accurate.
- Optimize the draw_line function to make it more robust to curve line.

