# 🚬 Cigarette Butt Detection System

An automated system for real-time detection and localization of cigarette butts. This project combines state-of-the-art Computer Vision (YOLOv8/v11), high-performance inference on Linux, and a dedicated mobile solution for Android.

---

## 🌟 Key Features
*   **Live Detection:** Process video streams with minimal latency (optimized for 100+ FPS).
*   **Small Object Accuracy:** Fine-tuned hyperparameters and CIoU Loss implementation for precise recognition of small litter.
*   **Cross-Platform Support:** Full compatibility with Linux and Android.
*   **Flexible Export:** Seamless conversion to TFLite (for mobile and edge devices).

---

## 🛠 Tech Stack

### ML & Backend (Python)
*   **Ultralytics (YOLOv8/YOLO11):** Core Object Detection framework.
*   **PyTorch:** Model training and custom data processing.
*   **TensorFlow Lite:** High-performance model optimization for inference.
*   **uv:** Fast Python package and environment manager.

### Mobile (Android)
*   **Kotlin:** Native Android development.
*   **CameraX:** High-performance camera integration for real-time processing.

---

## 🚀 Quick Start (Desktop)

### 1. Environment Setup
It is recommended to use `uv` to create an isolated environment with stable library versions:

```bash
uv venv .yolo --python 3.11
source .yolo/bin/activate
uv pip install ultralytics torch torchvision
```
### 2. TrainingOrganize your dataset according to the YOLO format and configure data.yaml. Start the training process:
```bash
yolo task=detect mode=train \
  data=/path/to/data.yaml \
  model=yolov8n.pt \
  epochs=175 imgsz=640 batch=16
```
*NOte* Вuring the learning process, it was noticed that on my relatively small dataset of 400 images, the nano model gives results comparable to the small version, but at the same time, on the inference, the first one performs better within the FPS  

### 3. TFLite ExportTo prepare the model for the mobile application, conversion is required. Due to specific dependency requirements, use the following configuration:
```bash
uv pip install "numpy<2" "ml-dtypes==0.2.0" "tensorflow<2.16" "onnx==1.15.0"
python -c "from ultralytics import YOLO; model = YOLO('/path/to/best.pt'); model.export(format='tflite', nms=True)"
```
*Note* The `nms=True` is nessesary for Android app.  

### 4. Metrics  
On the test dataset, my model showed mAP **0.85**, which I consider to be a good result for such a noisy dataset as cigarette butts in nature.
