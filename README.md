# Real-Time Weed Detection using Deep Learning

An automated weed detection and precision-spraying system that identifies weeds in crop fields in real time, built to reduce herbicide overuse and support sustainable agriculture.

## Overview

Weeds compete with crops for nutrients, water, and light, and traditional full-field herbicide spraying wastes chemicals and harms the environment. This project builds a **real-time weed detection system** using computer vision and deep learning, paired with a robotic sprayer that targets only the areas where weeds are detected — instead of spraying an entire field uniformly.

Two object detection models were trained and compared on the same custom dataset to evaluate which approach performs better for this task:

- **YOLOv7** (You Only Look Once)
- **SSD MobileNet** (Single Shot Detector)

## Dataset

- 1,793 images of weeds and crops, collected via smartphone and handheld digital cameras
- Images labeled and annotated using **Roboflow**
- Split into training, validation, and test sets
- In the field deployment, beans were used as the crop class and grass as the weed class

## Models & Results

| Model | Accuracy |
|---|---|
| SSD MobileNet | 100% |
| YOLOv7 | 94.4% |

In testing, **SSD MobileNet achieved the higher accuracy**, though YOLOv7 also performed strongly. The choice between the two in practice depends on project needs such as computational efficiency and deployment constraints, since both showed advanced detection capability on this dataset.

## Hardware: Real-Time Field Deployment

The trained model was deployed on a **Raspberry Pi**-based robotic unit for real-world testing in an agricultural field:

- **Raspberry Pi** running the trained detection model
- **Pi Camera** capturing live images of the field
- Classification determines whether a captured object is a **weed** or a **crop**
- If a weed is detected, the Pi triggers a **motor-driven micro-sprayer** to apply herbicide precisely to that spot
- A **DC motor** moves the unit forward through the field between detections
- Powered by a **Li-ion battery / portable power bank** for full mobility

This closed-loop system (detect → classify → spray only if needed → move on) minimizes herbicide usage compared to blanket spraying across a field.

## Repository Contents

| File | Description |
|---|---|
| `yolov7_weed_detection.ipynb` | Training and inference pipeline using YOLOv7 |
| `ssd_mobilenet_weed_detection.ipynb` | Training and inference pipeline using SSD MobileNet |
| `projectcontent.docx` | Full project report |
| `ProjectReport_FirstPages.docx` | Report cover/front matter |

## Tech Stack

- **Python**, **Google Colab** (training environment, GPU/TPU access)
- **OpenCV** for image processing
- **Roboflow** for dataset annotation and formatting
- **Raspberry Pi OS (Raspbian)** for on-device deployment
- **PuTTY / VNC Viewer** for remote access to the Raspberry Pi

## Future Enhancements

- Data augmentation (rotations, flips, lighting changes) to grow the training set and improve robustness
- Ensemble modeling — combining YOLOv7 and SSD MobileNet predictions for improved accuracy
- Additional sensors to extend crop-weed identification capabilities

## Conclusion

This project demonstrates a working real-time, in-row weed detection and selective-spraying pipeline that combines a machine vision model with a precision micro-jet sprayer. By spraying only where weeds are actually detected, the system reduces overall herbicide usage — supporting both environmental sustainability and reduced health risks associated with excess herbicide exposure.
