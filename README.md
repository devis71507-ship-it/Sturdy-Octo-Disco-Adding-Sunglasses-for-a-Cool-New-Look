# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look

Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## Features:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## Technologies Used:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## How to Use:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## Applications:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## Program:
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
# Load the Face Image
faceImage = cv2.imread(r"C:\Users\sdhan\Downloads\WhatsApp Image 2026-10-17 at 3.09.40 PM.jpeg")
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```

<img width="300" height="376" alt="image" src="https://github.com/user-attachments/assets/bb598285-7d6a-4cbd-a9aa-e525b4b04484" />

```
faceImage.shape
```
(531, 413, 3)
```
# Load the Sunglass image with Alpha channel
# (http://pluspng.com/sunglass-png-1104.html)
glassPNG = cv2.imread(r"C:\iv\sunglass.jpg",-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```

<img width="496" height="273" alt="image" src="https://github.com/user-attachments/assets/6bfe1d0a-9556-4d9f-9901-72deeefd10d7" />

```
# Resize the image to fit over the eye region
glassPNG = cv2.resize(glassPNG,(210,80))
print("image Dimension ={}".format(glassPNG.shape))
```
image Dimension =(80, 210, 3)

```
# Resize sunglasses
glassBGR = cv2.resize(glassBGR, (210, 80))

# Convert sunglasses to grayscale
glassGray = cv2.cvtColor(glassBGR, cv2.COLOR_BGR2GRAY)

# Create mask to remove white background
_, glassMask1 = cv2.threshold(glassGray, 240, 255, cv2.THRESH_BINARY_INV)
# Display the images for clarity
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
<img width="750" height="182" alt="image" src="https://github.com/user-attachments/assets/841bc77e-584c-4f54-af3c-5d6cade467d3" />

```
# Make a copy
#faceWithGlassesNaive = resized_faceImage.copy()
faceWithGlassesNaive = faceImage.copy()

# Replace the eye region with the sunglass image
faceWithGlassesNaive[95:175, 100:310]=glassBGR

plt.imshow(faceWithGlassesNaive[...,::-1])
```
<img width="451" height="370" alt="image" src="https://github.com/user-attachments/assets/31099efc-0873-4943-b9ec-57fd8ee5143b" />

```
# Make the dimensions of the mask same as the input image.
# Since Face Image is a 3-channel image, we create a 3 channel image for the mask
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))

# Make the values [0,1] since we are using arithmetic operations
glassMask = np.uint8(glassMask/255)

# Make a copy
faceWithGlassesArithmetic = faceImage.copy()

# Get the eye region from the face image
eyeROI= faceWithGlassesArithmetic[95:175, 100:310]

# Use the mask to create the masked eye region
maskedEye = cv2.multiply(eyeROI,(1 - glassMask ))

# Use the mask to create the masked sunglass region
maskedGlass = cv2.multiply(glassBGR,glassMask)

# Combine the Sunglass in the Eye Region to get the augmented image
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)

# Display the intermediate results
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```

<img width="745" height="165" alt="image" src="https://github.com/user-attachments/assets/ba480e27-84ce-41a9-a9bf-74b68dc8d1a6" />


```
# Replace the eye ROI with the output from the previous section
faceWithGlassesArithmetic[95:175, 100:310]=eyeRoiFinal

# Display the final result
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
<img width="727" height="447" alt="image" src="https://github.com/user-attachments/assets/f45b83c3-aee7-438f-9338-cc219e812d00" />

## Output:

<img width="727" height="447" alt="image" src="https://github.com/user-attachments/assets/d6e9cf37-75d9-4847-991e-49d3fb2f530c" />


## Result:

Thus Adding Sunglasses to Your Passport Photo Using OpenCV is done successfully.
