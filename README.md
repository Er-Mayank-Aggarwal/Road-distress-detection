
# Road Distresses Detection using YOLOv8

This repository contains a custom-trained YOLOv8 model designed to detect road surface distresses such as cracks, potholes, edge breaks, and similar defects. The goal is to assist in automating road condition monitoring using computer vision techniques.

## 🚀 Features

- ✅ Real-time road distress detection using YOLOv8
- 🧠 Trained on custom-labeled dataset using CVAT
- 📈 High performance:
  - Precision: 89.43%
  - Recall: 90.01%
  - mAP@0.5: 95.37%
  - mAP@0.5:0.95: 82.40%
- 🔬 Validation & metrics evaluation supported
- 🎥 Supports video input (live or offline)

---

## 📁 Project Structure

```
📦 Road_Distresses_Detection
│
├── best.pt                     # Trained YOLOv8 model weights
├── data.yaml                   # Dataset configuration file
├── images/                     # Images used for training/validation
├── labels/                     # Corresponding YOLO-format labels
├── rough.py                    # Evaluation/inference script
├── Road_Distresses_Detection_Modal.ipynb  # Colab-compatible notebook
├── sample.png                  # Sample output image
└── README.md                   # Project overview (this file)
```

---

## 📦 Dataset

- Collected and labeled using [CVAT](https://cvat.org/)
- Format: YOLO
- Classes: 
  - 0: Crack
  - 1: Pothole
  - 2: Edge Break

Make sure your data.yaml looks like this:

```yaml
train: images/train
val: images/val
nc: 3
names: ['Crack', 'Pothole', 'Edge Break']
```

---

## 🔧 Requirements

Install dependencies:

```bash
pip install ultralytics
```

You may need to restart your runtime or environment after installing.

---

## 🧪 Evaluation

Run evaluation using:

```python
from ultralytics import YOLO

model = YOLO("best.pt")
metrics = model.val(data="data.yaml", imgsz=640, batch=2, device='cpu')

print(f"Precision: {metrics.box.precision * 100:.2f}%")
print(f"Recall: {metrics.box.recall * 100:.2f}%")
print(f"mAP@0.5: {metrics.box.map50 * 100:.2f}%")
print(f"mAP@0.5:0.95: {metrics.box.map * 100:.2f}%")
```

---

## 🧠 Inference (Image / Video)

Predict on an image:

```python
results = model("path/to/image.jpg", save=True)
```

---

## 📓 Notebook

Use the Road_Distresses_Detection_Modal.ipynb notebook to:

- Run model on Google Colab with T4 GPU
- Upload dataset + weights
- Perform validation & inference interactively
- View annotated results

---

## 📊 Results

| Metric          | Value   |
|-----------------|---------|
| Precision       | 89.43%  |
| Recall          | 90.01%  |
| mAP@0.5         | 95.37%  |
| mAP@0.5:0.95    | 82.40%  |

---

## 💡 Future Improvements

- Deploy as a web app using Streamlit or Flask
- Expand dataset with more edge cases
- Add support for GPS tagging in images

---

## 🙌 Acknowledgments

- Model: [Ultralytics YOLOv8](https://docs.ultralytics.com/)
- Annotation Tool: [CVAT](https://cvat.org/)
- Hosted on: Google Colab (T4 GPU)

---

## 📬 Contact

For any issues or questions, feel free to open an issue or connect via GitHub.
