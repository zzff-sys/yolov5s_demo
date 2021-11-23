# yolov5s_demo
RP4 ,NCS2 and Openvino
(PC)openvino version: **w_openvino_toolkit_p_2021.4.752_online.exe**

​										**CMake 3.21.1**

​										**visual Studio Code 2017**

(rp4)openvino version:**l_openvino_toolkit_runtime_raspbian_p_2020.3.355**

### My deployment steps are:

##### (1) yolov5s.pt to yolov5s.onnx

Using the command line:   （success）

```c
python models/export.py --weights yolov5s.pt --img 640 --batch 1
```

![image-20211123162401575](C:\Users\xiaozhou\AppData\Roaming\Typora\typora-user-images\image-20211123162401575.png)

##### （2）yolov5s.onnx to IR(.bin and .xml)

Using the command line:   （success）

```c
python mo_onnx.py --input_model yolov5s.onnx --model_name best -s 255 --output Conv_250,Conv_304,Conv_196 --input_shape [1,3,640,640] --data_type=FP16
```

![image-20211123162708643](C:\Users\xiaozhou\AppData\Roaming\Typora\typora-user-images\image-20211123162708643.png)

##### (3) .bin and .xml  to RP4

Detect a photo of a human face:

```c
./armv7l/Release/object_detection_sample_ssd -m best.xml -d MYRIAD -i /home/pi/Downloads/face/6.jpeg
```

![image-20211123162935566](C:\Users\xiaozhou\AppData\Roaming\Typora\typora-user-images\image-20211123162935566.png)

