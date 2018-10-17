# Color Q
Color Q is a free mobile application developed in Java for the Google Play Store. The app was developed in the Android Studio v3.2.1 integrated development environment. It works alongside the Chrome-Q hardware also developed by Lambert iGEM in order to effectively quantify the result of a biological reporter, similar to the function of a plate reader. The app is able to use circle detection in order to find the samples on the base of the Chrome-Q hardware and then detect the red, green, and blue values (RGB) of the center of each circle. The way the circles are arranged allow for a range of values to be generated. The first row contains 4 circles. The average RGB values of the first two circles are calculated as the negative control and the average RGB values of the second pair of circles are calculated as the positive control. The distance between the positive and negative control is calculated in the 3D-coordinate plane using the following formula: 

<br>

<div style="text-align:center;"><img style="text-align:center;" src="http://2018.igem.org/wiki/images/e/eb/T--Lambert_GA--distance.png" /></div>

<br>

The Hough Circle Transform is used as the method of circle detection found in the app. Open Computer Vision (OpenCV) is a library that can be imported into Android Studio in order to perform image analysis-based methods. The image taken by the smartphone camera is converted into a grayscale photo. This essentially makes the image more readable in terms of edge detection and "round" estimation. There are several parameters that can be modified and calibrated in order to detect an accurate amount of circles: 

- Maximum Radius: The smallest value for the radius of a detected circle
- Minimum Radius: The largest value for the radius of a detected circle
- Minimum Distance: The smallest distance between the centers of any two detected circles
- Edge Gradient Value: The roundness of each detected circle
- Threshold Value: The amount of memory the system has to store the detected circles

The 6 by 6 grid located underneath the first row can be loaded with experimental samples and a percentage value can be determined on a scale from the negative control to the positive control. The circle detection process loops through until the maximum radius reaches 120 pixels. If anywhere from 35 to 40 circles are detected in total, then the loop stops. However, if there are fewer circles detected, then the loops restarts to finish through the maximum radius until anywhere from 25 to 40 circles are detected properly. If less than 25 circles are detected, then an error is caught and another picture is requested to be used. Zooming in or zooming out could possibly make the circle detection process easier for the system and more efficient. The following formula is used to calculate the relative percentage values: 

<br>

<div style="text-align:center;"><img style="text-align:center;" src="http://2018.igem.org/wiki/images/0/0b/T--Lambert_GA--value.png" /></div>

<br>

The results are then displayed based upon the row in which the circles fall in on the base of the Chrome-Q hardware. The app is able to determine the row in which the circles fall in by comparing y-coordinates. If the y-values are similar to each other, then the circles are classified as being on the same row. The relative values are then transferred to another page within the app where the user is able to enter information that could help contribute to our machine learning model, CALM. The application uses the latitude, longitude, and timestamp values obtained from the phone's GPS to effectively determine where and when the test was run. When the user submits the data, the results are sent to a MySQL database, which is a part of the Relational Database Service (RDS) as a part of the Amazon Web Services (AWS) platform. 
