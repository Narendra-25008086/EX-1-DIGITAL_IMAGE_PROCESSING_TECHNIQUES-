# EX-1-DIGITAL_IMAGE_PROCESSING_TECHNIQUES-

# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** KARNAM PAREESH NAIDU 
- **Register Number:** 212225230129

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
~~~
eagle_gray = cv2.imread("Eagle_in_Flight.jpg", cv2.IMREAD_GRAYSCALE)
assert eagle_gray is not None, "Eagle image not found"
print("Grayscale image loaded successfully")```
~~~
## OUTPUT:
![alt text](image.png)
## 2. Print the image width, height & Channel.
~~~
height, width = eagle_gray.shape
channels = 1
print(f"Width: {width} pixels\nHeight: {height} pixels\nChannels: {channels}")
~~~
## OUTPUT:
![alt text](image-1.png)
#### 3. Display the image using matplotlib imshow().
~~~
plt.figure(figsize=(9, 5))
plt.imshow(eagle_gray, cmap="gray", vmin=0, vmax=255)
plt.title("Eagle – Grayscale")
plt.axis("off")
plt.show()
~~~
## OUTPUT:
![alt text](image-2.png)
#### 4. Save the image as a PNG file using OpenCV imwrite().
~~~
saved = cv2.imwrite("eagle_grayscale.png", eagle_gray)
print("Saved eagle_grayscale.png:", saved)
~~~
## OUTPUT:
![alt text](image-3.png)
#### 5. Read the saved image above as a color image using cv2.cvtColor().
~~~
eagle_bgr = cv2.imread("eagle_grayscale.png", cv2.IMREAD_COLOR)
assert eagle_bgr is not None
eagle_from_png_rgb = cv2.cvtColor(eagle_bgr, cv2.COLOR_BGR2RGB)
print("Color image shape:", eagle_from_png_rgb.shape)
# For the following crop exercise, reload the original COLOR photograph.
eagle_original_bgr = cv2.imread("Eagle_in_Flight.jpg", cv2.IMREAD_COLOR)
eagle_rgb = cv2.cvtColor(eagle_original_bgr, cv2.COLOR_BGR2RGB)
~~~
## OUTPUT:
![alt text](image-4.png)
#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
~~~
plt.figure(figsize=(9, 5))
plt.imshow(eagle_rgb)
plt.title("Original Eagle – Color")
plt.axis("off")
plt.show()
h, w, c = eagle_rgb.shape
print(f"Width: {w}, Height: {h}, Channels: {c}")
~~~
## OUTPUT:
![alt text](image-5.png)
#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
~~~
eagle_crop = eagle_rgb[20:445, 200:555]
plt.figure(figsize=(7, 5))
plt.imshow(eagle_crop)
plt.title("Cropped Eagle")
plt.axis("off")
plt.show()
print("Cropped shape:", eagle_crop.shape)
~~~
## OUTPUT:
![alt text](image-6.png)
#### 8. Resize the image up by a factor of 2x.
~~~
eagle_resized = cv2.resize(eagle_crop, None, fx=2, fy=2, interpolation=cv2.INTER_CUBIC)
plt.figure(figsize=(7, 6))
plt.imshow(eagle_resized)
plt.title("Eagle – 2× Resize")
plt.axis("off")
plt.show()
print("Original crop:", eagle_crop.shape, "Resized:", eagle_resized.shape)
~~~
## OUTPUT:
![alt text](image-7.png)
#### 9. Flip the cropped/resized image horizontally.
~~~
eagle_flipped = cv2.flip(eagle_resized, 1)
plt.figure(figsize=(7, 6))
plt.imshow(eagle_flipped)
plt.title("Eagle – Horizontal Flip")
plt.axis("off")
plt.show()
~~~
## OUTPUT:
![alt text](image-8.png)
#### 10. Read in the image ('Apollo-11-launch.jpg').
~~~
apollo_bgr = cv2.imread("Apollo-11-launch.jpg", cv2.IMREAD_COLOR)
assert apollo_bgr is not None
apollo_rgb = cv2.cvtColor(apollo_bgr, cv2.COLOR_BGR2RGB)
print("Apollo image shape:", apollo_rgb.shape)
plt.figure(figsize=(10, 6))
plt.imshow(apollo_rgb)
plt.axis("off")
plt.show()
~~~
## OUTPUT:
![alt text](image-9.png)
#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
~~~
apollo_annotated = apollo_bgr.copy()
caption = "Apollo 11 Saturn V Launch, July 16, 1969"
h, w = apollo_annotated.shape[:2]
font = cv2.FONT_HERSHEY_SIMPLEX
scale = min(0.9, w / 1100)
thickness = 2
(text_w, text_h), baseline = cv2.getTextSize(caption, font, scale, thickness)
x = max(0, (w - text_w) // 2)
y = h - 30
cv2.putText(apollo_annotated, caption, (x, y), font, scale, (255, 255, 255), thickness, cv2.LINE_AA)
plt.figure(figsize=(11, 6))
plt.imshow(cv2.cvtColor(apollo_annotated, cv2.COLOR_BGR2RGB))
plt.title("Apollo 11 – Caption Added")
plt.axis("off")
plt.show()
~~~
## OUTPUT:
![alt text](image-10.png)
#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
~~~
cv2.rectangle(apollo_annotated, (480, 55), (705, 630), (255, 0, 255), 4)
print("Magenta rectangle drawn")
~~~
## OUTPUT:
![alt text](image-11.png)
#### 13. Display the final annotated image.
~~~
plt.figure(figsize=(12, 7))
plt.imshow(cv2.cvtColor(apollo_annotated, cv2.COLOR_BGR2RGB))
plt.title("Apollo 11 – Annotated Launch")
plt.axis("off")
plt.show()
cv2.imwrite("apollo_annotated.png", apollo_annotated)
~~~
## OUTPUT:
![alt text](image-12.png)
#### 14. Read the image ('Boy.jpg').
~~~
boy_bgr = cv2.imread("boy.jpg", cv2.IMREAD_COLOR)
assert boy_bgr is not None
boy_rgb = cv2.cvtColor(boy_bgr, cv2.COLOR_BGR2RGB)
print("Boy image shape:", boy_rgb.shape)
plt.figure(figsize=(8, 5))
plt.imshow(boy_rgb)
plt.axis("off")
plt.show()
~~~
## OUTPUT:
![alt text](image-13.png)
#### 15. Adjust the brightness of the image.
~~~
brightness_matrix = np.full(boy_rgb.shape, 50, dtype=np.uint8)
print("Brightness change:", brightness_matrix[0, 0])
~~~
## OUTPUT:
![alt text](image-14.png)
#### 16. Create brighter and darker images.
~~~
boy_brighter = cv2.add(boy_rgb, brightness_matrix)
boy_darker = cv2.subtract(boy_rgb, brightness_matrix)
~~~

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
~~~
fig, ax = plt.subplots(1, 3, figsize=(14, 4))
for a, im, title in zip(ax, [boy_rgb, boy_darker, boy_brighter], ["Original", "Darker (−50)", "Brighter (+50)"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
~~~
## OUTPUT:
![alt text](image-15.png)
#### 18. Modify the image contrast.
~~~
def adjust_contrast(image, alpha):
    return np.clip((image.astype(np.float32) - 128) * alpha + 128, 0, 255).astype(np.uint8)

boy_lower_contrast = adjust_contrast(boy_rgb, 0.8)
boy_higher_contrast = adjust_contrast(boy_rgb, 1.2)
# Additional 1.1× result, as mentioned in the supplied exercise:
boy_contrast_1_1 = adjust_contrast(boy_rgb, 1.1)
~~~


#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
~~~
fig, ax = plt.subplots(1, 3, figsize=(14, 4))
for a, im, title in zip(ax, [boy_rgb, boy_lower_contrast, boy_higher_contrast], ["Original", "Lower contrast (0.8×)", "Higher contrast (1.2×)"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
~~~
## OUTPUT:
![alt text](image-16.png)
#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
~~~
b, g, r = cv2.split(boy_bgr)
fig, ax = plt.subplots(1, 3, figsize=(13, 4))
for a, channel, title in zip(ax, [b, g, r], ["Blue", "Green", "Red"]):
    a.imshow(channel, cmap="gray", vmin=0, vmax=255); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
~~~
## OUTPUT:
![alt text](image-17.png)
#### 21. Merged the R, G, B , displays along with the original image
~~~
merged_rgb = cv2.merge([r, g, b])
fig, ax = plt.subplots(1, 2, figsize=(11, 4))
for a, im, title in zip(ax, [boy_rgb, merged_rgb], ["Original RGB", "Merged RGB"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
print("Identical:", np.array_equal(boy_rgb, merged_rgb))
~~~
## OUTPUT:
![alt text](image-18.png)
#### 22. Split the image into the H, S, V components & Display the channels.
~~~
hsv_img = cv2.cvtColor(boy_bgr, cv2.COLOR_BGR2HSV)
hue, saturation, value = cv2.split(hsv_img)
fig, ax = plt.subplots(1, 3, figsize=(13, 4))
for a, ch, title in zip(ax, [hue, saturation, value], ["Hue (0–179)", "Saturation (0–255)", "Value (0–255)"]):
    a.imshow(ch, cmap="gray"); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
~~~
## OUTPUT:
![alt text](image-19.png)
#### 23. Merged the H, S, V, displays along with original image.
~~~
merged_hsv = cv2.merge([hue, saturation, value])
restored_bgr = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)
restored_rgb = cv2.cvtColor(restored_bgr, cv2.COLOR_BGR2RGB)
fig, ax = plt.subplots(1, 2, figsize=(11, 4))
for a, im, title in zip(ax, [boy_rgb, restored_rgb], ["Original RGB", "Restored from HSV"]):
    a.imshow(im); a.set_title(title); a.axis("off")
plt.tight_layout(); plt.show()
print("Max rounding difference:", np.abs(boy_rgb.astype(int) - restored_rgb.astype(int)).max())
~~~
## OUTPUT:
![alt text](image-20.png)
## Output:
- **i)** Read and Display an Image.  
- **ii)** Adjust Image Brightness.  
- **iii)** Modify Image Contrast.  
- **iv)** Generate Third Image Using Bitwise Operations.

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.
