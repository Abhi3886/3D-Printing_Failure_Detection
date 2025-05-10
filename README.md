
# 🧠 3D Printing Failure Detection using YOLOv8 and ESP32-CAM

## 📌 Project Overview

This project aims to **automatically detect failures during 3D printing** using computer vision and machine learning. A YOLOv8 model was trained to recognize different types of 3D print failures in real-time. The trained model was then deployed alongside an **ESP32-CAM** to capture live print images and detect failures, allowing the system to stop or alert the user and prevent material waste.

---

## 🎯 Key Objectives

- Detect 3D print failures like **Spaghetti**, **Layer Shifts**,**Over Extrusion**, **Under Extrusion** and **Stringing**.
- Use a **YOLOv8 object detection model** for accurate detection.
- Deploy the system with **ESP32-CAM** for real-time inference.
- Improve efficiency and reduce waste in 3D printing.

---

## 🗂️ Dataset Preparation

- Combined multiple publicly available datasets with our oun custom prepared dataset on 3D print failures.
- Annotated images using **Roboflow**, creating bounding boxes for:
  - `Spaghetti`
  - `Layer_Shift`
  - `Over_Extrusion`
  - `Under_Extrusion`
  - `Stringing`
  - `good_print`
    
- Exported the dataset in **YOLOv8 format**.
- Dataset split:
  - Training: 70%
  - Validation: 20%
  - Test: 10%
- Performed data augmentation (flip, brightness, contrast) in Roboflow.

---

### Sample Images from our own Dataset
![Sample of Image used in the dataset](https://github.com/Abhi3886/3D-PrintingFailureDetection/blob/main/training_results/sample_images_dataset/sample_image.png)


---

## 🧠 Model Training

- Model: YOLOv8n (lightweight variant for fast inference)
- Training Command:
  ```bash
  yolo task=detect mode=train model=yolov8n.pt data=data.yaml epochs=50 imgsz=640
  ````

* Evaluation Metrics:

  * mAP\@0.5: \~88%
  * Precision: 89.4%
  * Recall: 93.3%
  * F1 Score: 91.3%

---

## 🚀 Real-Time Deployment with ESP32-CAM

### Architecture

```
[ESP32-CAM] --> captures image -->
[Edge Device] --> runs YOLOv8 inference -->
If failure:
  --> sends signal (Bluetooth/WiFi/UART) to alert/stop print
  ```

### Deployment Steps

1. Converted trained YOLOv8 model to **ONNX → TFLite**.
2. Quantized model using **INT8** for lightweight inference.
3. Edge device (e.g., Raspberry Pi or laptop) runs inference.
4. ESP32-CAM captures real-time images and sends them to the edge device.
5. Fault signals (1 or 0) are sent back to ESP32 to take action (e.g., alert/pause).

---

## 📈 Fault Detection Efficiency

| Metric             | Value   |
| ------------------ | ------- |
| Accuracy           | 92.4%   |
| Precision          | 89.4%   |
| Recall             | 93.3%   |
| F1 Score           | 91.3%   |
| Avg Detection Time | < 2 sec |

---

## 🧠 Skills Used

* Object Detection (YOLOv8)
* Embedded Systems (ESP32-CAM)
* Dataset Annotation (Roboflow)
* Image Processing (OpenCV)
* Edge Deployment (ONNX, TFLite)
* Communication Protocols (UART/Bluetooth/WiFi)
* Evaluation Metrics and Model Optimization

---

## 🔮 Future Improvements

* Store detection history on **Firebase / AWS IoT**.
* Add a **dashboard interface** for monitoring.
* Automate printer control with **relay modules**.

---

## 📁 Folder Structure

```
3D-Printing_Failure_Detection-main/
├── data.yaml
├── images/
│   ├── train/
│   ├── valid/
│   └── test/
├── labels/
│   ├── train/
│   ├── valid/
│   └── test/
├── train.py
├── detect.py
├── weights/
│   └── best.pt
├── esp32-code/
│   └── cam_sender.ino
└── README.md
```

---

