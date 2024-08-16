# YOLOv8_CDR

This study utilized YOLOv8 to segment the cup and disc areas in color fundus photography (CFP) captured by NIDEK and EIDON cameras, followed by the calculation of the cup-to-disc ratio for glaucoma detection.

This work utilizes the same dataset as the project available at [https://github.com/biodatlab/si-eye-screening](https://github.com/biodatlab/si-eye-screening)

## Dataset

|       | Total | Glaucoma (NIDEK/EIDON) | Normal (NIDEK/EIDON) |
| :---: | -----: | -----: | -----: |
| Train | 2,732 | | 
| Test  |   342 |               9 (1/8) | 333 (172/161) |
| Val   |   342 | | 

## Training image segmentation

> python src/train_yolov8.py

Training for 100 epochs 

|       | F1-score | Precision | Recall | Precision-Recall |
| :---: | -------- | --------- | ------ | ---------------- |
| Box   | ![](model/BoxF1_curve.png) | ![](model/BoxP_curve.png) | ![](model/BoxR_curve.png) | ![](model/BoxPR_curve.png) |
| Box   | ![](model/MaskF1_curve.png) | ![](model/MaskP_curve.png) | ![](model/MaskR_curve.png) | ![](model/MaskPR_curve.png) |

You can download the pre-trained model  [here](/model)

## Utilizing yolov8 for image segmentation and cup

What the different between this work ando default inferencing?

1. Adjusting 'conf' and 'iou' when inferencing with YOLOv8
    Default inferencing
    > results = model({image_path}, conf=0.25, iou=0.7)

    THis work inferencing 
    > results = model({image_path}, conf=0.001, iou=0.8)

    More detail for paremter adjusting with YOLOv8 [https://docs.ultralytics.com/usage/cfg/#predict-settings](https://docs.ultralytics.com/usage/cfg/#predict-settings)

2. Due to the previous step adjusting the parameter whrn inferenicng then it might be possible to detect more than one cup and dis per image which is not usually
    This work provide simple logic to find the cup and dis 
    First, this work find the largest disc with has cup inside
    Second, this work find the largest cup inside the largest disc


