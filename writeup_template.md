# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---


[//]: # (Image References)

[image2]: ./output_imagesWrite.md/gaussian_Blur.jpg "Grayscale"

---

[//]: # (Image References)

[image3]: ./output_imagesWrite.md/canny_edges.jpg "Grayscale"

---

[//]: # (Image References)

[image4]: ./output_imagesWrite.md/masked_image.jpg "Grayscale"

---

[//]: # (Image References)

[image5]: ./output_imagesWrite.md/final.jpg "Grayscale"

---

[//]: # (Image References)

[image6]: ./output_imagesWrite.md/hough+extrapolation.jpg "Grayscale"

---


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. The step5 covers the explanation of draw_lines function was modified.

1. First, I converted the input image to grayscale image. The image is shown below:

![alt text][image1]

2. Then gaussian blur was applied to reduce the noise. The output of the gausiian image is :

![alt text][image2]

3. After the gausian blur,  cany edge detection Algorithm was applied to detect edges from the blurred image. Canny edge detection helps to provide edges in an image. 

![alt text][image3]

4. The next step was to calculate the are of interest. We need to ignore the surroundings and only choose area of the lane.
So we mask the image, use fillPoly function to fill the pixels inside the image given by the vertices.

![alt text][image4]

5. Finally after selecting the area of interest, it was the most interesting and challenging aspect of the project.
   Hough Transform and the extrapolation of the lines. Initially Hough transform was applied using inbuilt openCV functions.
   Then the algorithm for extrapolation of lines was developed. 
   Below were the steps used for extrapolation of lines:
    a. Identify left lines and right lines.
      The left lines have a negative slope , because as y increases , x decreases.
      The right lines have a positive slope, because as y increases, x increases.
    b. Loop through the list of lines, separate left lanes,rightlanes, left slope, right slope, left intercept and right intercept and 
      store them all in separate list.
    c. Calculate the avergare slope, x,y for both left and right lanes. 
    c. Now we need maxY, minY for left and right lanes to draw the extrapolated the lines.
    d. the maxY = height of the image and the minY is found through iteration .
    e. Finally we substitute, the mean values and calculted X values to finally calculate the X coordinates.
    f. Finally with calculated X coordiantes and y , we draw the lines.
 
 The image  after applying hough tranform and extrapolation is shown below:
 
 ![alt text][image6]
 
 6.Finally we add the original image to the lines obatained through extrapolation as mentioned in point 5. 
 And below is the output.
 
 ![alt text][image5]    



### 2. Identify potential shortcomings with your current pipeline


I see below shortcomings on the project.
1. As the lanes start turning, the left and right lanes sometimes looks like they are converging.
   The extrapolated lines tend to converge.
2. Another shortcoming is on the challenge video.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to to see how extrapolation of lines could be made more efficient.

Another potential improvement could be to explore on the challenge video. Currently the extrapolation of lines doesnot work for challenge video.
