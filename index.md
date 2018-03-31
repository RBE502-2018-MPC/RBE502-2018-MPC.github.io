This is just some preliminary notes for now for how to setup everything.

# Setting Up the RC_Node
* Install the correct USB lib.  (something like libusb-0.1 or something.  Not 1.0.  TODO)
* Follow the installation instructions on: https://www.pjrc.com/teensy/td_download.html
* Make sure to install the udev rules for teensy hid: https://www.pjrc.com/teensy/49-teensy.rules
* `sudo cp 49-teensy.rules /etc/udev/rules.d/`
* go to `<workspace>/src`
* `https://github.com/RBE502-2018-MPC/rc_node`
* go to `<workspace>`
* `catkin_make` 

# Setting Up Vicon Code
* `sudo apt install ros-kinetic-vrpn`
* go to `<workspace>/src`
* `git clone https://github.com/ros-drivers/vrpn_client_ros`
* Comment out line 333 of `vrpn_client_ros.cpp`, and compile
* go to `<workspace>`
* `catkin_make`
* you can optionally make a new launch file that sets the windows computer as the default server ip address.

# Using a Logitech Gamepad to Control the Car
* `pip install inputs`
* go to workspace
* `git clone https://github.com/RBE502-2018-MPC/logitech_controller`

# Setting up the Vicon System for testing
* Set a static IP for you computer, and connect using ethernet through the switch connected to the vicon system.
* I set my static IP as: 192.168.10.111
* Maybe set yours to something like 192.168.10.112 or something around there, but it shouldn't really matter unless two of us are connected
* Turn on the Vicon system.  There is a switch in the back facing towards the motion capture area.  If the vicon system is on, there should be some leds on each of the cameras that light up purple.
* Start the Vicon Tracker software on the Windows computer and make sure that the cameras are connected (all the cameras should have blue LEDs).  If you click on one of the cameras in the software, the LED on the respective camera should change color to puruple
* Make sure the rc_car object is selected in the objects tab, and deselect everything else.  You should see the car show up in the environment as orange points and lines
* `roslaunch vrpn_client_ros sample.launch server:=192.168.10.1`
* This should then be publishing to topics like
* `/vrpn_client_node/rc_car/accel`
* `/vrpn_client_node/rc_car/pose`
* `/vrpn_client_node/rc_car/twist`
* Note that the accel topic won't be publishing anything useful, because it needs to be disabled to prevent the system from crashing.
