# Computer-Pointer-Controller


## Introduction
Computer Pointer Controller is an application which use a gaze detection model to control the mouse pointer of you computer.
This means that the position of mouse pointer correlate with the user's Gaze.

The models that are being used in this projects are based on the OpenVINO toolkit's model.

1.[Gaze Estimation](https://docs.openvinotoolkit.org/latest/_models_intel_gaze_estimation_adas_0002_description_gaze_estimation_adas_0002.html) model is used to estimate the gaze of the user's eyes and then feed the result into `pyautogui` module to change the position of mouse pointer. 

2.[Face Detection](https://docs.openvinotoolkit.org/2018_R5/_docs_Transportation_object_detection_face_pruned_mobilenet_reduced_ssd_shared_weights_caffe_desc_face_detection_adas_0001.html) model to detect faces. Specifically,the network features in this model is a default MobileNet backbone that includes depth-wise convolutions to reduce the amount of computation for the 3x3 convolution block.

3.[Head Pose Estimation](https://docs.openvinotoolkit.org/latest/omz_models_intel_head_pose_estimation_adas_0001_description_head_pose_estimation_adas_0001.html) model is used to estimate position of subject's head.

4.[Landmark Regression](https://docs.openvinotoolkit.org/latest/omz_models_intel_head_pose_estimation_adas_0001_description_head_pose_estimation_adas_0001.html) model is  is a lightweight landmarks regressor and a classic convolutional design: stacked 3x3 convolutions, batch normalizations, PReLU activations, and poolings. Final regression is done by the global depthwise pooling head and FullyConnected layers. The model predicts five facial landmarks: two eyes, nose, and two lip corners.




Below is architecture of the pipeline:

![pipline](https://github.com/SNNJM/ComputerPointerController/blob/master/bin/ComputerPointer.png?raw=true)




### Screenshot:
![show_app](https://github.com/SNNJM/ComputerPointerController/blob/master/bin/result.png?raw=true)




## Project Set Up and Installation
_______________
**1. A must have!** 
- [Install Intel® Distribution of OpenVINO™ toolkit for Windows* 10](https://docs.openvinotoolkit.org/latest/openvino_docs_install_guides_installing_openvino_windows.html#model_optimizer_configuration_steps) or you can choose install in Linux system.
- The `requirments.txt` in project directory needs to be installed. Using command: 
    - `pip3 install -r requirements.txt`



**2. Environment setup**

Initialize openVINO environment (command in cmd)

Go to openvinopath/bin/setupvars.bat for windows 10
    
This need to be initialized each time a new terminal/cmd is opened


**3.Download the required model**
- Download the required models:
    - [Face Detection](https://docs.openvinotoolkit.org/latest/_models_intel_face_detection_adas_binary_0001_description_face_detection_adas_binary_0001.html)
    - [Head Pose Estimation](https://docs.openvinotoolkit.org/latest/_models_intel_head_pose_estimation_adas_0001_description_head_pose_estimation_adas_0001.html)
    - [Facial Landmarks Detection](https://docs.openvinotoolkit.org/latest/_models_intel_landmarks_regression_retail_0009_description_landmarks_regression_retail_0009.html)
    - [Gaze Estimation Model](https://docs.openvinotoolkit.org/latest/_models_intel_gaze_estimation_adas_0002_description_gaze_estimation_adas_0002.html)
    
    OR
    
You can use the model_downloader in the OpenVINO toolkit path: /deployment_tools/tools/model_downloader

Adding -o path will help ypu specify to a targeted folder.

 
 - cd to project directory and follow command below to download the models.
 ```sh
    list out all of the available models: python downloader.pt --print_all
     
    python "C:\Program Files (x86)\IntelSWTools\openvino\deployment_tools\open_model_zoo\tools\downloader\downloader.py" --name face-detection-adas-binary-0001
    
    python "C:\Program Files (x86)\IntelSWTools\openvino\deployment_tools\open_model_zoo\tools\downloader\downloader.py" --name head-pose-estimation-adas-0001
    
    python "C:\Program Files (x86)\IntelSWTools\openvino\deployment_tools\open_model_zoo\tools\downloader\downloader.py" --name landmarks-regression-retail-0009
    
    python "C:\Program Files (x86)\IntelSWTools\openvino\deployment_tools\open_model_zoo\tools\downloader\downloader.py" --name gaze-estimation-adas-0002
```
  
 Below ois the source structure of project:
``` 
C:\Users\A221LPEN\Desktop\udacity\A5\Computer-Pointer-Controller-main>tree /a /f
Folder PATH listing for volume OS
Volume serial number is 6EF5-D9EA
C:.
|   .Instructions.md.swp
|   README.md
|   requirements.txt
|
+---bin
|       .gitkeep
|       ComputerPointer.png
|       demo.mp4
|       result.png
|
+---models
|   +---face-detection-adas-0001
|   |   +---FP16
|   |   |       face-detection-adas-0001.bin
|   |   |       face-detection-adas-0001.xml
|   |   |
|   |   +---FP16-INT8
|   |   |       face-detection-adas-0001.bin
|   |   |       face-detection-adas-0001.xml
|   |   |
|   |   \---FP32
|   |           face-detection-adas-0001.bin
|   |           face-detection-adas-0001.xml
|   |
|   +---face-reidentification-retail-0095
|   |   +---FP16
|   |   |       face-reidentification-retail-0095.bin
|   |   |       face-reidentification-retail-0095.xml
|   |   |
|   |   +---FP16-INT8
|   |   |       face-reidentification-retail-0095.bin
|   |   |       face-reidentification-retail-0095.xml
|   |   |
|   |   \---FP32
|   |           face-reidentification-retail-0095.bin
|   |           face-reidentification-retail-0095.xml
|   |
|   +---gaze-estimation-adas-0002
|   |   +---FP16
|   |   |       gaze-estimation-adas-0002.bin
|   |   |       gaze-estimation-adas-0002.xml
|   |   |
|   |   +---FP16-INT8
|   |   |       gaze-estimation-adas-0002.bin
|   |   |       gaze-estimation-adas-0002.xml
|   |   |
|   |   \---FP32
|   |           gaze-estimation-adas-0002.bin
|   |           gaze-estimation-adas-0002.xml
|   |
|   +---head-pose-estimation-adas-0001
|   |   +---FP16
|   |   |       head-pose-estimation-adas-0001.bin
|   |   |       head-pose-estimation-adas-0001.xml
|   |   |
|   |   +---FP16-INT8
|   |   |       head-pose-estimation-adas-0001.bin
|   |   |       head-pose-estimation-adas-0001.xml
|   |   |
|   |   \---FP32
|   |           head-pose-estimation-adas-0001.bin
|   |           head-pose-estimation-adas-0001.xml
|   |
|   \---landmarks-regression-retail-0009
|       +---FP16
|       |       landmarks-regression-retail-0009.bin
|       |       landmarks-regression-retail-0009.xml
|       |
|       +---FP16-INT8
|       |       landmarks-regression-retail-0009.bin
|       |       landmarks-regression-retail-0009.xml
|       |
|       \---FP32
|               landmarks-regression-retail-0009.bin
|               landmarks-regression-retail-0009.xml
|
\---src
    |   face_detection.py
    |   facial_landmarks_detection.py
    |   gaze_estimation.py
    |   head_pose_estimation.py
    |   input_feeder.py
    |   main.py
    |   model.py
    |   mouse_controller.py
    |   Project_log.log
    |
    \---__pycache__
            face_detection.cpython-36.pyc
            facial_landmarks_detection.cpython-36.pyc
            gaze_estimation.cpython-36.pyc
            head_pose_estimation.cpython-36.pyc
            input_feeder.cpython-36.pyc
            mouse_controller.cpython-36.pyc
```


