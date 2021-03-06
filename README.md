# Vehicle Monitoring System
This project is written in python and the vehicle detection is based on Tensorflow_Object_Detection_API
[**Demo Link V1.0**](https://www.bilibili.com/video/av48336782/)
<p align="center">
  <img src="https://github.com/yy0yaolinjun1/ScreenShot/blob/master/TrafficMonitoring/main_ui.png">
</p>

the processing speed of the video is about 8FPS(Detection model:mobilenet_v2. CPU:I700hq).If you pursue a higher processing speed,you could use YOLO_V3 instead.[**YOLO_V3 configuration tutorial Reference(Chinese)**](https://blog.csdn.net/KID_yuan/article/details/88380269)

the speed of YOLO_V3 is about 20 to 35FPS(the speed based on the number of objects in video) (Detection model: YOLO_V3. GPU:GTX1070. CPU:I700hq)
<p align="center">
  <img src="https://github.com/yy0yaolinjun1/ScreenShot/blob/master/TrafficMonitoring/Fps_YoloV3.JPG">
</p>


## v2.0)Code Refactoring and Optimization:
		speed detection,converse running detection,running red line detection,and vehicle leave detection all share the same detection area
		Avoiding repetitive detection
##	   New Capabilities:
		14)vehicle counting(through comparing the distance between the coordinates of bounding box and the detection area to determine which lane is the vehicle in)
<p align="center">
	<img src="https://github.com/yy0yaolinjun1/ScreenShot/blob/master/TrafficMonitoring/vehicle_counting.JPG">
</p>		

##v1.1) New Capability:
	    13)Double line crossing detection:(notice: since detecting the vehicle through the width of detected bounding box and because of the perspective projection,
the width of the vehicle bounding box that first appears in the video is large,which may lead to error detection and therefore,modifying the interest area is needed)
<p align="center">
  <img src="https://github.com/yy0yaolinjun1/ScreenShot/blob/master/TrafficMonitoring/double_line_crossing.JPG">
</p>

## v1.0) General Capabilities of This Project:

1) Real-time traffic monitoring(using ssd_mobilenet_v2 Model,more detection model see here https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/detection_model_zoo.md)

2) Interest Area:only the vehicles in the area will be detected by Tensorflow

3) Speed detection:(The speed of the vehicle on each lane is calculated separately)

4) speeding vehicle capture:When the vehicle speed is over the speed limit, the vehicle will be captured and the relevant info and image will be stored.

5) Recognition of traffic light color:the current color of the traffic light will be recognized
(This part of the code reference from @ONLINE{cr,author="Ahmet Özlü",title="Color Recognition",year="2018",url="https://github.com/ahmetozlu/color_recognition")

6) Cross-line detection and capture

7) Vehicle leave detection:

8) ROI values setting and dynamically previewing the modified effect

9) Saving and loading ROI values

10) viewing the violation records from the database

11) Avoiding repetitive detection

12)Converse running detection:
<p align="center">
  <img src="https://github.com/yy0yaolinjun1/ScreenShot/blob/master/TrafficMonitoring/converse_crossing.jpg">
</p>



## Notice:
	1)The variable with a value of 0 in the UI means it is no longer used in the v2.0 version.
	2)The relevant code for vehicle detection is in vehicle_detection_api.py while the following variables in vehicle_detection_api.py should be modified according to the actual situation.
		2.1)SPEED_DIRECTION:determine the default positive direction(default value:-1 from bottom to top;while 1: from top to bottom)	
		2.2)TRAFFIC_JAM_INTERVAL_REFRESH_COUNT:to calculate the vehicle count more accurately(default value:25,which means thatevery time the vehicle is detected in the detection area, the corresponding counter will be added 1,once  the counter reach 25,the value that used to record the frame number when the vehicle is detected in the current lane will be set to the current video frame number,and the counter will be reset.)
		2.3)LINE_CROSSING_DETECTION_INTERVAL_IN_EACH_LANE:if the (current frame number) - (the frame number that the vehicle is last detectd in the detection area)>DETECTION_INTERVAL,the vehicle will be considered to have left the corresponding detection area and therefore,the vehicle could be detected again in the area.
		2.4)WIDTH_OF_TURNING_VEHICLE:it is used to detect the vehicle that crossing the double solid line if (right-left)>WIDTH_OF_TURNING_VEHICLE
	3)the width of the detection area should not be too wide
	
## User Guide
## Installation
install tensorflow_cpu
installation guide:(https://tensorflow-object-detection-api-tutorial.readthedocs.io/en/latest)
## Operating Guide
1->choose video file->2setting the roi values and store them to configuration file/choosing existing roi configuration file->3running video detection-4viewing records

ps:1)pip install missing_package_name
   2)please press 'q' to quit the preview before running video detection(one of the bugs that needed to be fixed...)
   3)For Chinese Users:文件路径不能带有中文，否则通过CV2写入图片会失败OVO//
   
## future work(if time allows ~OvO~):
								  1)optmizing converse running detection
								  2)UI modification
							      3)using YOLO_V3