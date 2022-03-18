# Description
Program to remove speckle  (salt and pepper) noise from images. Two common filters in this are implemented in this  project: 

1.	Alpha-trim filter 

2.	Adaptive median filter
 
The main idea of both filters is to sort the pixel values in a neighborhood region with certain window size and then chose/calculate the single value from them and 
places it in the center of the window in a new image, see figure 1. This process is repeated for all pixels in the original image

![Screenshot 2022-03-18 214854](https://user-images.githubusercontent.com/75753459/159073899-8a153a36-7a7e-4cb0-96b8-e60cffc1ca9a.png)

# First: Alpha-trim filter
The idea is to calculate the average of some neighboring pixels' values after trimming out (excluding) the smallest T pixels and largest T pixels. This can be done by repeating the following steps for each pixel in the image:   

1.	Store the values of the neighboring pixels in an array. The array is called the window, and it should be odd sized.

2.	Sort the values in the window in ascending order.

3.	Exclude the first T values (smallest) and the last T values (largest) from the array.

4.	Calculate the average of the remaining values as the new pixel value and place it in the center of the window in the new image.

This filter is usually used to remove both salt & pepper noise and random noise. 

![Screenshot 2022-03-18 215055](https://user-images.githubusercontent.com/75753459/159074162-406b57e5-98ef-4271-ac89-92a1b1e1e16f.png)
Alpha-trim filter implemented with TWO different algorithms: 

1.	Counting Sort

2.	Selecting Kth smallest element in the array without sorting it (Textbook sec. 9.2). where K = T to exclude the smallest T values, then on the remaining array, apply the algorithm again to exclude the largest T values. Finally, calculate the average of the remaining values

# Second: Adaptive Median Filter
The idea of the standard median filter is similar to alpha-trim filter but instead we calculate the median of neighboring pixels' values (middle value in the window array after sorting). 

It's usually used to remove the salt and pepper noise.

However, the standard median filter has the following drawbacks:

1.	It fails to remove salt and pepper noise with large percentage (greater than 20%) without causing distortion in the original image.

2.	It usually has a side-effect on the original image especially when it’s applied with large mask size, see figure 2 with window 7×7. 
Adaptive median filter is designed to handle these drawbacks by:

  1.	Seeking a median value that’s not either salt or pepper noise by increasing the window size until reaching such median.
  
  2.	Replace the noise pixels only. (i.e. if the pixel is not a salt or a pepper, then leave it).

![Screenshot 2022-03-18 215400](https://user-images.githubusercontent.com/75753459/159074520-aa79841a-437d-4510-9a6c-df067e9bc438.png)

Adaptive median filter implemented with TWO different algorithms: 

1.	Quick Sort

2.	Counting Sort

# Timing graphs:
1.	Display two graphs to show the execution time against different window sizes (3, 5, 7,… Wmax), where Wmax is user input.

   1.	One graph for alpha-trim filter to compare its two methods (counting & selecting kth element)
   
   2.	Another graph for adaptive median filter to compare its two methods (quick & counting).

