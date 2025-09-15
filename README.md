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

### Developed by: Naveen Kumar V
### Register Number: 212223230140

```
import cv2
import matplotlib.pyplot as plt
import numpy as np
faceImage = cv2.imread('passport.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img width="425" height="435" alt="download" src="https://github.com/user-attachments/assets/3b481ec5-b428-49d8-b336-4ae28b8c5752" />

```
glassPNG = cv2.imread('glasses.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
<img width="542" height="435" alt="download" src="https://github.com/user-attachments/assets/5923d6d4-3d3c-441c-854e-6a87fa45311b" />

```
glassPNG = cv2.resize(glassPNG,(200,120))
print("image Dimension ={}".format(glassPNG.shape))
glassBGR = glassPNG[:,:,0:3]
glassMask1 = glassPNG[:,:,3]
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
<img width="1218" height="383" alt="download" src="https://github.com/user-attachments/assets/f1e89d8c-645f-4a9b-8c9d-ded991c18e51" />

```
faceWithGlassesNaive = faceImage.copy()
faceWithGlassesNaive[135:255, 116:316] = glassBGR
plt.imshow(faceWithGlassesNaive[...,::-1])
```
<img width="425" height="418" alt="download" src="https://github.com/user-attachments/assets/5684fcb3-42c4-49f1-b623-0970dca8579d" />

```
glassMask = cv2.merge((glassMask1,glassMask1,glassMask1))
glassMask = np.uint8(glassMask/255)
faceWithGlassesArithmetic = faceImage.copy()
eyeROI= faceWithGlassesArithmetic[135:255, 116:316]
maskedEye = cv2.multiply(eyeROI,(1-  glassMask ))
maskedGlass = cv2.multiply(glassBGR,glassMask)
eyeRoiFinal = cv2.add(maskedEye, maskedGlass)
plt.figure(figsize=[20,20])
plt.subplot(131);plt.imshow(maskedEye[...,::-1]);plt.title("Masked Eye Region")
plt.subplot(132);plt.imshow(maskedGlass[...,::-1]);plt.title("Masked Sunglass Region")
plt.subplot(133);plt.imshow(eyeRoiFinal[...,::-1]);plt.title("Augmented Eye and Sunglass")
```
<img width="1606" height="339" alt="download" src="https://github.com/user-attachments/assets/6d12e216-78b3-43c4-ab64-960244adb0e8" />

```
faceWithGlassesArithmetic[135:255, 116:316]=eyeRoiFinal
plt.figure(figsize=[20,20]);
plt.subplot(121);plt.imshow(faceImage[:,:,::-1]); plt.title("Original Image");
plt.subplot(122);plt.imshow(faceWithGlassesArithmetic[:,:,::-1]);plt.title("With Sunglasses");
```
<img width="1606" height="770" alt="download" src="https://github.com/user-attachments/assets/b415cfe4-e153-4d80-b67e-9ba93f5e3a3d" />


Feel free to fork, contribute, or customize this project for your creative needs!
