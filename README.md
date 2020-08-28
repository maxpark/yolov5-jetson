# yolov5

The Pytorch implementation is [ultralytics/yolov5](https://github.com/ultralytics/yolov5).

Currently, we support yolov5 v1.0(yolov5s only), v2.0 and v3.0.

- For yolov5 v3.0, please visit [yolov5 release v3.0](https://github.com/ultralytics/yolov5/releases/tag/v3.0), and use the latest commit of this repo.
- For yolov5 v2.0, please visit [yolov5 release v2.0](https://github.com/ultralytics/yolov5/releases/tag/v2.0), and checkout commit ['7cd092d'](https://github.com/wang-xinyu/tensorrtx/commit/7cd092d38289123442157cf7defab78e816f4440) of this repo.
- For yolov5 v1.0, please visit [yolov5 release v1.0](https://github.com/ultralytics/yolov5/releases/tag/v1.0), and checkout commit ['0504551'](https://github.com/wang-xinyu/tensorrtx/commit/0504551c0b7d0bac5f998eda349810ba410715de) of this repo.

## Config

- Choose the model s/m/l/x by `NET` macro in yolov5.cpp
- Input shape defined in yololayer.h
- Number of classes defined in yololayer.h
- FP16/FP32 can be selected by the macro in yolov5.cpp
- GPU id can be selected by the macro in yolov5.cpp
- NMS thresh in yolov5.cpp
- BBox confidence thresh in yolov5.cpp
- Batch size in yolov5.cpp

## How to Run, yolov5s as example

```
1. generate yolov5s.wts from pytorch with yolov5s.pt

git clone https://github.com/wang-xinyu/tensorrtx.git
git clone https://github.com/ultralytics/yolov5.git
// download its weights 'yolov5s.pt'
// copy tensorrtx/yolov5/gen_wts.py into ultralytics/yolov5
// ensure the file name is yolov5s.pt and yolov5s.wts in gen_wts.py
// go to ultralytics/yolov5
python gen_wts.py
// a file 'yolov5s.wts' will be generated.

2. build tensorrtx/yolov5 and run

// put yolov5s.wts into tensorrtx/yolov5
// go to tensorrtx/yolov5
// ensure the macro NET in yolov5.cpp is s
mkdir build
cd build
cmake ..
make
sudo ./yolov5 -s             // serialize model to plan file i.e. 'yolov5s.engine'
sudo ./yolov5 -d  ../samples // deserialize plan file and run inference, the images in samples will be processed.

3. check the images generated, as follows. _zidane.jpg and _bus.jpg

4. optional, load and run the tensorrt model in python

// install python-tensorrt, pycuda, etc.
// ensure the yolov5s.engine and libmyplugins.so have been built
python yolov5_trt.py
```

<p align="center">
<img src="https://user-images.githubusercontent.com/15235574/78247927-4d9fac00-751e-11ea-8b1b-704a0aeb3fcf.jpg">
</p>

<p align="center">
<img src="https://user-images.githubusercontent.com/15235574/78247970-60b27c00-751e-11ea-88df-41473fed4823.jpg">
</p>

## More Information

See the readme in [home page.](https://github.com/wang-xinyu/tensorrtx)

