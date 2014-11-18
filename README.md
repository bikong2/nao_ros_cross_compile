nao_ros_cross_compile
=====================

A way to cross compile your ROS packages without the NAO OpenVM

This package is still under heavy development. So you are welcome to participate.

The goal is to use the Aldebaran Cross Compile Toochain, available at https://community.aldebaran.com/en/resources/software (you need an account), to cross compile your own ROS packages directly for your NAO. In order to develop this together, we simply took the ROS beginners_tutorials package, especially the talker.cpp, and modified it to let the strings be published to the "chatter"-topic, which the NAOs speech-node is subscribed to. When everything works, we are able to compile the nao_talker.cpp, copy the binary to the NAO and let the NAO say something.


Utilized Versions
-----------------

Currently we are testing with the following setup.

- NAO Robot:
-- Hardware Version 5 (atom cpu)
--  Operating System Naoqi 2.0.19 
--  ROS Version Indigo, compiled from source following this tutorial http://wiki.ros.org/nao/Installation/compileFromVirtualNao
- Development PC (64bit):
-- ROS Version Indigo
-- Aldebaran Cross Compile Toolchain "linux64-atom-pub.zip" (available under https://community.aldebaran.com/en/resources/software)

Setup Steps
-----------

This part will be updated frequently, in order to reflect the development of this package. Currently, the following steps reflect our attempt to make this minimal example work:

1) Download the cross-compile toolchain from aldebaran under https://community.aldebaran.com/en/resources/software . For that you need an aldebaran account, which you probably have anyway, because you probably own a NAO.

2) Unzip the toolchain and place it somewere reachable (e.g. your homefolder)

3) Try to compile the nao_ros_cross_compile package by calling 

.. code-block:: bash

	catkin_make --pkg nao_ros_cross_compile -DCMAKE_TOOLCHAIN_FILE=<path2toolchain>/cross-config.cmake

4) Check whether the resulting binary is compiled for the NAO architecture, by checking its properties (e.g. try "file nao_talker" on commandline).

5) If 4) looks nice, copy it onto your NAO.

6) Start the bring-up script from step 4 under http://wiki.ros.org/nao/Installation/compileFromVirtualNao (you need to be ssh on your NAO)

7) Wait for the bring-up script to run and then start the nao_talker binary.

Maybe, it is easier to test on an instance of the OpenNAO-VM 2.1.0.19 (also available at Aldebaran), but then you won't hear anything... ;-)


Helpfull Resources and Hints
----------------------------

http://www.cmake.org/Wiki/CMake_Cross_Compiling#The_toolchain_file

https://github.com/ros/catkin/issues/484

