# yolov5_tensorRT

- tensorRT docker pull
```
sudo docker run --gpus all -it nvcr.io/nvidia/tensorrt:23.11-py3
```

- yolov5 install
```
git clone https://github.com/ultralytics/yolov5

cd yolov5

pip install -r requirements.txt
```

- convert pt to tensorRT
```
python export.py --weights yolov5s.pt --include onnx  # pt -> onnx

trtexec --onnx=yolov5s.onnx --saveEngine=yolov5s.engine   # onnx -> tensorRT

```

- inference pytorch model
```
python detect.py --weights yolov5s.pt --source /workspace/yolov5/data/images/

image 1/2 /workspace/yolov5/data/images/bus.jpg: 640x480 4 persons, 1 bus, 65.5ms
image 2/2 /workspace/yolov5/data/images/zidane.jpg: 384x640 2 persons, 2 ties, 55.4ms
Speed: 0.5ms pre-process, 60.5ms inference, 33.2ms NMS per image at shape (1, 3, 640, 640)

```

- inference tensorRT model
```
python detect.py --weights yolov5s.engine --source /workspace/yolov5/data/images/

image 1/2 /workspace/yolov5/data/images/bus.jpg: 640x640 4 persons, 1 bus, 4.5ms
image 2/2 /workspace/yolov5/data/images/zidane.jpg: 640x640 2 persons, 2 ties, 4.5ms
Speed: 7.3ms pre-process, 4.5ms inference, 42.3ms NMS per image at shape (1, 3, 640, 640)

```
**inference:   pytorch 60.5ms  | tensorRT  4.5ms**

![bus](https://github.com/pchxp/yolov5_tensorRT/assets/31230133/4fffa94b-efc6-46c4-a967-9c67daa66441)

## References
```
https://docs.nvidia.com/deeplearning/tensorrt/container-release-notes/index.html
https://github.com/ultralytics/yolov5
```

## Author
```
ChangHyun Park: sigpch@naver.com
```
  

