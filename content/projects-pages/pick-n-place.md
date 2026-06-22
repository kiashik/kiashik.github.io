+++
title = 'Autonomous Pick-and-Place: Color-Based Sorting with 4-DOF Manipulator'
date = 2024-12-03
draft = false
+++
<div style="text-align:center;">Authors: Ashik Islam, Dmitri Dobrynin</div>


## Demos
### Pick-and-Place
<video controls width="100%">
  <source src="/images/pick-n-place/pick-n-place_demo-eye-in-hand.mp4" type="video/mp4">
</video>

### Visual Servoing 

<video controls width="100%">
  <source src="/images/pick-n-place/Position-Based_Visual_Servo_control_Demo.mp4" type="video/mp4">
</video>

## Overview

This project demonstrates robotic pick-and-place manipulation using visual feedback and a vision-guided control pipeline. The system focuses on detecting a target object, estimating its pose, and commanding the robot to move toward the object for manipulation.

The project includes both a pick-and-place demonstration and a position-based visual servoing demonstration. Together, these show how perception and control can be combined to move a robotic manipulator from high-level object detection toward physical task execution.

## Resources

<div class="d-flex flex-wrap gap-2 mb-4">
  <a class="btn btn-secondary" href="/docs/pick-n-place-demo_Islam-Dobrynin.pdf" target="_blank" rel="noopener noreferrer" download>
    <i class="fas fa-file-pdf"></i> Project Report
  </a>
</div>

## How It Works

The system uses a camera-based perception pipeline to observe the robot workspace and provide visual feedback for manipulation. In the pick-and-place demo, the robot uses the camera view to locate the target and execute a manipulation sequence. In the visual servoing demo, the robot continuously adjusts its motion based on the perceived target position.

The project highlights the connection between computer vision, coordinate frames, robot motion, and feedback control. Instead of relying only on fixed scripted poses, the robot uses visual information to guide its motion and improve task execution.

## Results

The demos show the robot performing camera-guided motion for manipulation tasks. The pick-and-place demo demonstrates the full manipulation sequence, while the visual servoing demo shows the robot responding to visual feedback as it moves toward a target.

The project helped validate the use of visual feedback for robotic manipulation and provided practical experience with perception-driven robot control.

## Reflection

This project helped me understand how important calibration, coordinate frames, and feedback timing are in robotic manipulation. Even a simple pick-and-place task becomes more complex when the robot needs to use camera data instead of only moving to predefined positions.

The biggest takeaway was that visual servoing connects perception directly to control. Small errors in image processing, pose estimation, or frame transformation can affect the final robot motion, so the full pipeline has to be tested as an integrated system.

If I continued this project, I would improve the object detection and pose-estimation pipeline, add more robust failure handling. Pose estimation is currently done using Perspective-n-Point (PnP). The Intel RealSense D35 is a RGBD camera, so I wonder if pose estimation using depth would be more accurate.