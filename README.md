# Installation Guide

https://ardupilot.org/dev/docs/building-setup-linux.html

# Build in ArduPilot

Initial dependencies

	$sudo apt-get install python-dev python-opencv python-wxgtk3.0 python-matplotlib python-pygame python-lxml python-yaml vim git 
	
	$sudo apt install python-pip
	$pip --version (make sure its working)
		
	$sudo pip install --upgrade pip
	$pip --version (make sure its working)
	
	$sudo pip install MAVProxy==1.6.2
		
	$sudo usermod -a -G dialout $USER
	
	$sudo apt-get remove modemmanager
  
All the vehicles share the same code in libraries. Once you compile the code, build directory will be made. 

The tool to build is waf. We need to specify the vehicle type and the hardware target we compile to.
Example check the support hardware using

	ardupilot$ ./waf list_boards


# Flight Modes in ArduPilot

A flight mode is a particular way in which the drone can be controlled. 

For example:	

Stabilize flight mode: Uses exclusively RC Input from the pilot to control the drone
Loiter flight mode: Uses GPS/Barometer and other sensor inputs to automatically hold the drone at the desired place in 3D space without requiring input from the pilot


Primary flight modes: GUIDED, AUTO, RTL, LAND

More info: 

https://ardupilot.org/copter/docs/flight-modes.html

# SITL Simulator (Software In the loop)

What does sim_vehicle.py do?

	Launches our simulated drone with four main 
		Detects what vehicle to build for (Copter, Plane, Rover, etc.). launch sim_vehicle from ArduCopter means that the vehicle type is copter.
	
		$sim_vehicle.py  --map 	--console

	Compiles the necessary source code into an executable.
	Launches the simulated drone by running the SITL executable.
	Launches MAVProxy to communicate with/command the SITL drone.

STABILIZE> mode GUIDED
GUIDED> arm throttle
GUIDED> takeoff 10

# Parameter in ArduPilot
A variable that can be set to different numbers to change some of the drone’s settings/configuration or behavior

Example parameters:	

	-RTL_ALT (cm): The height the drone will fly to when switched into RTL mode.
	-BATT_CAPACITY (mAh): A number that is set to the milli-amp-hours of	the battery that is being used on the drone. This may be used in the calculation of the 	remaining battery life. 	
	-ANGLE_MAX (centi-degrees): The maximum angle the drone will be able	to pitch/roll to. 

Check the parameter

	ArduCopter$ ls mav.parm
	ArduCopter$ wc –l mav.parm
	ArduCopter$ cat mav.parm

Modify parameter

$cat mav.parm | grep RTL_ALT


# Parameter with SITL Drone and MAVProxy

New MAVProxy commands

param show <PARAMETER NAME>
Param set <PARAMETER NAME> <VALUE>

# Ground Control Station

	It is an interface to the done that gives the pilots a way to communicate with the drone.
	This interface can be used to command the drone or simply receive the info updates (GPS health, battery, speed, etc).
	GCS can refer to the hardware setup of the ground control station, or the high levelsoftware that presents all the incoming data with a GUI. 

