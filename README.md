<div align="center">

# YOLOv7 with ROS1

![Ubuntu 20.04](https://img.shields.io/badge/Ubuntu-20.04-blue?style=flat-square&logo=Ubuntu&logoColor=FFFFFF)
![Ros Noetic](https://img.shields.io/badge/Ros-Noetic-blue?style=flat-square&logo=ROS)
![Python 3.8.10](https://img.shields.io/badge/Python-3.8.10-blue?style=flat-square&logo=Python&logoColor=FFFFFF)

</div>

<font size=2>

> **Note** <br>
> This project if forked from <br>
> [WongKinYiu/yolov7](https://github.com/WongKinYiu/yolov7) <br>
> [alexandrefch/yolov7-ros](https://github.com/alexandrefch/yolov7-ros)

</font>

<font size=2>

## :computer: Test Environment
정밀착륙 알고리즘 수행환경과 동일
- [ros noetic] 
- [gazebo] 
- [px4] 


## :rocket: install

Following ROS packages are required:
- [vision_msgs](http://wiki.ros.org/vision_msgs)
- [geometry_msgs](http://wiki.ros.org/geometry_msgs)
```shell
sudo apt install ros-noetic-vision-msgs
sudo apt install ros-noetic-geometry-msgs
```
clone the repo into your catkin workspace and build the package:
```shell
mkdir -p yolo_ws/src/yolov7-ros
git clone https://github.com/JINtaeung/yolov7_ros ~/yolo_ws/src/yolov7-ros/
cd ~/yolo_ws
catkin_make
echo "source ~/yolo_ws/devel/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
The Python requirements are listed in the `requirements.txt`. You can simply
install them as
```shell
cd src/yolov7-ros/
pip install -r requirements.txt
sudo apt install ros-noetic-opencv*
```
테스트용 가중치 파일 다운로드 (default는 1번으로 작성됨)
1. [yolov7.pt](https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7.pt)   
by [WongKinYiu/yolov7](https://github.com/WongKinYiu/yolov7).   
2. [berkeley_yolov7.pt](https://drive.google.com/drive/folders/1OfC1dQx2db0dmmQA15_WScUptbYcfsZ8?usp=sharing)   
by [berkeley.edu](https://bdd-data.berkeley.edu/)   

- 다운받은 가중치 파일 넣기   
[yolov7.pt]()  or  [berkeley_yolov7.pt]()  -> [yolov7-ros/weights]()

## :clipboard: Usage
Before you launch the node, adjust the parameters in the [launch file](launch/yolov7.launch).   
For example, you need to set the path to your YOLOv7 weights and the image topic to which this node should listen to.   
The launch file also contains a description for each parameter.   

- [launch/yolov7.launch]() for developer
1. param name="weights_path" value="사용할 가중치 파일"
2. param name="classes_path" value="사용할 txt 파일"
3. param name="img_topic" value="받아올 rostopic 경로"
4. param name="device" value="cuda or cpu 환경에 맞게 선택"
```shell
roslaunch yolov7_ros yolov7.launch
```

## :movie_camera: Visualization
[launch/yolov7.launch]() param name="visualize" value="true" 요구
```shell
sudo apt-get install ros-noetic-rqt*
rviz
```
rviz 좌측 하단 add - by topic - /yolov7 - visualization - image
## :satellite: Outpit Rostopic
- [launch/yolov7.launch]() param name="out_topic" value="`example`" 일때 output topic은 /yolov7/`example`
- using the [vision_msgs/Detection2DArray](http://docs.ros.org/en/api/vision_msgs/html/msg/Detection2DArray.html) message type.
- [launch/yolov7.launch]() param name="visualize" value="true" 일때 `/yolov7/example/visualization` 도 rostopic으로 넘어옴.

