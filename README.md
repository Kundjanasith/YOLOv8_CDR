# YOLOv8_CDR

This work applied YOLOv8 to segmemt cup and disc area from color fundus phtography (CFP) from NIDEK and EIDON camera and then calculate cup-to-disc ratio for detecting glaucoma.

This work utilize same dataset from this project [https://github.com/biodatlab/si-eye-screening](https://github.com/biodatlab/si-eye-screening)

## Dataset

|       | Total | Glaucoma (NIDEK/EIDON) | Normal (NIDEK/EIDON) |
| :---: | -----: | -----: | -----: |
| Train | 2,732 | | 
| Test  |   342 |               9 (1/8) | 333 (172/161) |
| Val   |   342 | | 

## Training image segmentation

> python train_yolov8.py

After training for 100 epochs 

Download the pre-trained model [here](/model)

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


