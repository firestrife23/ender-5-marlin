# Ender-5-Marlin
Custom configuration.h and configuration_adv.h for Ender 5 and based on Marlin's latest bugfix-1.1.x.

## Guide

it's a drop in replacement files for Marlin's firmware https://github.com/MarlinFirmware/Marlin/archive/bugfix-1.1.x.zip

## Features and Fixes

* Set machine name to Ender-5
* Set Homing to rear right corner
* Invert Z Stepper Direction
* Disabled Bootscreen (reclaim memory space)
* Disabled Status Screen Image (this remove "Ender-5" from the top left corner, for much cleaner status screen)
* Enabled S-Curve Acceleration & Junction Deviation @ 0.8 for 0.4mm nozzle (You'll need to change the value if you're different nozzle)
* Linear Advance Supported. To make the use of Linear Advance, you will need to do the calibration, then add M900 K## to Slicer's Custom Starting G-Code.
* Disabled Speaker
* Disabled ARC Support (It's for laser etching, reclaim memory space)
* Boosted Buffer for improved print quality with Octopi, almost as good as printing from SD Card
* Enabled Unknown Z No Raise (No more horrible grinding sound at Max Position.)
* Set print bed to 220x220 with the volume of 300 (you can change it to 235x235 however, keep in mind if you have custom hotend cooling or Auto Leveling sensors it'll crash into frame unless you reduced it to 220x220 or less)
* Enabled Mesh Bed Leveling with 5x5 points (I'm old school, you can disable if you don't want it)
  1. #define MESH_BED_LEVELING
  2. #define GRID_MAX_POINTS_X 5
* Enabled Restore Leveling Data after G28 (Very useful for mesh or auto leveling)
* Enabled LCD Bed Leveling Menu

Special Note about LCD stuffs below, I disabled a lot of those to reclaim memory space for above features and I do most of the configuration through octopi and turned my LCD into more of Progress Report with minimal basic stuff. Now that you know why some of the menu options are missing.

* Enabled Slim LCD Menus (reclaim memory space)
* Disabled LCD Info Menu (reclaim memory space)
* Disabled Status Message Scrolling (reclaim memory space)
* Disabled Long Filename Scrolling (reclaim memory space)
* Enabled Set LCD progress manually (useful for Octoprint's plugin)

## Future Plan

Create different set of configuration.h for: 
- [x] Mesh Leveling
- [ ] EZABL Leveling
- [ ] BLTouch Leveling
