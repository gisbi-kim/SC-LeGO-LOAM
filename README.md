# SC-LeGO-LOAM
- LiDAR SLAM: Scan Context (18 IROS) + Lego-LOAM (18 IROS)
- This repository is an example use-case of <a href="https://github.com/irapkaist/scancontext/tree/master/cpp"> Scan Context C++ </a>, the LiDAR place recognition method, for LiDAR SLAM applications.  
- Just include `Scancontext.h`. For details see the file `mapOptmization.cpp`. 
- This example is integrated with LOAM, but our simple module (i.e., `Scancontext.h`) can be easily integrated with any other key-frame-based odometry (e.g., wheel odometry or ICP-based odometry).


## Features 
- Light-weight: a single header and cpp file named "Scancontext.h" and "Scancontext.cpp"
    - Our module has KDtree and we used <a href="https://github.com/jlblancoc/nanoflann"> nanoflann </a>. nanoflann is an also single-header-program and that file is in our directory.
- Easy to use: A user just remembers and uses only two API functions; `makeAndSaveScancontextAndKeys` and `detectLoopClosureID`.
- Fast: The loop detector runs at 10-15Hz (for 20 x 60 size, 10 candidates)


## Examples
- <a href="https://youtu.be/MtQ8-PiBK3E?t=194"> Video 1: DCC (MulRan dataset)</a>
- <a href="https://youtu.be/p-NsVs8GATA?t=436"> Video 2: Riverside (MulRan dataset) </a>

<p align="center"><img src="results/mulran_merged.png" width=700></p>
<p align="center"><img src="results/pangyo_merged.png" width=700></p>


## Scan Context integration

- For implementation details, see the `mapOptmization.cpp`; all other files are same as the original LeGO-LOAM.
- Some detail comments
    - We use non-conservative threshold for Scan Context's nearest distance, so expect to maximise true-positive loop factors, while the number of false-positive increases.
    - To prevent the wrong map correction, we used Cauchy (but DCS can be used) kernel for loop factor. See `mapOptmization.cpp` for details. (the original LeGO-LOAM used non-robust kernel). We found that Cauchy is emprically enough.
    - We use both two-type of loop factor additions (i.e., radius search (RS)-based as already implemented in the original LeGO-LOAM and Scan context (SC)-based global revisit detection). See `mapOptmization.cpp` for details. SC is good for correcting large drifts and RS is good for fine-stitching.
    - Originally, Scan Context supports reverse-loop closure (i.e., revisit a place in a reversed direction) and examples in <a href="https://github.com/kissb2/PyICP-SLAM"> here (py-icp slam) </a>. Our Scancontext.cpp module contains this feature. However, we did not use this for closing a loop in this repository because we found PCL's ICP with non-eye initial is brittle. 

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
