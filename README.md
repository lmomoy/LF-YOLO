This project is based on [ultralytics/yolov3](https://github.com/ultralytics/yolov3).

LF-YOLO (Lighter and Faster YOLO) is used to detect defect of X-ray weld image. 

<img width="500" src="https://raw.githubusercontent.com/lmomoy/images/main/weld.jpg">  


[comment]: <> (<a align="left" href="https://apps.apple.com/app/id1452689527" target="_blank">)

[comment]: <> (<img width="800" src="https://user-images.githubusercontent.com/26833433/99805965-8f2ca800-2b3d-11eb-8fad-13a96b222a23.jpg"></a>)

[comment]: <> (&nbsp)

[comment]: <> (<a href="https://github.com/ultralytics/yolov3/actions"><img src="https://github.com/ultralytics/yolov3/workflows/CI%20CPU%20testing/badge.svg" alt="CI CPU testing"></a>)

[comment]: <> (This repository represents Ultralytics open-source research into future object detection methods, and incorporates lessons learned and best practices evolved over thousands of hours of training and evolution on anonymized client datasets. **All code and models are under active development, and are subject to modification or deletion without notice.** Use at your own risk.)

[comment]: <> (<p align="left"><img width="800" src="https://user-images.githubusercontent.com/26833433/114424655-a0dc1e00-9bb8-11eb-9a2e-cbe21803f05c.png"></p>)

[comment]: <> (<details>)

[comment]: <> (  <summary>YOLOv5-P5 640 Figure &#40;click to expand&#41;</summary>)
  
[comment]: <> (<p align="left"><img width="800" src="https://user-images.githubusercontent.com/26833433/114313219-f1d70e00-9af5-11eb-9973-52b1f98d321a.png"></p>)

[comment]: <> (</details>)

[comment]: <> (<details>)

[comment]: <> (  <summary>Figure Notes &#40;click to expand&#41;</summary>)
  
[comment]: <> (  * GPU Speed measures end-to-end time per image averaged over 5000 COCO val2017 images using a V100 GPU with batch size 32, and includes image preprocessing, PyTorch FP16 inference, postprocessing and NMS. )

[comment]: <> (  * EfficientDet data from [google/automl]&#40;https://github.com/google/automl&#41; at batch size 8.)

[comment]: <> (  * **Reproduce** by `python test.py --task study --data coco.yaml --iou 0.7 --weights yolov3.pt yolov3-spp.pt yolov3-tiny.pt yolov5l.pt`)

[comment]: <> (</details>)


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

Model |size<br><sup>(pixels) |mAP<sup>val<br>0.5:0.95 |mAP<sup>test<br>0.5:0.95 |mAP<sup>val<br>0.5 |params<br><sup>(M) |FLOPS<br><sup>640 (B)
---   |---                   |---                     |---                      |---                |---                |---
YOLOv3-tiny            |640  |17.6     |17.6     |34.8     |8.8   |13.2
YOLOv3                 |640  |43.3     |43.3     |63.0     |61.9  |156.3
YOLOv3-SPP             |640  |44.3     |44.3     |64.6     |63.0  |157.1
LF-YOLO                |640  |27.8     |27.9     |47.8     |7.4   |17.1




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

