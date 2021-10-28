This project is based on [ultralytics/yolov3](https://github.com/ultralytics/yolov3).

LF-YOLO (Lighter and Faster YOLO) is used to detect defect of X-ray weld image. 

<img width="500" src="https://raw.githubusercontent.com/lmomoy/images/main/weld_results.jpg">

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
We test our model on public dataset MS COCO, and it also achieves competitive results.

Model                  |size<br><sup>(pixels)  |mAP<sup>test<br>0.5 |params<br><sup>(M) |FLOPS<br><sup>640 (B)
---                    |---                    |---                 |---                |---               
YOLOv3-tiny            |640                    |34.8                |8.8                |13.2
YOLOv3                 |320                    |51.5                |39.0               |61.9
SSD                    |300                    |41.2                |35.2               |34.3
SSD                    |512                    |46.5                |99.5               |34.3
Faster R-CNN(VGG16)    |shorter size: 800      |43.9                |-                  |278.0
R-FCN(ResNet50)        |shorter size: 800      |49.0                |-                  |133.0
R-FCN(ResNet101)       |shorter size: 800      |52.9                |-                  |206.0
LF-YOLO                |640                    |47.8                |7.4                |17.1




<details>
  <summary>Table Notes (click to expand)</summary>
  
  * AP<sup>test</sup> denotes COCO [test-dev2017](http://cocodataset.org/#upload) server results, all other AP results denote val2017 accuracy.  
  * AP values are for single-model single-scale unless otherwise noted. **Reproduce mAP** by `python test.py --data coco.yaml --img 640 --conf 0.001 --iou 0.65`  
  * Speed<sub>GPU</sub> averaged over 5000 COCO val2017 images using a GCP [n1-standard-16](https://cloud.google.com/compute/docs/machine-types#n1_standard_machine_types) V100 instance, and includes FP16 inference, postprocessing and NMS. **Reproduce speed** by `python test.py --data coco.yaml --img 640 --conf 0.25 --iou 0.45`  
  * All checkpoints are trained to 300 epochs with default settings and hyperparameters (no autoaugmentation). 
</details>


## Requirements

Python 3.8 or later with all [requirements.txt](https://github.com/ultralytics/yolov3/blob/master/requirements.txt) dependencies installed, including `torch>=1.7`. To install run:
```bash
$ pip install -r requirements.txt
```
## Inference
```bash
$ python detect.py --source data/images --weights LF-YOLO.pt --conf 0.25
```

