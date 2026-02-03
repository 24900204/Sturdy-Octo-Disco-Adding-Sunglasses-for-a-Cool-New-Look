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


import cv2
import matplotlib.pyplot as plt

face_img = cv2.imread(r"C:\Users\admin\Downloads\rithika photo.jpeg")
face_gray = cv2.cvtColor(face_img, cv2.COLOR_BGR2GRAY)

glass_bgr = cv2.imread(r"C:\Users\admin\Downloads\glass.jpeg")
gray = cv2.cvtColor(glass_bgr, cv2.COLOR_BGR2GRAY)
_, glass_alpha = cv2.threshold(gray, 240, 255, cv2.THRESH_BINARY_INV)

eye_cascade = cv2.CascadeClassifier(cv2.data.haarcascades + "haarcascade_eye.xml")
eyes = eye_cascade.detectMultiScale(face_gray, 1.2, 5)

h, w = face_img.shape[:2]

eyes = [e for e in eyes if e[1] < h // 2]

eyes = sorted(eyes, key=lambda x: -x[2])[:2]

if len(eyes) == 2:
    eyes = sorted(eyes, key=lambda x: x[0])
    x1, y1, w1, h1 = eyes[0]
    x2, y2, w2, h2 = eyes[1]

    left_eye = (x1 + w1 // 2, y1 + h1 // 2)
    right_eye = (x2 + w2 // 2, y2 + h2 // 2)

    eye_distance = int(((right_eye[0] - left_eye[0]) ** 2 + (right_eye[1] - left_eye[1]) ** 2) ** 0.5)
    glasses_w = int(eye_distance * 2.0)
    glasses_h = int(glass_bgr.shape[0] * (glasses_w / glass_bgr.shape[1]))

    glasses_resized = cv2.resize(glass_bgr, (glasses_w, glasses_h))
    mask_resized = cv2.resize(glass_alpha, (glasses_w, glasses_h))

    center_x = (left_eye[0] + right_eye[0]) // 2
    center_y = (left_eye[1] + right_eye[1]) // 2
    x_offset = center_x - glasses_w // 2 + 20   # move right
    y_offset = center_y - glasses_h // 2 - 27   # move up

    y1, y2 = max(0, y_offset), min(h, y_offset + glasses_h)
    x1, x2 = max(0, x_offset), min(w, x_offset + glasses_w)

    mask_resized = mask_resized[0:y2 - y1, 0:x2 - x1]
    glasses_resized = glasses_resized[0:y2 - y1, 0:x2 - x1]
    roi = face_img[y1:y2, x1:x2]

    mask_inv = cv2.bitwise_not(mask_resized)
    bg = cv2.bitwise_and(roi, roi, mask=mask_inv)
    fg = cv2.bitwise_and(glasses_resized, glasses_resized, mask=mask_resized)

    combined = cv2.add(bg, fg)
    face_img[y1:y2, x1:x2] = combined


plt.imshow(cv2.cvtColor(face_img, cv2.COLOR_BGR2RGB))
plt.axis("off")
plt.title("Face with Glasses")
plt.show()
```


<img width="1388" height="847" alt="image" src="https://github.com/user-attachments/assets/cf955660-6d1c-4c0b-a9b2-a00f84e10d0a" />



```
import matplotlib.pyplot as plt
import cv2

plt.figure(figsize=(10,5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(faceimage, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(face_img, cv2.COLOR_BGR2RGB))
plt.title("With Glasses")
plt.axis("off")

plt.show()
```



<img width="1376" height="700" alt="image" src="https://github.com/user-attachments/assets/bfaa7269-3f83-48aa-a71c-ae565373f6a2" />
