ROS drivers for Optris thermal imagers

This bag is to run optris thermal camera with ros.

This code copy and change a little from https://github.com/evocortex/optris_drivers.

When I use the ros driver http://wiki.ros.org/optris_drivers to run the thermal camera.

I meet some troubles and bug.
-----------------------------------------------------------------------------------------
Error:

A.
[optris/optris_imager_node-1] process has died [pid 15942, exit code -6, cmd /home/pal/deployed_ws/lib/optris_drivers/optris_imager_node __name:=optris_imager_node __log:=/home/pal/.ros/log/dd7bea30-cfda-11e9-ac1c-d43b04def328/optris-optris_imager_node-1.log]. log file: /home/pal/.ros/log/dd7bea30-cfda-11e9-ac1c-d43b04def328/optris-optris_imager_node-1*.log


then it just stop there.

B.
others alos meet like :
terminate called after throwing an instance of 'std::runtime_error'
  what():  Duration is out of dual 32-bit range
 
then it stop there.
  
It just happen on my two computers and two systems(windows and ubuntu).
But at last I fix it and run it successfully.
I follow the issue :https://github.com/evocortex/optris_drivers/issues/30
Then copy two files to fix it.

Follow is the totally steps from begining.

1.you need to download the SDK from http://ftp.evocortex.com/
I use  libirimager-8.6.0-amd64.deb  

2.unpack the deb 

3.you need to follow the step on document of oprits SDK(Linux install):
http://documentation.evocortex.com/libirimager2/html/Installation.html#sec_basic
And stop at Determining serial number.

4.git clone or download my src file and catkin_make it 

5.ros launch it

---------------------------------------------------------------------------------------
How can I fix my problem:

I just use the debug code from the doc:http://documentation.evocortex.com/libirimager2/html/index.html#sec_trouble
and add the 

evo::IRLogger::setVerbosity(evo::IRLoggerVerbosityLevel::IRLOG_DEBUG, evo::IRLoggerVerbosityLevel::IRLOG_OFF);

in optris_imager_node.cpp 

--------------------------------------------------------------------------------------
maybe u need to use 
set (CMAKE_CXX_STANDARD 11)
in cmake list to change your c++ to 11
maybe u need to use 
include_directories(
  ${catkin_INCLUDE_DIRS}
)
in cmake list to find some include file.
