# Road Distresses Detection using YOLOv8

This repository contains a custom-trained YOLOv8 model designed to detect road surface distresses such as cracks, potholes, edge breaks, and similar defects. The goal is to assist in automating road condition monitoring using computer vision techniques.

## 🚀 Features

* ✅ Real-time detection of road distresses using YOLOv8
* 🧠 Trained on custom-labeled dataset merged from three sources via CVAT
* 📈 High performance:

  * Precision: 89.43%
  * Recall: 90.01%
  * mAP\@0.5: 95.37%
  * mAP\@0.5:0.95: 82.40%
* 🔬 Built-in validation & metrics evaluation
* 🎥 Supports inference on images, videos (including YouTube), and live streams

---

## 📁 Project Structure

```
Road_Distresses_Detection/
├── best.pt
├── data.yaml
├── images/
├── labels/
├── rough.py
├── Road_Distresses_Detection_Modal.ipynb
├── sample.png
└── README.md
```

* **best.pt**: Trained YOLOv8 model weights
* **data.yaml**: Dataset configuration (train/val paths, class names)
* **images/** & **labels/**: YOLO-format images and annotations
* **rough.py**: Local evaluation/inference script
* **Road\_Distresses\_Detection\_Modal.ipynb**: Colab notebook (T4 GPU)
* **sample.png**: Example output image

---

## 📦 Dataset

**Merged from three sources:**

1. Road Cracks (\~154 images)
2. Potholes & Cracks (\~200 images)
3. Pothole Segmentation (\~720 images)

**Final dataset (with train/val split) available here:**
[Google Drive Download](https://drive.google.com/file/d/1iPH18ZAMuSe0ejRngGtWCRXjXDnATU3R/view?usp=sharing)

**Classes (9):**

```
0: Low_Cracking
1: Medium_Cracking
2: High_Cracking
3: minor_pothole
4: moderate_pothole
5: major_pothole
6: Minor_Edge_Break
7: Modrate_Edge_Break
8: Major_Edge_Break
```

**Example `data.yaml`:**

```yaml
train: ./dataset/train/images
val: ./dataset/val/images
nc: 9
names: [
  'Low_Cracking', 'Medium_Cracking', 'High_Cracking',
  'minor_pothole', 'moderate_pothole', 'major_pothole',
  'Minor_Edge_Break', 'Modrate_Edge_Break', 'Major_Edge_Break'
]
```

---

## 🔧 Installation

```bash
pip install ultralytics opencv-python
```

---

## 🧪 Evaluation

```python
from ultralytics import YOLO

model = YOLO("best.pt")
metrics = model.val(data="data.yaml", imgsz=640, batch=2, device='0')  # GPU recommended

print(f"Precision:   {metrics.box.precision * 100:.2f}%")
print(f"Recall:      {metrics.box.recall * 100:.2f}%")
print(f"mAP@0.5:     {metrics.box.map50 * 100:.2f}%")
print(f"mAP@0.5-0.95 {metrics.box.map * 100:.2f}%")
```

---

## 🧠 Inference Examples

* **Image:**

  ```python
  results = model.predict(source='sample.jpg', save=True)
  ```
* **YouTube Video:**

  ```python
  import cv2
  cap = cv2.VideoCapture('https://youtube.com/shorts/gqLAY02FarA?si=3QihWb1i9Rm7XVAU')
  ```
* **Live Stream/Webcam:**

  ```python
  cap = cv2.VideoCapture(0)
  ```

---

## 📓 Google Colab Notebook

Open `Road_Distresses_Detection_Modal.ipynb` to:

* Mount Google Drive
* Install dependencies
* Upload model & dataset
* Auto split train/val
* Evaluate & visualize predictions on T4 GPU

---

## 💡 Future Work

* Web deployment (Flask/Streamlit)
* Larger, more diverse dataset
* Geo-tagging of detected distresses

---

## 📬 Contact

Feel free to open an issue or connect via GitHub for questions and contributions.
