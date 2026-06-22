+++
title = 'CARLA Autonomous Parking'
date = 2026-06-15
draft = false
+++
<div style="text-align:center;">Authors: Ashik Islam, William Taing</div>

##
<video controls width="100%">
  <source src="/videos/ee470_final_demo_v2.mp4" type="video/mp4">
</video>

## Overview

This project is a simulation-based autonomous parking system developed in CARLA using ROS 2 Jazzy and Nav2. The system allows a simulated vehicle to identify available parking spots, select a valid goal, plan a feasible path, and track that path into the selected parking space.

The project focuses on the path planning and control portions of the autonomous parking pipeline. Since the work was done in simulation, ground-truth vehicle pose and predefined parking spot locations were used to reduce perception and localization complexity while still demonstrating the full parking behavior.

## Resources

<div class="d-flex flex-wrap gap-2 mb-4">
  <a class="btn btn-primary" href="https://github.com/kiashik/carla_autonomous_parking" target="_blank" rel="noopener noreferrer">
    <i class="fab fa-github"></i> GitHub Repo
  </a>
  <a class="btn btn-secondary" href="/docs/CarlaAutonomousParking_TaingIslam.pdf" target="_blank" rel="noopener noreferrer" download>
    <i class="fas fa-file-pdf"></i> Project Report
  </a>
</div>

## How It Works

The system uses a modular ROS 2 architecture built around CARLA, Nav2, and several custom nodes. CARLA provides the simulated parking lot, vehicle model, LiDAR data, and ground-truth vehicle pose. ROS 2 nodes then handle odometry conversion, parking spot occupancy detection, parking spot selection, path planning, path tracking, and CARLA vehicle actuation.

A hard-coded occupancy map represents the parking lot and separates drivable regions from occupied or non-drivable regions. Parking spots are represented as predefined goal poses and 3D polygons. Simulated LiDAR points are transformed into the map frame and checked against each parking spot volume to classify spots as free, occupied, or unknown.

Once parking begins, the system selects the closest free parking spot and sends it as the navigation goal. Nav2’s Smac Hybrid-A* planner generates a feasible path that respects the vehicle’s nonholonomic constraints, while the Regulated Pure Pursuit controller tracks the path. A custom conversion node translates Nav2 velocity commands into CARLA throttle, brake, reverse, and steering commands.

## Results

<video controls width="100%">
  <source src="/videos/long_park_extended_odom.mp4" type="video/mp4">
</video>

The final system successfully demonstrated an autonomous parking pipeline in simulation. The path planner consistently generated feasible paths from valid starting poses, avoided occupied cells, and guided the vehicle toward the selected parking space.

The controller also tracked the planned trajectory well. In the report evaluation, the actual vehicle path closely followed the reference trajectory, showing that the Regulated Pure Pursuit controller and CARLA command conversion were effective for low-speed parking maneuvers.

The parking spot classification system successfully distinguished between free and occupied spaces using simulated LiDAR data. After classification, the system dynamically selected the closest available parking spot as the navigation goal.



## Reflection

This project helped me better understand how autonomous driving systems are built from multiple connected subsystems. Even in simulation, the parking task required odometry, coordinate frame conversion, occupancy mapping, parking spot classification, planning, control, and vehicle command conversion to work together.

One of the main challenges was connecting ROS 2 navigation outputs to CARLA vehicle controls. Nav2 publishes high-level velocity commands, while CARLA expects lower-level vehicle commands such as throttle and steering. Building that conversion made the difference between having a planned path and actually making the simulated vehicle follow it.

If I continued this project, I would add reverse-capable planning, improve the vehicle control model, and replace some of the simulation assumptions with more realistic perception and localization. I would also test the system in more varied parking layouts and starting positions.
