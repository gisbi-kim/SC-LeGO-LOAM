# SC-LeGO-LOAM
LiDAR SLAM: Scan Context + Lego-LOAM

<p align="center"><img src="results/mulran_merged.png" width=600></p>

<p align="center"><img src="results/pangyo_merged.png" width=600></p>

## Examples
- <a href="https://youtu.be/MtQ8-PiBK3E?t=194"> Video 1: DCC (MulRan dataset)</a>
- <a href="https://youtu.be/p-NsVs8GATA?t=436"> Video 2: Riverside (MulRan dataset) </a>

## Scan Context integration
- For implementation details, see the `mapOptmization.cpp`; all other files are same as the original LeGO-LOAM.

## How to use 
- Place the directory `SC-LeGO-LOAM` under user catkin work space 
- For example, 
```
cd ~/catkin_ws/src
git clone https://github.com/irapkaist/SC-LeGO-LOAM.git
cd ..
catkin_make
source devel/setup.bash
roslaunch lego_loam run.launch
```

## MulRan dataset 
- If you want to reproduce the results as the above video, you can download the <a href="https://sites.google.com/view/mulran-pr/home"> MulRan dataset </a> and use the <a href="https://sites.google.com/view/mulran-pr/tool"> ROS topic publishing tool </a>.   






## Dependencies
- All dependencies are same as LeGO-LOAM (i.e., ROS, PCL, and GTSAM).
