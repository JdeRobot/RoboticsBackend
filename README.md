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

## Robotics Academy

### Github Action _Release Robotics Academy_

This action should be used when releasing a new RoboticsAcademy version. You should not use this action when creating a beta or testing image. For that purpose use the ones below.

This github action is prepared to call the actions _Generate Robotics Academy_ and _Generate Robotics Academy Database_. This github action needs some inputs:

* Docker Image tag: The id of the tag of the RoboticsAcademy image to pull from Dockerhub. It must be the version number __(ex: 5.4.1)__.
* Upload as latest: The id of the tag of the RoboticsAcademy image is also set to latest to pull from Dockerhub. Uncheck only if testing the action.
* Branch of Robotics Academy: The branch of RoboticsAcademy repo that will be packaged. It must be _humble-devel_.
* Branch of RoboticsInfrastructure: The branch of RoboticsInfrastructure repo that will be packaged. It's default value is _humble-devel_.
* Branch of RoboticsInfrastructure for Universes Database: The branch of RoboticsInfrastructure repo where the universes database is stored. It's default value is _database_.
* Branch of RoboticsApplicationManager: The branch of RoboticsApplicationManager repo that will be packaged. It's default value is _humble-devel_.
* ROS Distro: ROS version that will be used on the simulations. From now on RA and Unibotics-webserver only use __ROS 2 (humble)__.

### Github Action _Generate Robotics Academy_

This github action is prepared to package every image created by the Dockerfiles into a RoboticsAcademy tagged docker image. This github action needs some inputs:

* Docker Image tag: The id of the tag of the RoboticsAcademy image to pull from Dockerhub. It is usually a the version number __(ex: 5.4.1)__ unless it's a beta image, which should be tagged as __beta__
* Upload as latest: The id of the tag of the RoboticsAcademy image is also set to latest to pull from Dockerhub. Check only if the image is desired to be used as the latest reference.
* Branch of Robotics Academy: The branch of RoboticsAcademy repo that will be packaged. It's default value is _humble-devel_. Note that If you're creating a beta image of RA, you must specify the branch of RA which has the desired changes.
* Branch of RoboticsInfrastructure: The branch of RoboticsInfrastructure repo that will be packaged. It's default value is _humble-devel_.
* Branch of RoboticsApplicationManager: The branch of RoboticsApplicationManager repo that will be packaged. It's default value is _humble-devel_.
* ROS Distro: ROS version that will be used on the simulations. From now on RA and Unibotics-webserver only use __ROS 2 (humble)__.

  #### How does this github action works?

  1. All the necessary setups for github action is prepared.
  2. The github action logs in the Dockerhub webpage using the __github actions secrets__.
  3. Then builds a base image with all the deppendencies used on robotics applications.
  4. Finally starts compiling and packaging every repo to create the RA image.
  5. New RA image is pushed into [Dockerhub](https://hub.docker.com/r/jderobot/robotics-academy).

### Github Action _Generate Robotics Academy Database_

This github action is prepared to package every image created by the Dockerfiles into a Robotics Academy Database tagged docker image. This github action needs some inputs:

* Docker Image tag: The id of the tag of the Robotics Academy Database image to pull from Dockerhub. It is usually a the version number __(ex: 5.4.1)__ unless it's a beta image, which should be tagged as __beta__
* Upload as latest: The id of the tag of the Robotics Academy Database image is also set to latest to pull from Dockerhub. Check only if the image is desired to be used as the latest reference.
* Branch of RoboticsAcademy: The branch of RoboticsAcademy repo that will be used to retrieve the exercise database and the django_auth databse. It's default value is _humble-devel_. Note that If you're creating a beta image of RA, you must specify the branch of RoboticsAcademy which has the desired changes.
* Branch of RoboticsInfrastructure: The branch of RoboticsInfrastructure repo where the universe database is stored. It's default value is _database_.

  #### How does this github action works?

  1. All the necessary setups for github action is prepared.
  2. The github action logs in the Dockerhub webpage using the __github actions secrets__.
  3. Then builds a base image with all the deppendencies used on robotics applications.
  4. Finally starts compiling and packaging every repo to create the Robotics Academy Database image.
  5. New Bt Studio image is pushed into [Dockerhub](https://hub.docker.com/r/jderobot/robotics-database).

## Bt Studio

### Github Action _Release Bt Studio_

This action should be used when releasing a new Bt Studio version. You should not use this action when creating a beta or testing image. For that purpose use the ones below.

This github action is prepared to call the actions _Generate Bt Studio_ and _Generate Bt Studio Database_. This github action needs some inputs:

* Docker Image tag: The id of the tag of the Bt Studio image to pull from Dockerhub. It must be the version number __(ex: 5.4.1)__.
* Upload as latest: The id of the tag of the Bt Studio image is also set to latest to pull from Dockerhub. Uncheck only if testing the action.
* Branch of Bt Studio: The branch of Bt Studio repo that will be packaged. It must be _main_.
* Branch of RoboticsInfrastructure: The branch of RoboticsInfrastructure repo that will be packaged. It's default value is _humble-devel_.
* Branch of RoboticsInfrastructure for Universes Database: The branch of RoboticsInfrastructure repo where the universes database is stored. It's default value is _database_.
* Branch of RoboticsApplicationManager: The branch of RoboticsApplicationManager repo that will be packaged. It's default value is _humble-devel_.
* ROS Distro: ROS version that will be used on the simulations. From now on Bt Studio and Unibotics-webserver only use __ROS 2 (humble)__.

### Github Action _Generate Bt Studio_

This github action is prepared to package every image created by the Dockerfiles into a Bt Studio tagged docker image. This github action needs some inputs:

* Docker Image tag: The id of the tag of the Bt Studio image to pull from Dockerhub. It is usually a the version number __(ex: 0.7.1)__ unless it's a beta image, which should be tagged as __beta__
* Upload as latest: The id of the tag of the Bt Studio image is also set to latest to pull from Dockerhub. Check only if the image is desired to be used as the latest reference.
* Branch of Bt Studio: The branch of Bt Studio repo that will be packaged. It's default value is _main_. Note that If you're creating a beta image of BT, you must specify the branch of Bt Studio which has the desired changes.
* Branch of RoboticsInfrastructure: The branch of RoboticsInfrastructure repo that will be packaged. It's default value is _humble-devel_.
* Branch of RoboticsApplicationManager: The branch of RoboticsApplicationManager repo that will be packaged. It's default value is _humble-devel_.
* ROS Distro: ROS version that will be used on the simulations. From now on Bt Studio and Unibotics-webserver only use __ROS 2 (humble)__.

  #### How does this github action works?

  1. All the necessary setups for github action is prepared.
  2. The github action logs in the Dockerhub webpage using the __github actions secrets__.
  3. Then builds a base image with all the deppendencies used on robotics applications.
  4. Finally starts compiling and packaging every repo to create the Bt Studio image.
  5. New Bt Studio image is pushed into [Dockerhub](https://hub.docker.com/r/jderobot/bt-studio).

### Github Action _Generate Bt Studio Database_

This github action is prepared to package every image created by the Dockerfiles into a Bt Studio Database tagged docker image. This github action needs some inputs:

* Docker Image tag: The id of the tag of the Bt Studio Database image to pull from Dockerhub. It is usually a the version number __(ex: 0.7.1)__ unless it's a beta image, which should be tagged as __beta__
* Upload as latest: The id of the tag of the Bt Studio Database image is also set to latest to pull from Dockerhub. Check only if the image is desired to be used as the latest reference.
* Branch of Bt Studio: The branch of Bt Studio repo that will be used to retrieve the django_auth databse. It's default value is _main_. Note that If you're creating a beta image of BT, you must specify the branch of Bt Studio which has the desired changes.
* Branch of RoboticsInfrastructure: The branch of RoboticsInfrastructure repo where the universe database is stored. It's default value is _database_.

  #### How does this github action works?

  1. All the necessary setups for github action is prepared.
  2. The github action logs in the Dockerhub webpage using the __github actions secrets__.
  3. Then builds a base image with all the deppendencies used on robotics applications.
  4. Finally starts compiling and packaging every repo to create the Bt Studio Database image.
  5. New Bt Studio image is pushed into [Dockerhub](https://hub.docker.com/r/jderobot/bt-studio-database).

## RA Dockerfiles

These files are located on the _scripts_ directory and end with _RA. These Dockerfiles are used by the github action to start creating the RA components that will be avaliable on a RB container such as GPU acceleration, OS, ROS dependencies and such.

__NOTE:__ These dockerfiles comes from the RADI scripts available on RoboticsAcademy. If those files are updated, then these should be too.

## BT Dockerfiles

These files are located on the _scripts_ directory and end with _BT. These Dockerfiles are used by the github action to start creating the BT components that will be avaliable on a RB container such as GPU acceleration, OS, ROS dependencies and such.

__NOTE:__ These dockerfiles comes from the BTDI scripts available on Bt Studio. If those files are updated, then these should be too.

## Adding a new application to _Robotics Backend_ docker image.

At the time this documentation is being written, RA and BT are the only robotics application used on Unibotics-webserver. Nonetheless, there's future plans to add new apps. The only requirements to do so is to add the necesarry dockerfiles to the _scripts_ directory and add the builiding of that new app into the Github Action.
