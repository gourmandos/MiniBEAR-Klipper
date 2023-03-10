# MiniBEAR-Klipper
Custom miniBEAR config

THIS IS STILL A WORK IN PROGRESS - use at your own discretion, I take no responsibilty. 
REFER TO [WIP](WIP.md) for completion status. 

### Prerequisites

  * A Prusa-Mini with bear upgrade with a Buddy MCU board (the stock board included with Prusa Mini printers).
  * In order to flash a custom firmware on the Buddy board, you need to [break the appendix](https://help.prusa3d.com/article/flashing-custom-firmware-mini_14) on the board, which VOIDS THE WARRANTY!
  * Intructions on installing Klipper on the Prusa Mini [here](https://github.com/singh-gur/mini_klipper) .
  * Klipper + client already up and running on your choice of host. You can use [Mainsail](https://docs.mainsail.xyz/) on a Raspberry Pi 3b+ or Pi Zero 2W. Install can be done easily with [KIAUH](https://github.com/th33xitus/kiauh) : Klipper Installation And Update Helper.


### Cloning to Your Config Directory

SSH into your Pi, and run the following commands:

    cd ~/klipper_config
    git clone https://github.com/gourmandos/MiniBEARb-Klipper

You should now see the `printer.cfg` file and the `/cfg/...` subfolders in the current `~/klipper_config` directory.


### Printer Setup and Initialization

 * In [`printer.cfg`](/printer.cfg), make the following changes:
  * Under `[mcu]`, verify `serial:` matches your Buddy's serial id so the Klipper host can talk to it.
 * Run through all of the Klipper [configuration checks](https://www.klipper3d.org/Config_checks.html) to ensure your printer is ready to print safely.
  * This page references Octoprint, which can be ignored - everything can be done the same in Mainsail, Fluidd, or any other .  
  * Pay particular attention to the [verify stepper motors](https://www.klipper3d.org/Config_checks).html#verify-stepper-motors) section, where you check the steppers are moving in the right directions. Remember that when the y axis (the bed) is moving in a positive direction, that means the *nozzle* is moving in a positive direction *relative to the bed*.
 * **IMPORTANT:** Use [`PROBE_CALIBRATE`](https://www.klipper3d.org/Probe_Calibrate.html#calibrating-probe-z-offset) to calibrate your base probe offset (the z-offset from the probe trigger point to the actual tip of the nozzle) so you don't crash your nozzle/damage the bed. Do not assume the current value in this config matches your printer.
 * Check and calibrate [`rotation_distance`](https://www.klipper3d.org/Rotation_Distance.html).

 ### Slicer Setup
 
 In your slicer of choice, make sure the following is called in the "start gcode" section: 
 `PRINT_START EXTRUDER_TEMP=[first_layer_temperature] BED_TEMP=[first_layer_bed_temperature]`
 
 As well as the following in the "end gcode" section:
 `PRINT_END`
 
 
 ### Klipper Config Reference

 [Klipper Configuration Reference Docs](https://www.klipper3d.org/Config_Reference.html)  
 [Klipper Supported G-codes Docs](https://github.com/Klipper3d/klipper/blob/master/docs/G-Codes.md)
 
### Must read

[Tuning Guide](https://ellis3dp.com/Print-Tuning-Guide/)

 ### Credits
 
* Adapted from https://github.com/ngolshan/mk3s-barebones-klipper-config .
* Original pin mapping and LCD support from https://github.com/matthewlloyd .

* Large parts of this config are based on the [Universal Prusa Config](https://github.com/Prutsium/3D-Druckerplausch-Klipper) by Pinky#1302 on the 602 Wasteland Discord.
* Various macros adapted from other users of the [602 Wasteland Discord Server](https://discord.gg/hYUjSnW) .