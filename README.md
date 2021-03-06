# Edgedetection

## Objective:
Document Detection helps in differentiating the receipt from the background of an image which would help to decrease the workload of OCR. The overall process was seen to be faster/equally fast in most cases when the background was removed.

## Detailed Explanation behind the steps involved:

### Extension of his Image: 
It helps to extend the borders of the image so that it helps in the further steps. We extend it by 25 pixels on all the sides.
### Median Filter: Params(Filter size=51)
Median Filter has been used in edge detection to extract the edge pixels of the receipt. Unlike other image smoothening filters,Median filter helps in removing the noises while preserving the edges in the image.The function smoothens an image using the median filter with the Filter_size* Filter size aperture. Each channel of a multi-channel image is processed independently.The value 51 was chosen by trial and error.
### Colour Transformation(Colour Space):
We convert the three channel image to a black and white image so that (1)computation is simplified and (2) we don’t need the colour information for the further steps. Using cvtcolor function of opencv we transform colour image to grayscale image.
### Edge Detection with canny edge detector:
Canny edge detection algorithm is a multi-stage algorithm. First Algorithm removes noise by using a Gaussian filter of size 5*5. 

Then the second stage involves the search of the image Intensity Gradient. The image is filtered with a Sobel kernel both in vertical and horizontal direction, thus obtaining the first derivatives in the two directions (Gx and Gy). From these two images, you then find the edge gradient G. 

The next stage is the Not-maximum Suppression, where some unwanted pixels are removed so they will not be confused as edge. To do this, the entire image is analysed, checking if each pixel is a local maximum in the direction of the gradient relative to its area.

Finally the last stage is the application of the Hysteresis Thresholding. In this final stage the algorithm determines which edges are real edge and those who are not at all. For this you must determine two threshold values, the minVal the minimum threshold, and maxVal the maximum threshold. Any edge with an intensity gradient greater than maxval is sure to be an edge, and those with a value less than minVal will be discarded, because they are nor real edge. For all other edge that may be found in the range between these two threshold values, are subjected to a further analysis, establishing whether they are real edges through their connectivity. If they are connected to an edge of those already detected, then it is also considered as such, otherwise discarded.
For Canny edge Detector, you pass in min val and max val as parameters.
### Finding Contours:
Contours can be explained simply as a curve joining all the continuous points (along the boundary), having same color or intensity. The contours are a useful tool for shape analysis and object detection and recognition. There are three arguments in cv2.findContours() function, first one is source image, second is contour retrieval mode, third is contour approximation method. 
                  The purpose of contour approximation is given a curve composed of line segments (which is also called a Polyline in some contexts), to find a similar curve with fewer points. The algorithm defines 'dissimilar' based on the maximum distance between the original curve and the simplified curve .The simplified curve consists of a subset of the points that defined the original curve.
                  The output are the image, contours and hierarchy .Contours is a Python list of all the contours in the image. Each individual contour is a Numpy array of (x,y) coordinates of boundary points of the object.
We sort the contours according to the area and check for the longest contour.
### Finding Polygons enclosing the Contour and choosing 4 corners:
   Once we obtain the longest contour, we use the function approxPolyDP to find the Polygon enclosing the contour. It takes the parameter (contour,epsilon and information whether the contour is closed or open).
It approximates a contour shape to another shape with less number of vertices depending upon the precision we specify as epsilon and returns the shape.
We identify the 4 corners by their property and copy it as new image.
                            
## How to run the program :
Insert your file address as the input and stages as well as the output file will get saved.
The algorithm would work its best if receipt is a significant part of the Image and as long as the background is different from the receipt. If the above conditions are met, then the receipt contour would be picked up as the biggest contour and we can extract the receipt from the background.
## Requirements:
Opencv and Numpy
python                                         
                                              
                                              
                                              
                                              
                                              

