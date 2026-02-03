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

Feel free to fork, contribute, or customize this project for your creative needs!
## program
```
import cv2
import numpy as np
import matplotlib.pyplot as plt
faceimage=cv2.imread("C:\\Users\\admin\\dipt\\rithika photo.jpeg")
plt.imshow(faceimage[:,:,::-1]);plt.title("face")
```

<img width="1357" height="577" alt="image" src="https://github.com/user-attachments/assets/3dad7e52-325a-4628-a393-1a45d637cdfb" />

```
glasspng=cv2.imread("C:\\Users\\admin\\Downloads\\glass.jpeg",-1)
plt.imshow(glasspng[:,:,::-1]);plt.title("GLASSPNG")
```
<img width="1218" height="405" alt="image" src="https://github.com/user-attachments/assets/c5b8ec2e-7789-4ced-afbd-0e59e5403a58" />

```
import cv2
import matplotlib.pyplot as plt
glasspng = cv2.imread("C:\\Users\\admin\\OneDrive\\Desktop\\DIPT\\glass.jpeg")
b, g, r = cv2.split(glasspng)
glass_bgr = cv2.merge((b, g, r))
gray = cv2.cvtColor(glasspng, cv2.COLOR_BGR2GRAY)

_, glass_alpha = cv2.threshold(gray, 240, 255, cv2.THRESH_BINARY_INV)

print("BGR shape:", glass_bgr.shape)
print("Alpha shape:", glass_alpha.shape)


plt.subplot(1,2,1)
plt.imshow(cv2.cvtColor(glass_bgr, cv2.COLOR_BGR2RGB))
plt.title("Sunglass BGR")
plt.axis("off")

plt.subplot(1,2,2)
plt.imshow(glass_alpha, cmap="gray")
plt.title("Generated Alpha Mask")
plt.axis("off")

plt.show()
```


<img width="1374" height="347" alt="image" src="https://github.com/user-attachments/assets/460de9ba-6442-4147-bf03-2fd34728f18b" />



```

glass_w = int(face_w * 0.60)
glass_h = int(glass_w * glassBGR.shape[0] / glassBGR.shape[1])

glassBGR = cv2.resize(glassBGR, (glass_w, glass_h))

glass_gray = cv2.cvtColor(glassBGR, cv2.COLOR_BGR2GRAY)
_, glassMask = cv2.threshold(glass_gray, 240, 255, cv2.THRESH_BINARY_INV)

glassMask = cv2.merge([glassMask, glassMask, glassMask])
glassMask = glassMask / 255.0  # normalize

x1 = int(face_w * 0.20)
y1 = int(face_h * 0.28)

x2 = x1 + glass_w
y2 = y1 + glass_h

faceWithGlasses = faceImage.copy()
eyeROI = faceWithGlasses[y1:y2, x1:x2]

eyeROI_f    = eyeROI.astype(np.float32)
glassBGR_f  = glassBGR.astype(np.float32)
glassMask_f = glassMask.astype(np.float32)

maskedEye   = cv2.multiply(eyeROI_f, (1 - glassMask_f))
maskedGlass = cv2.multiply(glassBGR_f, glassMask_f)

eyeFinal = cv2.add(maskedEye, maskedGlass)
eyeFinal = np.clip(eyeFinal, 0, 255).astype(np.uint8)

faceWithGlasses[y1:y2, x1:x2] = eyeFinal


plt.figure(figsize=(6,8))
plt.imshow(cv2.cvtColor(faceWithGlasses, cv2.COLOR_BGR2RGB))
plt.title("Final Output – Sunglasses on Eyes ")
plt.axis("on")
plt.show()


```


<img width="1388" height="847" alt="image" src="https://github.com/user-attachments/assets/cf955660-6d1c-4c0b-a9b2-a00f84e10d0a" />



```

faceWithGlassesArithmetic = faceImage.copy()

face_h, face_w, _ = faceWithGlassesArithmetic.shape

glass_w = int(face_w * 0.60)
glass_h = int(glass_w * glassBGR.shape[0] / glassBGR.shape[1])
glass_resized = cv2.resize(glassBGR, (glass_w, glass_h))

glass_gray = cv2.cvtColor(glass_resized, cv2.COLOR_BGR2GRAY)
_, glassMask = cv2.threshold(glass_gray, 240, 255, cv2.THRESH_BINARY_INV)
glassMask = cv2.merge([glassMask, glassMask, glassMask]) / 255.0

x1 = int(face_w * 0.20)
y1 = int(face_h * 0.28)
x2 = x1 + glass_w
y2 = y1 + glass_h

eyeROI = faceWithGlassesArithmetic[y1:y2, x1:x2]

eyeROI_f    = eyeROI.astype(np.float32)
glass_f     = glass_resized.astype(np.float32)
glassMask_f = glassMask.astype(np.float32)

maskedEye   = cv2.multiply(eyeROI_f, 1 - glassMask_f)
maskedGlass = cv2.multiply(glass_f, glassMask_f)
eyeFinal    = cv2.add(maskedEye, maskedGlass)
eyeFinal    = np.clip(eyeFinal, 0, 255).astype(np.uint8)

faceWithGlassesArithmetic[y1:y2, x1:x2] = eyeFinal

plt.figure(figsize=[10,10])
plt.subplot(121)
plt.imshow(cv2.cvtColor(faceImage, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(122)
plt.imshow(cv2.cvtColor(faceWithGlassesArithmetic, cv2.COLOR_BGR2RGB))
plt.title("With Sunglasses")
plt.axis("off")
plt.show()

```
<img width="1372" height="741" alt="image" src="https://github.com/user-attachments/assets/b9c0526e-bbdf-48f1-8360-db13b4184038" />




