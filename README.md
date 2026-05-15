# Visual-Inertial SLAM with LiDAR-Camera Fusion

> **Project** | ORB-SLAM3 + Intel RealSense D435i + 3D LiDAR
> > Visual-Inertial Odometry · EKF LiDAR Odometry · Kalibr Calibration · ROS 2
> >
> > ---
> >
> > ## Overview
> >
> > A **hybrid SLAM system** fusing ORB-SLAM3 (visual-inertial odometry) with EKF-based LiDAR odometry, achieving sub-2cm localization accuracy in dynamic indoor environments. Includes a full Kalibr-calibrated multi-sensor pipeline and an open-sourced ROS 2 wrapper.
> >
> > ---
> >
> > ## Key Results
> >
> > | Metric | Value |
> > |---|---|
> > | Localization Accuracy | **< 2 cm** in dynamic indoor environments |
> > | Trajectory Accuracy Improvement | ~30% vs. either modality alone |
> > | Calibration | Kalibr intrinsic/extrinsic calibration |
> > | Open Source | ROS 2 wrapper + calibration pipeline on GitHub |
> >
> > ---
> >
> > ## System Architecture
> >
> > ```
> > Intel RealSense D435i (RGB-D + IMU)
> >        ↓
> > ORB-SLAM3 (Visual-Inertial Odometry)
> >        ↓
> >          ↘
> > EKF Fusion ← 3D LiDAR Odometry (KISS-ICP / LiDAR odom)
> >          ↙
> > Fused Trajectory Estimate (< 2 cm accuracy)
> >        ↓
> > ROS 2 tf2 Pose Broadcasting
> > ```
> >
> > ---
> >
> > ## Features
> >
> > - **ORB-SLAM3** integration with Intel RealSense D435i for visual-inertial odometry
> > - - **Kalibr-calibrated** extrinsic transforms between camera, IMU, and LiDAR coordinate frames
> >   - - **EKF-based fusion** of visual-inertial and LiDAR odometry modalities
> >     - - **< 2 cm localization accuracy** in dynamic indoor environments
> >       - - **~30% trajectory accuracy improvement** over single-modality approaches
> >         - - Open-sourced **ROS 2 wrapper** for ORB-SLAM3 + LiDAR hybrid fusion
> >           - - Published **calibration pipeline** and benchmark results
> >            
> >             - ---
> >
> > ## Tech Stack
> >
> > | Category | Tools / Libraries |
> > |---|---|
> > | SLAM | ORB-SLAM3 |
> > | Sensors | Intel RealSense D435i, 3D LiDAR |
> > | State Estimation | EKF (Extended Kalman Filter) |
> > | Calibration | Kalibr (intrinsic + extrinsic) |
> > | Middleware | ROS 2 (Humble) |
> > | Point Cloud | PCL, KISS-ICP |
> > | Programming | Python, C++ |
> >
> > ---
> >
> > ## Package Structure
> >
> > ```
> > vi_slam_fusion_ws/
> > ├── src/
> > │   ├── orb_slam3_ros2_wrapper/
> > │   │   ├── orb_slam3_ros2/
> > │   │   │   ├── orb_slam3_node.py           # ORB-SLAM3 ROS 2 interface
> > │   │   │   └── pose_publisher.py
> > │   │   ├── config/
> > │   │   │   ├── realsense_d435i.yaml        # Camera + IMU config
> > │   │   │   └── orb_slam3_params.yaml
> > │   │   └── launch/
> > │   │       └── orb_slam3.launch.py
> > │   ├── lidar_odometry/
> > │   │   ├── lidar_odometry/
> > │   │   │   └── kiss_icp_node.py            # LiDAR odometry with KISS-ICP
> > │   │   └── launch/
> > │   │       └── lidar_odom.launch.py
> > │   ├── sensor_fusion/
> > │   │   ├── sensor_fusion/
> > │   │   │   ├── ekf_fusion.py               # EKF for VI + LiDAR fusion
> > │   │   │   └── transform_manager.py
> > │   │   └── config/
> > │   │       └── ekf_params.yaml
> > │   └── calibration/
> > │       ├── kalibr_config/
> > │       │   ├── camera_imu.yaml
> > │       │   └── lidar_camera_extrinsics.yaml
> > │       └── scripts/
> > │           ├── run_kalibr.sh
> > │           └── verify_calibration.py
> > ├── docs/
> > │   ├── calibration_results/
> > │   └── benchmark_results/
> > └── README.md
> > ```
> >
> > ---
> >
> > ## Installation
> >
> > ```bash
> > # Clone the repository
> > git clone https://github.com/DKrishna007/visual-inertial-slam-lidar-camera-fusion.git
> > cd visual-inertial-slam-lidar-camera-fusion
> >
> > # Install ORB-SLAM3 dependencies
> > sudo apt-get install libopencv-dev libeigen3-dev libpangolin-dev
> >
> > # Install ROS 2 dependencies
> > rosdep install --from-paths src --ignore-src -r -y
> > pip install kiss-icp
> >
> > # Build
> > colcon build --symlink-install
> > source install/setup.bash
> > ```
> >
> > ---
> >
> > ## Usage
> >
> > ```bash
> > # Launch full VI-SLAM + LiDAR fusion
> > ros2 launch sensor_fusion full_fusion.launch.py
> >
> > # Run Kalibr calibration
> > cd calibration && bash scripts/run_kalibr.sh
> >
> > # Verify calibration results
> > python3 calibration/scripts/verify_calibration.py
> > ```
> >
> > ---
> >
> > ## Calibration Pipeline
> >
> > The repository includes a complete **Kalibr-based calibration pipeline**:
> > 1. Camera intrinsic calibration (checkerboard)
> > 2. 2. Camera-IMU extrinsic calibration (Kalibr `kalibr_calibrate_imu_camera`)
> >    3. 3. LiDAR-Camera extrinsic calibration (target-based)
> >       4. 4. Temporal synchronization verification
> >         
> >          5. ---
> >         
> >          6. ## Author
> >         
> >          7. **Krishna Digamarthi** | Robotics Engineer | University of Delaware
> > 📧 shivasaikrishna23@gmail.com | [GitHub](https://github.com/DKrishna007)
