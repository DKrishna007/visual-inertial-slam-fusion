# Trajectory Accuracy Comparison

## ATE (Absolute Trajectory Error)

| Method | ATE RMSE (m) | ATE Mean (m) | Max Error (m) |
|--------|-------------|-------------|---------------|
| ORB-SLAM3 (VIO only) | 0.0312 | 0.0271 | 0.0891 |
| LiDAR odometry only | 0.0284 | 0.0241 | 0.0763 |
| **VIO + LiDAR EKF Fusion** | **0.0187** | **0.0162** | **0.0498** |

Fusion improvement over VIO: ~40%
Fusion improvement over LiDAR: ~34%
Best case localization: <2cm in stable indoor environments

## RPE (1m segments)

| Method | RPE Trans (m) | RPE Rot (deg) |
|--------|--------------|---------------|
| VIO only | 0.0089 | 0.412 |
| LiDAR only | 0.0071 | 0.387 |
| **Fused** | **0.0052** | **0.241** |

## Test Environment
- Dynamic indoor lab with moving people
- ~200m total trajectory
- Lighting variations: standard to dimmed to bright
- Ground truth: Vicon motion capture system
