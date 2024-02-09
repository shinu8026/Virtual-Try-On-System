Online fashion shopping often suffers from difficulty visualizing outfits and the environmental impact of unnecessary returns. This project seeks to address these issues by creating a virtual try-on system that allows users to visualize different clothing items on their body without physically trying them on, promoting informed purchase decisions and reducing returns.


## Utilized Methodologies

The GrabCut algorithm was used to segment the user and clothing images. 
For Pose Estimation of the user, MediaPipe Library has been used. 
Perspective Transformation has been used for Warping and Clothing Alignment
Weighted composition of user and clothing images for Virtual Try-On image

## Method:1 
There are four functions:

1. Segmentor: 
        Arguments: image_path, image_type
        In this function, image is being segmented using GrabCut Algorithm.
2. try_on_clothing:Args(user_image, clothing_image, keypoints)
        i.Reading User and Clothing image and creating and extracting a mask of the clothing image and scaling the clothing image inorder to fit according to the user image.
        ii.Aligning Clothing image based on the keypoints, that are being calculated in the pose estimator function.  
        iii.A transformation matrix that describes how to map the points from the original image to the desired output image,is being calculated.This is commonly used in tasks like image stitching or perspective correction.
        iv.This transformation matrix is used for warping of the clothing image and the user image. 
        v. The above created mask is being resized according to the user image. 
        vi. bitwise AND is being performed and the image retained is where mask is zero/black. 
        vii. addWeighted is being used in order to get the blend of the user and the warped image, known as composite image. 
3. pose_estimator: Args(user_image_path)
        Pose estimation is being performed using the MediaPipe Open Source Framework.It easily works with computer vision tasks, such as recognizing body poses in images or videos. It's used because it's user-friendly, works in real-time, can be used on different devices, and allows customization to fit specific needs.
4. align_and_convert_color: Args(clothing_image_path, user_image)
        Resizing the clothing image and finding contours in the image after converting it to the grayscale iamge. 
        Finding contours process is done iteratively untill the largest contour is being found in order to get the exact/nearest-accurate boundary box around the object/clothing.

Now, segmentor is being executed for the User Image and as for the Clothing image, first align_and_convert_color() is being executed and then the segmentor().

Finding the body keypoints using the pose estimator().
Alligning the specific body parts to the clothing image.



