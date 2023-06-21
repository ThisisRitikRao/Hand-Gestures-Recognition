<h1 align = "center">CONTOUR BASED HAND GESTURE RECOGNITION </h1>
<h2> Introduction</h2>
<p align = "left">The communication between the user and the computer can be done through various
input devices such as the keyboard, mouse etc.
However this project report is based on the method of another way of communication
using hand gestures and identifying them based on image processing techniques. It is
coded in Python and uses the OpenCV library. Experiments show that the
implementation is reliable enough for practical use.</p><br>
<p>Hand gestures can be identified by various algorithms, I am going to use python
programming and more specifically open-cv(library of programming functions which
mainly aims at computer vision and it includes all those methods which deals with all
the computer vision techniques) through which hand gesture will be identified.</p>

<h2>General Architecture</h2>
The project is based on taking the gestures as input from the camera of the laptop.<br>
The whole system has been divided into various stages :<br>
1. The acquisition of image frames<br>
2.Creating a hand segmentation mask<br>
3.Using dilation and erosion for noise removal<br>
4.The most important part the contour identification stage<br>
5. Finding convexity defects and contour areas<br>
6.Identifying the gesture shown based on the contour areas and ratio<br>
<img src = "https://github.com/ThisisRitikRao/Hand-Gestures-Recognition/blob/master/gesture_images/architecture.JPG" height = 300px width = 900px>
<h2>Various stages involved</h2>
<p>Architecture diagram/ Flow diagram describes the different modules and process
involved in this project and how they are arranged.
The flow diagram given below shows the steps or tasks done to make a complete hand
gesture recognition project</p>
<img src = "https://github.com/ThisisRitikRao/Hand-Gestures-Recognition/blob/master/gesture_images/flowchart.JPG" height = 400px width = 550px>
<h2> Detailed description of modules</h2>
<h3>1.Image Frame Acquisition</h3>
<p>
<b>Main Function used = ret, frame = cap.read()</b><br>
The first stage of any vision system is the image acquisition stage. In this stage the I
will take the video as input from my laptop camera. Video is nothing but just frames
that keep on playing one after other very quickly.</p>

<h3>2.Hand Segmentation</h3>
<p>
Colour is very powerful descriptor for object detection. So for the
segmentation purpose colour information was used, which is invariant to rotation and
geometric variation of the hand . Human perceives characteristics of colour component
such as brightness, saturation and hue component than the percentage of primary
colour red, green, and blue.
For this a mask needs to be created which will segment the hand from the background.
The upper and lower skin colour range are used for the identification of hand. Than
the mask is created through this range using <b>cv2.inRange()</b> 
<img src = "https://github.com/ThisisRitikRao/Hand-Gestures-Recognition/blob/master/gesture_images/hand_segment.JPG" height = 200px width = 350px><br>
Functions used:<br>
<b>
lower_skin =
np.array([0,20,70], dtype=np.uint8)<br>
upper_skin = np.array([20,255,255],
dtype=np.uint8) <br>mask =
cv2.inRange(hsv, lower_skin,
upper_skin)</b> 
</p>

<h3>3.Erosion and Dilation</h3>
<p>
The most basic morphological operations are dilation and erosion. Dilation adds pixels
to the boundaries of objects in an image, while erosion removes pixels on object
boundaries. The number of pixels added or removed from the objects in an image
depends on the size and shape of the structuring element used to process the image<br>
<b>1. Erosion:</b><br>
• It is useful for removing small white noises.<br>
• Used to detach two connected objects etc.<br>
<b>2. Dilation:</b><br>
• In cases like noise removal, erosion is followed by dilation. Because,
erosion removes white noises, but it also shrinks our object. So we dilate
it. Since noise is gone, they won’t come back, but our object area increases.
It is also useful in joining broken parts of an object.
</p>
<h3>4. Contours identification</h3>
<p>

Functions used are:<br>
<b>Contours, hierarchy= cv2.findContours(mask, cv2.RETR_TREE,
cv2.CHAIN_APPROX ) <br>cnt = max(contours, key = lambda x: cv2.contourArea(x))</b><br>
In this step we focus on finding or forming the boundary along the segmented hand as
contour is nothing but join of all continuous or similar values the function is applied
over the mask we made.

</p>
<h3>5. Getting convexity defects and contour area</h3>
<p>


Functions used:<br>
<b>
hull = cv2.convexHull(cnt)<br>
areahull = cv2.contourArea(hull)<br>
areacnt = cv2.contourArea(cnt)<br>
arearatio=((areahull-areacnt)/areacnt)*100<br>
cv2.convexHull(approx, returnPoints=False)<br> 
defects = cv2.convexityDefects(approx, hull)<br></b>

Given a set of points in the plane. the convex hull of the set is the smallest convex
polygon that contains all the points of it.
<img src = "https://github.com/ThisisRitikRao/Hand-Gestures-Recognition/blob/master/gesture_images/contour.JPG" height = 150px width = 350px><br>
Thus in this step a boundary or overlapping object kind of thing is being made and
then the convexity defects are find out which are like gaps between the fingers and I
draw a dot kind of structure representing different different numbers taking contour
area also In consideration.<br><br>
<img src = "https://github.com/ThisisRitikRao/Hand-Gestures-Recognition/blob/master/gesture_images/contour2.JPG" height = 200px width = 400px><br>
</p>

<h3>6.Identifying gesture</h3>
<p>
At last for every defect we calculate some angles between the fingers and the number
of defects which is used for identifying the gesture. Based on different different values
of the output parameters like area of the contour we classify the input getures.</p>
<img src = "https://github.com/ThisisRitikRao/Hand-Gestures-Recognition/blob/master/gesture_images/gesture.JPG" height = 200px width = 300px>

<h2> Software Requirments</h3>
<p>
The entire project has been developed using python language.I have taken python
because it has many good modules and packages which can be imported and their
functions can be used.
Particularly for image processing python contains open-cv library:
<br>
<b>OpenCV (Open Source Computer Vision) </b>is a library of programming functions
mainly aimed at real-time computer vision. In simple language it is library used for
Image Processing. It is mainly used to do all the operation related to Images.
It contains inbuilt functions for many processing and enhancement related work like:<br>
<b>1.Cv2.VideoCapture()<br>
2.Cv2.recatngle()<br>
3.Cv2.inrange()<br>
4.Cv2.erode()<br>
5.Cv2.dilate()<br>
6.Cv2.cvtColor()</b> …. And many more such functions<br>
Next requirement is to<b> import numpy </b>which is used to handle multi-dimensional
arrays , specifically as images are 2d representation of pixels numpy is used to handle
operations on them.<br>
All the OpenCV array structures are converted to and from Numpy arrays. This also
makes it easier to integrate with other libraries that use Numpy such as <b>SciPy and
Matplotlib.</b>
Also to perform mathematical operations on the images we will need to <b>import the
math module</b> present in python which also has certain functions like sqrt abs and other.
<img src = "https://github.com/ThisisRitikRao/Hand-Gestures-Recognition/blob/master/gesture_images/softw_req.JPG" height = 250px width = 680px>
</p>
