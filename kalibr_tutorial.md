# Kalibr 标定单相机内参
```
cd ~/catkin_ws/src
git clone https://github.com/ethz-asl/kalibr.git
catkin_make
source ~/catkin_ws/devel/setup.bash
```
将所需要用到的文件（.bag,.yaml）移动到~/catkin_ws路径下
```
rosrun kalibr kalibr_calibrate_cameras  --target target.yaml  --models pinhole-radtan  --topics /camera/color/image_raw  --bag new.bag  --bag-freq 10.0
```
freq可以用rostopic hz或者foxglove查看
pinhole-radtan是相机模型-畸变模型，查看官网找其他类型
运行时可能会碰到缺module，使用
```
pip3 install module名 --verbose
```
yaml文件如下格式
```yaml
target_type: 'checkerboard' #gridtype
targetCols: 6               #number of internal chessboard corners
targetRows: 8               #number of internal chessboard corners
rowSpacingMeters: 0.75      #size of one chessboard square [m]
colSpacingMeters: 0.75      #size of one chessboard square [m]

#或者是（根据标定板分类）

target_type: 'aprilgrid' #gridtype
tagCols: 6               #number of apriltags
tagRows: 6               #number of apriltags
tagSize: 0.088           #size of apriltag, edge to edge [m]
tagSpacing: 0.3          #ratio of space between tags to tagSize
                         #example: tagSize=2m, spacing=0.5m --> tagSpacing=0.25[-]
```

具体参考[官方教程](https://github.com/ethz-asl/kalibr/wiki/multiple-camera-calibration)

