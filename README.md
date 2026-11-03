# Experiment 4: Record-Image Transformations

### Name: Parani Bala M
### Reg.no: 212224230192

## Aim
To perform geometric transformations on an image using Python and OpenCV, including translation, scaling, shearing, reflection, rotation, and cropping.

## Objectives
- To load and display an input image.
- To translate an image horizontally and vertically.
- To resize an image using scaling factors.
- To perform image shearing using an affine transformation matrix.
- To reflect an image using the OpenCV flip function.
- To rotate an image by a specified angle.
- To crop a selected region from an image.
- To visualize the original and transformed images using Matplotlib.

## Software Requirements
- Python 3.x
- Jupyter Notebook
- OpenCV (`cv2`)
- NumPy
- Matplotlib
- Input image: `My_Image.png`

## Algorithm
1. Start the program.
2. Import OpenCV, NumPy, and Matplotlib libraries.
3. Load the input image using `cv2.imread()`.
4. Display the original image.
5. Perform **translation** by shifting the image 100 pixels horizontally and 50 pixels vertically.
6. Perform **scaling** using horizontal and vertical scaling factors of 5.0 and 2.0.
7. Perform **shearing** using an affine transformation matrix.
8. Perform **reflection** using `cv2.flip()`.
9. Rotate the image by 45 degrees using `cv2.getRotationMatrix2D()`.
10. Crop a region of width 200 pixels and height 150 pixels from the specified coordinates.
11. Display each transformed image using Matplotlib.
12. Stop the program.

## Program

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Step 1: Load the image
image = cv2.imread('My_Image.png')  # Load the image from file

# Display the original image
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))  # Convert BGR to RGB for correct display
plt.title("Original Image")
plt.axis('off')

# Step 2: Image Translation
tx, ty = 100, 50  # Translation factors (shift by 100 pixels horizontally and 50 vertically)
M_translation = np.float32([[1, 0, tx], [0, 1, ty]])  # Translation matrix:
# [1, 0, tx] - Horizontal shift by tx
# [0, 1, ty] - Vertical shift by ty
translated_image = cv2.warpAffine(image, M_translation, (image.shape[1], image.shape[0]))

plt.imshow(cv2.cvtColor(translated_image, cv2.COLOR_BGR2RGB))  # Display the translated image
plt.title("Translated Image")
plt.axis('off')

# Step 3: Image Scaling
fx, fy = 5.0, 2.0  # Scaling factors (1.5x scaling for both width and height)
scaled_image = cv2.resize(image, None, fx=fx, fy=fy, interpolation=cv2.INTER_LINEAR)
# resize: Resize the image by scaling factors fx, fy
# INTER_LINEAR: Uses bilinear interpolation for resizing

plt.imshow(cv2.cvtColor(scaled_image, cv2.COLOR_BGR2RGB))  # Display the scaled image
plt.title("Scaled Image")  # Set title
plt.axis('off')

# Step 4: Image Shearing
shear_matrix = np.float32([[1, 0.5, 0], [0.5, 1, 0]])  # Shearing matrix
# The matrix shears the image by a factor of 0.5 in both x and y directions
# [1, 0.5, 0] - Shear along the x-axis (horizontal)
# [0.5, 1, 0] - Shear along the y-axis (vertical)
sheared_image = cv2.warpAffine(image, shear_matrix, (image.shape[1], image.shape[0]))

plt.imshow(cv2.cvtColor(sheared_image, cv2.COLOR_BGR2RGB))  # Display the sheared image
plt.title("Sheared Image")
plt.axis('off')

# Step 5: Image Reflection
reflected_image = cv2.flip(image, 2)  # Flip the image horizontally (1 means horizontal flip)
# flip: 1 means horizontal flip, 0 would be vertical flip, -1 would flip both axes

plt.imshow(cv2.cvtColor(reflected_image, cv2.COLOR_BGR2RGB))  # Display the reflected image
plt.title("Reflected Image")
plt.axis('off')

# Step 6: Image Rotation
(height, width) = image.shape[:2]  # Get the image height and width
angle = 45  # Rotation angle in degrees (rotate by 45 degrees)
center = (width // 2, height // 2)  # Set the center of rotation to the image center
M_rotation = cv2.getRotationMatrix2D(center, angle, 1)  # Get the rotation matrix
# getRotationMatrix2D: Takes the center of rotation, angle, and scale factor (1 means no scaling)
rotated_image = cv2.warpAffine(image, M_rotation, (width, height))  # Apply rotation

plt.imshow(cv2.cvtColor(rotated_image, cv2.COLOR_BGR2RGB))  # Display the rotated image
plt.title("Rotated Image")
plt.axis('off')

# Step 7: Image Cropping
x, y, w, h = 100, 100, 200, 150  # Define the top-left corner (x, y) and the width (w) and height (h) of the crop
# Cropping the image from coordinates (x, y) to (x+w, y+h)
cropped_image = image[y:y+h, x:x+w]
# The crop is performed by slicing the image array in the y and x directions

plt.imshow(cv2.cvtColor(cropped_image, cv2.COLOR_BGR2RGB))  # Display the cropped image
plt.title("Cropped Image")
plt.axis('off')
```
## Output:
<img width="1523" height="602" alt="image" src="https://github.com/user-attachments/assets/01ffc1bc-3b8e-490a-97ae-2f59dbf7246d" />
<img width="1516" height="595" alt="image" src="https://github.com/user-attachments/assets/649f3128-8a62-4df8-966e-59e598f82b73" />
<img width="1506" height="427" alt="image" src="https://github.com/user-attachments/assets/72ac7337-c6a1-4720-9119-a941cbf32550" />
<img width="1508" height="591" alt="image" src="https://github.com/user-attachments/assets/f47e747b-3283-4574-ab44-3946503472c1" />
<img width="1505" height="613" alt="image" src="https://github.com/user-attachments/assets/f0121e39-9fbc-4590-8561-b75fdf5fd97b" />
<img width="1515" height="597" alt="image" src="https://github.com/user-attachments/assets/830547ef-fdf7-4c98-826a-6830b79d83f7" />
<img width="1502" height="616" alt="image" src="https://github.com/user-attachments/assets/577eb526-48c9-4dfb-9c38-d265dec05ff6" />

## Result
Geometric transformations were performed on the input image using OpenCV. The original image and the translated, scaled, sheared, reflected, rotated, and cropped images were displayed successfully using Matplotlib.
