# Blood-Cells-Identifcation-with-Yolov4-Faster-R-CNN


Step-1:
	clone github repository using: 
git clone https://github.com/AlexeyAB/darknet
Step-2:
Open MakeFile present in darknet repository in any editor of your choice and edit it:
1.	Set GPU = 1 and CUDNN = 1 --if you have a GPU otherwise 0.
2.	Set OPENCV = 1 
GPU=1
CUDNN=1
CUDNN_HALF=0
OPENCV=1
AVX=0
OPENMP=0
LIBSO=0
ZED_CAMERA=0
ZED_CAMERA_v2_8=0<img width="471" alt="yv41" src="https://user-images.githubusercontent.com/64285157/110252259-58866c00-7f39-11eb-8609-c8435ca84523.PNG">


Save that file. 
Step-3:
	Open a terminal in darknet directory and type commad make, to start compiling darknet.
Step-4:
	In directory darknet/cfg find the cfg file named as yolov4-custom.cfg. copy and rename it with any name of your choice i.e. yolo-obj.cfg 
Now open this file in any editor and edit the following:
1.	Set batch (in line 6) according to requirement i.e batch=64
2.	Set subdivision (in line 7) according to your requirement i.e. subdivisions=16
3.	Set width and height (in line 8, 9) of your image to be resized. i.e. width=416, height=416.
4.	Set max_batches (in line 20) according to (classes*2000) i.e. if no. of classes is 3 then max_batches=6000
5.	Set steps (in line 22) as 80%, 90% of your max_batches i.e. steps = 4800, 5200
6.	Set no. of classes in each YOLO layer (in line 967, 1055, 1143) according to your problem.
7.	Set no. of filters according to (classes + 5)*3 in each Convolutional Layer Right Before Each YOLO (in Line 963, 1051, 1139) i.e. if no. of classes is 3 then filters = 24
Save the cfg file.
Step-4:
	In directory darknet/data create a file named i.e. obj.names and place all the classes names in it (each in single line).
Note: order of Classes matters During Testing so write them in same order classes are in annotation files.
Step-5:
	Create a text file train.txt and write all the paths to each training image in it.
	Create another text file test.txt and write all the paths to each testing images in it.
Step-6:
	Create a file obj.data in the directory darknet/data and write the following:
classes = 3 #No. of Classes
train  = data/train.txt  #path to train.txt
valid  = data/test.txt	  #path to test.txt
names = data/obj.names	  #path to obj.names
backup = backup/	  #path to backup folder in darkent directory

Step-7:
	Download pre-trained weights for your YOLO Version. https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.conv.137

Step-8:
	Now write the following command in terminal (opened in darkent directory) 
./darknet train <path-to-obj.data> <path-to-yolo-obj.cfg> <path-to-pre-trained-weights>
And hit enter your training will start.
	
