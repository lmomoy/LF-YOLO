This project is based on [ultralytics/yolov3](https://github.com/ultralytics/yolov3).

LF-YOLO (Lighter and Faster YOLO) is used to detect defect of X-ray weld image. The related paper is available [here](http://arxiv.org/abs/2110.15045).

<img width="500" src="https://raw.githubusercontent.com/lmomoy/images/main/weld_result.jpg">

## Download

```download
$ git clone https://github.com/lmomoy/LF-YOLO
```
## Train
We provide multiple versions of LF-YOLO with different depths. 

```train
$ python train.py --data coco.yaml --cfg LF-YOLO.yaml      --weights '' --batch-size 1
                                         LF-YOLO-1.25.yaml                           1
                                         LF-YOLO-0.75.yaml                           1
                                         LF-YOLO-0.5.yaml                            1
```

## Results
We test LF-YOLO on our weld defect image dataset. Other methods are trained and tested based on [MMDetection](https://github.com/open-mmlab/mmdetection).

Model                      |size (pixels)          |mAP50<sup>test<br>  |params (M)         |FLOPS (B)
---                        |---                    |---                 |---                |---               
Cascasde-RCNN (ResNet50)   |(1333, 800)            |90.0                |68.9               |243.2
Cascasde-RCNN (ResNet101)  |(1333, 800)            |90.7                |87.9               |323.1
Faster-RCNN (ResNet50)     |(1333, 800)            |90.1                |41.1               |215.4
Faster-RCNN (ResNet101)    |(1333, 800)            |92.2                |60.1               |295.3
Dynamic-RCNN (ResNet50)    |(1333, 800)            |90.3                |41.1               |215.4
RetinaNet (ResNet50)       |(1333, 800)            |80.0                |36.2               |205.2
VFNet (ResNet50)           |(1333, 800)            |87.0                |32.5               |197.8
VFNet (ResNet101)          |(1333, 800)            |87.2                |51.5               |277.7
Reppoints (ResNet101)      |(1333, 800)            |82.7                |36.6               |199.0
SSD300 (VGGNet)            |300                    |88.1                |24.0               |30.6
YOLOv3 (Darknet52)         |416                    |91.0                |62.0               |33.1
SSD (MobileNet v2)         |300                    |82.3                |3.1                |0.7
YOLOv3 (MobileNet v2)      |416                    |90.2                |3.7                |1.6
LF-YOLO-0.5                |640                    |90.7                |1.8                |1.1
LF-YOLO                    |640                    |92.9                |7.4                |17.1


We test our model on public dataset MS COCO, and it also achieves competitive results.

Model                  |size (pixels)          |mAP50<sup>test<br>  |params (M)         |FLOPS (B)
---                    |---                    |---                 |---                |---               
YOLOv3-tiny            |640                    |34.8                |8.8                |13.2
YOLOv3                 |320                    |51.5                |39.0               |61.9
SSD                    |300                    |41.2                |35.2               |34.3
SSD                    |512                    |46.5                |99.5               |34.3
Faster R-CNN (VGG16)   |shorter size: 800      |43.9                |-                  |278.0
R-FCN (ResNet50)       |shorter size: 800      |49.0                |-                  |133.0
R-FCN (ResNet101)      |shorter size: 800      |52.9                |-                  |206.0
LF-YOLO                |640                    |47.8                |7.4                |17.1




[comment]: <> (<details>)

[comment]: <> (  <summary>Table Notes &#40;click to expand&#41;</summary>)
  
[comment]: <> (  * AP<sup>test</sup> denotes COCO [test-dev2017]&#40;http://cocodataset.org/#upload&#41; server results, all other AP results denote val2017 accuracy.  )

[comment]: <> (  * AP values are for single-model single-scale unless otherwise noted. **Reproduce mAP** by `python test.py --data coco.yaml --img 640 --conf 0.001 --iou 0.65`  )

[comment]: <> (  * Speed<sub>GPU</sub> averaged over 5000 COCO val2017 images using a GCP [n1-standard-16]&#40;https://cloud.google.com/compute/docs/machine-types#n1_standard_machine_types&#41; V100 instance, and includes FP16 inference, postprocessing and NMS. **Reproduce speed** by `python test.py --data coco.yaml --img 640 --conf 0.25 --iou 0.45`  )

[comment]: <> (  * All checkpoints are trained to 300 epochs with default settings and hyperparameters &#40;no autoaugmentation&#41;. )

[comment]: <> (</details>)


## Requirements

Python 3.8 or later with all [requirements.txt](https://github.com/ultralytics/yolov3/blob/master/requirements.txt) dependencies installed, including `torch>=1.7`. To install run:
```bash
$ pip install -r requirements.txt
```
## Inference
```bash
$ python detect.py --source data/images --weights LF-YOLO.pt --conf 0.25
```

