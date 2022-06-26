# Traffic Sign Detection using YoloV4

Dataset link : https://www.kaggle.com/code/valentynsichkar/traffic-signs-images-with-bounding-boxes-in-yolo/notebook

# Changes to do in yolov4 architecture as per custom dataset

#### Open darknet folder -> cfg folder -> yolov4-custom.cfg
Note: Delete everything from this "cfg" folder but don't delete yolov4-custom.cfg.
This step is optional. We are just deleting all these files to simply the process. Those files are extra, not required for executing yolov4

#### Open yolov4-custom.cfg file and do the changes as per your dataset Training
#### change batch=1 from batch=64
#### change subdivisions=1 from subdivisions=16
#### width=608 #416
#### height=608 #416

Next is max_batches.This parameter is very very important.The thing to remember here is that minimum batch value would be 6000 ( if you have 1 class or 2 classes or 3 classes.)
In our case we have 4 classes. So max_batches would be 4*2000 = 8000 i.e 8000 would be the max_batches.

Steps are also important. There are 2 steps:Ist step should be 90% of the max_batch value. And 2nd step would be the 80% of the max_batch
steps are steps=7200,6400 (90% of 8000 and 80% of 8000)
We have 3 YOLO layers for 3 different scales.
Showing you a demo below. Just see the [Yolo] layer. Above [YOLO] layer, we have [convolutional] layer. Change the number of
filters as per your output classes as per this calculation (classes+5)3 = (4+5)3 = 27
"""

#### [convolutional]
size=1 stride=1 pad=1 filters=255 # change this to 27 activation=linear

#### [yolo]
In the same way search for other 2 [Yolo] layers and then the [Convolutional] layer which is above the [yolo] layer. Just change the number of filters
Also change the number of classes as per your dataset.

Next Change is open Darknet folder -> data folder

Delete everything from this folder except labels folder. Don't delete Labels Folder

Under this data folder paste your dataset folder (images with their text files)

Now create 2 files data.obj and data.names in the darknet -> data .
data.obj have details like how many classes you have, path of your training and test file. Also mentioned the path where we want to store the trained model weights.
