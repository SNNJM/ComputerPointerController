# Computer-Pointer-Controller


## Introduction
Computer Pointer Controller is an application which use a gaze detection model to control the mouse pointer of you computer.
This means that the position of mouse pointer correlate with the user's Gaze.

The models that are being used in this projects are based on the OpenVINO toolkit's model.

1.[Gaze Estimation](https://docs.openvinotoolkit.org/latest/_models_intel_gaze_estimation_adas_0002_description_gaze_estimation_adas_0002.html) model is used to estimate the gaze of the user's eyes and then feed the result into `pyautogui` module to change the position of mouse pointer. 

2. [Face Detection](https://docs.openvinotoolkit.org/2018_R5/_docs_Transportation_object_detection_face_pruned_mobilenet_reduced_ssd_shared_weights_caffe_desc_face_detection_adas_0001.html) model to detect faces. Specifically,the network features in this model is a default MobileNet backbone that includes depth-wise convolutions to reduce the amount of computation for the 3x3 convolution block.

3. [Head Pose Estimation](https://docs.openvinotoolkit.org/latest/omz_models_intel_head_pose_estimation_adas_0001_description_head_pose_estimation_adas_0001.html) model is used to estimate position of subject's head.

4. [Landmark Regression](https://docs.openvinotoolkit.org/latest/omz_models_intel_head_pose_estimation_adas_0001_description_head_pose_estimation_adas_0001.html) model is  is a lightweight landmarks regressor and a classic convolutional design: stacked 3x3 convolutions, batch normalizations, PReLU activations, and poolings. Final regression is done by the global depthwise pooling head and FullyConnected layers. The model predicts five facial landmarks: two eyes, nose, and two lip corners.




Below is architecture of the pipeline:

![pipline](https://github.com/SNNJM/ComputerPointerController/blob/master/bin/ComputerPointer.png?raw=true)




### Screenshot:
![show_app](https://github.com/SNNJM/ComputerPointerController/blob/master/bin/result.png?raw=true)

