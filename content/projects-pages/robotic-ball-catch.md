+++
title = 'Autonomous Catch with a Robotic Arm'
date = 2026-06-12
draft = false
+++
<div style="text-align:center;">Authors: Ashik Islam, Kayla Go-Oco, Raegan Gritzmacher</div>

## Demo

<video controls width="100%">
  <source src="/videos/ball_interception_demo_with_trajectory_OMY.mp4" type="video/mp4">
</video>

## Overview

This project is a vision-guided robotic interception system designed to detect, track, and attempt to catch a tossed tennis ball with an OpenMANIPULATOR-Y, a 6 DoF robotic arm. The system combines YOLO-based object detection, an Intel RealSense D455 RGB-D camera, projectile-motion prediction, OMPL motion planning, and MoveIt Servo real-time control.

The goal was to build a complete perception-to-control pipeline where the robot could observe a tossed tennis ball, estimate its 3D position, predict where it would cross a fixed catch plane, and move the arm toward that predicted interception point.

## Resources
<div class="d-flex flex-wrap gap-2 mb-4">
  <a class="btn btn-primary" href="https://github.com/kiashik/throw_and_catch/tree/main" target="_blank" rel="noopener noreferrer">
    <i class="fab fa-github"></i> GitHub Repo
  </a>
  <a class="btn btn-secondary" href="/docs/Vision-Guided%20Motion%20Planning%20for%20Autonomous%20Catch%20with%20a%20Robotic.pdf" target="_blank" rel="noopener noreferrer" download>
    <i class="fas fa-file-pdf"></i> Project Report
  </a>
</div>

## How It Works

The RealSense D455 camera provides RGB and depth data. A custom-trained YOLO model detects the tennis ball in the RGB image, while the aligned depth image is used to estimate the ball’s 3D position. The position is transformed from the camera frame into the robot base frame using an eye-to-hand calibration process.

A Kalman-filter-based projectile prediction node estimates the ball’s trajectory and predicts where it will intersect a fixed catch plane. OMPL is used to move the robot into a ready position before the toss, while MoveIt Servo streams real-time Cartesian velocity commands to guide the arm toward the predicted catch point.

## Results

The system successfully integrated computer vision, trajectory prediction, and real-time robotic control. The vision pipeline was able to estimate the tennis ball position accurately enough for interception planning, and the robot consistently moved toward physically reachable predicted catch points.

The final system did not achieve a fully successful catch during testing. The main limitation was not the predicted catch point itself, but the combined latency and speed limitations of the OpenMANIPULATOR-Y arm. In end-to-end testing, the robotic arm reached the predicted interception point about 150 ms after the tennis ball crossed the catch plane.

## Reflection

This project taught me how difficult real-time robotic systems become when perception, prediction, and hardware motion all have to work together under tight timing constraints. Each subsystem worked individually, but the full system exposed bottlenecks that were not obvious during isolated testing.

One major takeaway was that motion planning and real-time control serve different purposes. OMPL was useful for safe, collision-free pre-positioning, but it was not fast enough for continuously changing dynamic targets. MoveIt Servo was a better fit for reactive control, but the physical robot still had speed and workspace limitations.

If I continued this project, I would focus on reducing the control latency and testing a faster robotic platform. I would also explore lower-level control methods or direct inverse-kinematics-based commands to reduce the delay between predicted catch point generation and robot motion.


## 2026 Cal Poly Project Expo
![OMY team at the Expo](/images/OMY/omy_team_at_expo.jpg)
*From left: Raegan Gritzmacher, Ashik Islam, Kayla Go-Oco*