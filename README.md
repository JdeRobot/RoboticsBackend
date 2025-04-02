# RoboticsBackend

This repo purpose is to have all the necessary requirements to compile and push new docker images to Dockerhub.  Esentially, it holds the Dockerfile scripts to make the respective app images and a github action that joins everything into a Docker container image that is pushed into Dockerhub. The images that can be generated are the following:

* RoboticsBackend (RB for short): For use in Unibotics and as a base to all others.
* RoboticsAcademy (RA for short): For use in RoboticsAcademy, formerly known as RADI.
* RoboticsDatabase: Database for use in RoboticsAcademy, contains universes db, excercises db and RA django_auth db.
* Bt-Studio (BT for short): For use in Bt Studio, formerly known as BTDI.
* Bt-Studio Database: Database for use in Bt Studio, contains universes db and Bt Studio django_auth db.

## Github Action _Generate Robotics Backend_

This github action is prepared to package every image created by the Dockerfiles into a RoboticsBackend tagged docker image. This github action needs some inputs:

* Docker Image tag: The id of the tag of the RoboticsBackend image to pull from Dockerhub. It is usually a number followed by points __(ex: 4.6.3)__ unless it's a beta image, which should be tagged as __beta__
* Upload as latest: The id of the tag of the RoboticsBackend image is also set to latest to pull from Dockerhub. Check only if the image is desired to be used as the latest reference.
* Branch of RoboticsInfrastructure: The branch of RoboticsInfrastructure repo that will be packaged. It's default value is _humble-devel_.
* Branch of RoboticsApplicationManager: The branch of RoboticsApplicationManager repo that will be packaged. It's default value is _humble-devel_.
* ROS Distro: ROS version that will be used on the simulations. From now on RA and Unibotics-webserver only use __ROS 2 (humble)__.

  ### How does this github action works?

  1. All the necessary setups for github action is prepared.
  2. The github action logs in the Dockerhub webpage using the __github actions secrets__.
  3. Then builds a base image with all the deppendencies used on robotics applications.
  4. Finally starts compiling and packaging every repo to create the RB image.
  5. New RB image is pushed into [Dockerhub](https://hub.docker.com/r/jderobot/robotics-backend).

## Adding a new application to _Robotics Backend_ docker image.

At the time this documentation is being written, RA and BT are the only robotics application used on Unibotics-webserver. Nonetheless, there's future plans to add new apps. The only requirements to do so is to add the necesarry dockerfiles to the _scripts_ directory and add the builiding of that new app into the Github Action.
