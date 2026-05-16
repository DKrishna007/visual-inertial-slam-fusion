# Architecture

  ## Sensor Setup

  Intel RealSense D435i:
- RGB Camera (640x480, 30fps)
  - Depth Camera (640x480, 30fps)
  - IMU (200Hz)

  3D LiDAR (Velodyne/Ouster):
- Kalibr-calibrated extrinsics to camera

  ## Fusion Pipeline

  ORB-SLAM3 (visual+IMU) -> VIO Odometry
  KISS-ICP (point cloud ICP) -> LiDAR Odometry
  EKF Fusion (7-state: x,y,z, qx,qy,qz,qw) -> /fused_pose

  ## EKF State Covariances
  - VIO measurement noise: position 5mm std, rotation 2mm std
    - LiDAR measurement noise: position 10mm std, rotation 5mm std
      - EKF update rate: 30 Hz
