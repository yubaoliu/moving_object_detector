# Moving objects detection from stereo images

This contains ROS packages to detect moving objects from stereo images.

## Prerequisite

### Hardware

* NVIDIA GPU
* [Xbox 360 Controller](https://www.microsoft.com/accessories/en-ww/products/gaming/xbox-360-controller-for-windows/52a-00004)

  This can be replaced with other controller supported by [joy package](http://wiki.ros.org/joy).
  But maybe change of key assignment is needed.

### Software

* Docker
* Docker Compose (version >= 1.19)
* [NVIDIA Container Toolkit with nvidia-docker2](https://github.com/NVIDIA/nvidia-docker#nvidia-container-toolkit)

  nvidia-docker2 is deprecated now but it is needed to use Docker Compose with NVIDIA GPU.

## Already tested environment

### Hardware

* NVIDIA RTX 2070
* [Xbox 360 Controller](https://www.microsoft.com/accessories/en-ww/products/gaming/xbox-360-controller-for-windows/52a-00004)

### Software

* Ubuntu 19.04
* Docker 19.03
* Docker Compose 1.21
* nvidia-docker2 2.2.1
* nvidia-container-toolkit 1.0.3

## Build

```shell
$ git clone --recursive https://aisl-serv6.aisl.cs.tut.ac.jp:20443/fujimoto/moving_object_detector.git
$ cd moving_object_detector/docker
$ sudo docker-compose build
```

## Test

1. Plug Xbox controller to PC
2. Launch commands at `moving_object_detector/docker` directory:

   ```shell
   $ xhost +local:root
   $ sudo docker-compose up
   ```

   Then Gazebo and rqt windows will be opened.

   Robots in Gazebo is controlled by A + left/right stick.

## contained packages

* disparity_image_proc

  Small library to process stereo_msgs/DisparityImage

* moving_object_detector_launch

  Launch files

* moving_object_msgs

  Message definition represents moving objects

* moving_object_to_marker

  Convert moving_object_msgs to visualization_msgs/MarkerArray to visualize by RViz

* moving_object_tracker

  Track moving objects by Kalman filter

* project_moving_objects_on_image

  Visualize moving_object_msgs with input image

* velocity_estimator

  Generate pointcloud with velocity from camera transform, disparity image and optical flow

* velocity_pc_clusterer

  Clustering pointcloud with velocity

* kkl

  Kalman filter library written by Kenji Koide.
  It is copied from https://aisl-serv6.aisl.cs.tut.ac.jp:20443/koide/grace_person_following.git