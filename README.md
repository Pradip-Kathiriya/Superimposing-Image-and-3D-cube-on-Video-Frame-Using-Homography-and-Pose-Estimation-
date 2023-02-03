# Superimposing-Image-and-3D-cube-on-Video-Frame-Using-Homography-Estimation-

### Project Description:

This Project is divided into two parts:
1. In part 1, I have used the concepts of projective geometry and homographies to project an image on a scene in a way that respects perspective. To demonstrate this, I have projected Testudo (University of Maryland's mascot) image into the video frame. We are provided with the Testudo image and video with AprilTag. Our task is to track the april tag by identifying its corner, decode the april tag to indetify its orientation, and perfrom the warping to project the Testudo in the place of AprilTag in the video frame.

2. In part 2, I have used the tracking and pose estimation from projective transformation to implement a simple augemented reality application. There are two steps in this process. First, identify the AprilTag and get the position of the corner across different frames. Then, we have to use the homography estimation to compute the 3D pose of a set of 4 points in the world and, instead of simply overlaying image like in part 1, render a 3D object in a frame. For simplicity we will be rendering a cube, but in principle, any object could be used. The goal is to form a set of 4 points on the image with known coordinates(AprilTag), find the necessary position and orientation to draw the cube over the points.

Input video:


![1tagvideo_AdobeExpress](https://user-images.githubusercontent.com/90370308/216509501-92cef3d1-141d-4ce1-ba4f-b7fa5b74b39a.gif)

Testudo Image:


![testudo](https://user-images.githubusercontent.com/90370308/216509638-b587a724-e8a8-4cd5-938c-ebf6b5ee89d4.png)

### Results:

Apply FFT and Low pass filter to detect edges and corners in the frame


![Q1_A_output](https://user-images.githubusercontent.com/90370308/216510160-4b00c196-a3cd-4399-9430-daed298e9b61.png)
Apply [Shi-Tomashi](https://opencv24-python-tutorials.readthedocs.io/en/latest/py_tutorials/py_feature2d/py_shi_tomasi/py_shi_tomasi.html) corner detector to detect the corner in the images. Upon futher preprocessing and using simple geometry, we can detect corner of the AprilTag.

Using the 4 detected corner and the testudo image's corner, compute the homography matrix and perform the inverse warping to transport the pixel from testudo image to the AprilTag. It is worth noting that we need perform the inverse warping, because if we compute the forward warping and project all the Testudo points into the video frame, we will most likely have the case where multiple testudo points project to one video frame pixel(due to rounding of the pixels), while other pixels may have no testudo points at all. This results in 'Holes' in the video frame where no testudo points are mapped.To avoid this, we calculate the projection from video frame points to testudo points
to guarantee that every video frame gets a point from the testudo image.

Result for part 1:

![Testudo_imposed_AdobeExpress](https://user-images.githubusercontent.com/90370308/216512844-044bd934-a6ec-4db6-8040-f2e5646f870b.gif)

Results for part 2:

![cube_imposed_AdobeExpress](https://user-images.githubusercontent.com/90370308/216512944-e20929f4-e12e-4787-a2ca-795e05968879.gif)

## Requirement
Python 2.0 or above

## License

 [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Copyright (c) Feb 2023 Pradip Kathiriya

