# Ender-5-Marlin-1.1.x

### UPDATE: 2.8.2020
I'm no longer maintaining this repository because I've completely rebuild My ender 5 with BigTreeTech's SKR 1.3 with TMC2208 drivers. Marlin's latest firmware now included pre-made configuration for Ender 5 so you should use that as a starting point instead of mine. 


## Guide

it's a drop in replacement files for Marlin's firmware https://github.com/MarlinFirmware/Marlin/archive/bugfix-1.1.x.zip

**It's recommended to run M503 & M500 before and after flashing firmware**

## Features and Fixes

* Set machine name to Ender-5
* Set Homing to rear right corner
* Invert Z Stepper Direction
* Disabled Bootscreen (reclaim memory space)
* Disabled Status Screen Image (this remove "Ender-5" from the top left corner, for much cleaner status screen)
* Enabled S-Curve Acceleration & Junction Deviation @ 0.08 for 0.04mm nozzle (You'll need to change the value if you're using different nozzle)
* Linear Advance Supported. To make the use of Linear Advance, you will need to do the calibration, then add M900 K## to Slicer's Custom Starting G-Code.
* Disabled Speaker
* Disabled ARC Support (It's for laser etching, reclaim memory space)
* Boosted Buffer for improved print quality with Octopi, almost as good as printing from SD Card
* Enabled Unknown Z No Raise (No more horrible grinding sound at Max Position. However, disable this if you use Auto Bed Leveling)
* Set print bed to 220x220 with the volume of 300 (you can change it to 235x235 however, keep in mind if you have custom hotend cooling or Auto Leveling sensors it'll crash into frame unless you reduced it to 220x220 or less)
* Enabled Mesh Bed Leveling with 5x5 points (I'm old school, you can disable if don't want it)
  ```
  #define MESH_BED_LEVELING
  #define GRID_MAX_POINTS_X 5
  ```
* Enabled Restore Leveling Data after G28 (Very useful for mesh or auto leveling)
* Enabled LCD Bed Leveling Menu

Special Note about LCD stuffs below, I disabled a lot of those to reclaim memory space for above features and I do most of the configuration through octopi and turned my LCD into more of Progress Report with minimal basic stuff. Now that you know why some of the menu options are missing.

* Enabled Slim LCD Menus (reclaim memory space)
* Disabled LCD Info Menu (reclaim memory space)
* Disabled Status Message Scrolling (reclaim memory space)
* Disabled Long Filename Scrolling (reclaim memory space)
* Enabled Set LCD progress manually (useful for Octoprint's plugin)
  * You'll need the following OctoPrint plugins for more accurate progress bar:
    * [Detailed Progress](https://plugins.octoprint.org/plugins/detailedprogress/)
    * [PrintTimeGenius](https://plugins.octoprint.org/plugins/PrintTimeGenius/)
    * [OctoPrint-ProgressBasedOnTime](https://plugins.octoprint.org/plugins/ProgressBasedOnTime/)
    
## Slicer G-Code

Start G-Code
```
G28 ; home all axes
M117 Purge extruder
G92 E0 ; reset extruder
G1 Z1.0 F3000 ; move z up little to prevent scratching of surface
G1 X5.0 Y20 Z0.3 F5000.0 ; move to start-line position adjusted to not hit clips
G1 X5.0 Y220.0 Z0.3 F1500.0 E15 ; draw 1st line
G1 X5.4 Y220.0 Z0.3 F5000.0 ; move to side a little
G1 X5.4 Y20 Z0.3 F1500.0 E30 ; draw 2nd line
G92 E0 ; reset extruder
G1 Z1.0 F3000 ; move z up little to prevent scratching of surface
```
End G-Code
```
G91; set coordinates to relative
G1 F1800 E-3; retract
G1 F3000 Z10; lift nozzle off the print 10mm
G90; change to absolute
G28 X0 Y0 ; homing XY
G1 Z300; prepare for part removal by lowering bed to bottom.
M106 S0 ; turn off cooling fan
M104 S0 ; turn off extruder
M140 S0 ; turn off bed
M84 ; disable motors
```


## Future Plan

Create different set of configuration.h for: 
- [x] Mesh Leveling
- [ ] ~~EZABL Leveling~~ **Please use [TH3D's firmware](https://www.th3dstudio.com/knowledgebase/th3d-unified-firmware-package/)**
- [ ] ~~BLTouch Leveling~~ **Dropped, due to variation of BLtouch/3Dtouch Clones**
- [ ] Create guide on how to edit your firmware for Bltouch/3Dtouch 
