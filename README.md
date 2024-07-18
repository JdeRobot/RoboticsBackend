# RoboticsBackend

This repo purpose is to have all the necessary requirements to compile and push new RoboticsBackend (RB for short) images to Dockerhub.  Esentially, it holds the Dockerfile scripts to make the respective app images and a github action that joins everything into a Docker container image that is pushed into Dockerhub.

## Github Action _Generate Robotics Backend_

This github action is prepared to package every image created by the Dockerfiles into a RoboticsBackend tagged docker image. This github action needs some inputs:

  * Docker Image tag: The id of the tag of the RoboticsBackend image to pull from Dockerhub. It is usually a number followed by points __(ex: 4.63)__ unless it's a beta image, which should be tagged as 
  __beta__ 
  * Branch of Robotics Academy: The branch of RoboticsAcademy repo that will be packaged. It's default value is _humble-devel_. Note that If you're creating a beta image of RB, you must specify the branch of      RA which has the desired changes.
  * Branch of RoboticsInfrastructure: The branch of RoboticsInfrastructure repo that will be packaged. It's default value is _humble-devel_.
  * Branch of RoboticsApplicationManager: The branch of RoboticsApplicationManager repo that will be packaged. It's default value is _humble-devel_.
  * ROS Distro: ROS version that will be used on the simulations. From now on RA and Unibotics-webserver only use __ROS 2 (humble)__.

  ### How does this github action works?

  1. All the necessary setups for github action is prepared.
  2. The github action logs in the Dockerhub webpage using the __github actions secrets__.
  3. Then builds a base image with all the deppendencies used on robotics applications.
  4. Finally starts compiling and packaging every repo to create the RB image.
  5. New RB image is pushed.

## RA Dockerfiles
