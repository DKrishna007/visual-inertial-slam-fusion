# Proof Materials Guide

## Best Proof Screenshot
Trajectory overlay showing:
- Blue: ground truth (Vicon mocap)
- Red: VIO only (ORB-SLAM3)
- Green: Fused (VIO + LiDAR EKF)

## Required Visual Proofs
| Proof | Description |
|-------|-------------|
| Trajectory plots | 3 overlaid trajectories (GT, VIO, Fused) |
| Kalibr calibration | Target board image + reprojection error |
| ORB feature tracking | Frame with ORB keypoints overlaid |
| Sensor setup photo | D435i + LiDAR mounted on robot/rig |
| Error plot | ATE over time for all 3 methods |

## Key Numbers
- <2cm localization accuracy (fused)
- 0.42px Kalibr reprojection error
- ~40% ATE improvement over single modality
- 7-state EKF (position + quaternion)
