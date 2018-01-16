# Apollo

[![Build Status](https://travis-ci.org/ApolloAuto/apollo.svg?branch=master)](https://travis-ci.org/ApolloAuto/apollo)

```
We choose to go to the moon in this decade and do the other things,
not because they are easy, but because they are hard.
-- John F. Kennedy, 1962
```

Welcome to the Apollo GitHub.

[Apollo](http://apollo.auto) is an open autonomous driving platform. It is a high performance flexible architecture which supports fully autonomous driving capabilities.
For business contact, please visit http://apollo.auto

**Apollo Team now proudly presents to you the latest [version 2.0](https://github.com/ApolloAuto/apollo/releases/tag/v2.0.0).**

## Installation

We strongly recommend building Apollo in our pre-specified Docker environment.
See the following instructions on how to set up the docker environment and build from source.
The steps are:
 - Run a machine that runs linux (tested on Ubuntu 16.04 with and without an nVidia GPU)
 - Create a docker environment
 - Build Apollo from source
 - Bootstrap start Apollo
 - Download the demonstration loop and run it
 - Start a browser session and see the Dreamview user interface

More instructions are below

### The docker environment can be set by the commands below.

Running a docker container from a linux system is done with this sequence. At the end, the `dev_into.sh` 
script will get you into the container

```
bash docker/scripts/install_docker.sh
# logout and login back in the system to make sure to run docker command without sudo
docker ps  # to verify docker works without sudo
# in case you forgot to logout and login back, do so, remove ~/.docker/config.json
# and check again with `docker ps`
bash docker/scripts/dev_start.sh
bash docker/scripts/dev_into.sh

```

### To build from source
Now you will need to build from the source. If you want to run the entire system, make sure you have an 
nVidia GPU and that you have installed the Linux nVidia drivers. 

```
# To get a list of build commands
./apollo.sh
# To make sure you start clean
./apollo.sh clean
# This will build the full system and requires that you have an nVidia GPU with nVidia drivers loaded
bash apollo.sh build
```

If you do not have an nVidia GPU, the system will run but with the CUDA-based perception and other modules. You must 
specify either `dbg` for debug mode or `opt` for optimized code

```
./apollo.sh build_no_perception dbg
```

If you make modifications to the Dreamview frontend, then you must run `./apollo.sh build_fe`  before you run the 
full build.


## Run Apollo
Follow the steps below to launch Apollo:

### Start Apollo from MacOS

Install Docker for Mac using the Edge release. This is easily down with `brew
cask install docker-edge` or you can run `install-docker.sh` and it will do this
for you and install Brew if needed.

Make sure the shares are added in Docker for Mac icon. This is a little
complicated as not all files are visible so you have to:

- Start Docker for Mac
- Click on Preferences/File Sharing and click the `+` icon
- Add any random directory 
- Click on that and then manually enter `/etc/localtime`

There is a current bug in Docker for Mac
https://github.com/docker/for-mac/issues/2396 which prevents this from working
because localtime is not handled properly


### Start Apollo

Running Apollo will start the ROS core and then startup a web user interface called Dreamview, this is handled by 
the bootstrap script, so from within the docker container, you should run:

```
# start module monitor
bash scripts/bootstrap.sh
```

### Access Dreamview
Access Dreamview by opening your favorite browser, e.g. Chrome, go to http://localhost:8888 and you should see this screen
However, there will be nothing running in the system.


![Access Dreamview](docs/demo_guide/images/apollo_bootstrap_screen.png)


### Replay demo rosbag

To see if the system works, use the demo 'bag' which feeds the system.

```
# get rosbag note that the command download is required
bash ./docs/demo_guide/rosbag_helper.sh download

# You can now replay this demo "bag" in a loop with the '-l' flag
rosbag play -l ./docs/demo_guide/demo_2.0.bag
```

Dreamview should show a running vehicle now. (The following image might be different due to changes in frontend.)

![Dreamview with Trajectory](docs/demo_guide/images/dv_trajectory.png)

## Documents

Apollo documents can be found under the [docs](https://github.com/ApolloAuto/apollo/blob/master/docs/) repository.
   * [quickstart](https://github.com/ApolloAuto/apollo/blob/master/docs/quickstart/): the quickstart tutorial.
   * [demo_guide](https://github.com/ApolloAuto/apollo/blob/master/docs/demo_guide/): the guide for demonstration.
   * [![Apollo Offline Demo](https://img.youtube.com/vi/Q4BawiLWl8c/0.jpg)](https://www.youtube.com/watch?v=Q4BawiLWl8c)
   * [how to contribute code](https://github.com/ApolloAuto/apollo/blob/master/CONTRIBUTING.md): the guide for contributing code to Apollo.
   * [howto](https://github.com/ApolloAuto/apollo/blob/master/docs/howto/): tutorials on how to build, run and modify codes.
   * [specs](https://github.com/ApolloAuto/apollo/blob/master/docs/specs/): Specification documents of Apollo.
   * [Doxygen APIs](https://apolloauto.github.io/doxygen/apollo/): Apollo Doxygen pages

## Ask Questions

You are welcome to submit questions and bug reports as [Github Issues](https://github.com/ApolloAuto/apollo/issues).

## Copyright and License

Apollo is provided under the [Apache-2.0 license](LICENSE).

## Disclaimer
Please refer the Disclaimer of Apollo in [Apollo official website](http://apollo.auto/docs/disclaimer.html).
