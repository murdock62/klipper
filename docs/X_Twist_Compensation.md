# X Twist Compensation

This document describes the [x_twist_compensation] module. 

Printer's with a probe that have a probe `y_offset` may give inaccurate probe
results due to a twist in the probe's X axis. This is common in printer's with
designs like the Prusa MK3, Sovol 06 etc and is further described under 
[probe location bias](Probe_Calibrate.md#location-bias-check). It may result in
probe operations such as [Bed Mesh](Bed_Mesh.md), 
[Screws Tilt Adjust](G-Codes.md#screws_tilt_adjust), 
[Z Tilt Adjust](G-Codes.md#z_tilt_adjust) etc returning inaccurate
representations of the bed.

This module uses manual measurements by the user to correct the probe's results.
Note that if your axis is significantly twisted it is strongly recommended to
first use mechanical means to fix it prior to applying software corrections.

## Overview of compensation usage
> **Tip:** A feeler gauge is recommended in place of paper for more accurate 
> measurements

> **Tip:** Perform all levelling and calibration steps at 
> your printing bed temperature
1. Manually tram the bed to the gantry as much as possible 
(eg. using paper at all bed screws)
2. After setting up the [x_twist_compensation] module, 
perform `X_TWIST_CALIBRATE`
* The calibration wizard will prompt you to measure the probe z-offset at a few 
points along the bed
* The calibration wizard recommends a probe `z_offset`
3. Load the X twist calibration using `X_TWIST_PROFILE_LOAD NAME=<profile_name>`
4. Verify that the calibration is active using `X_TWIST_COMPENSATE_STATUS`
5. Perform automatic/probe-based bed tramming operations, such as 
[Screws Tilt Adjust](G-Codes.md#screws_tilt_adjust), 
[Z Tilt Adjust](G-Codes.md#z_tilt_adjust) etc
6. Home all axis, then perform a [Bed Mesh](Bed_Mesh.md) if required
7. Perform a test print, followed by any fine-tuning as desired

> **Tip:** Disable the X twist compensation using `X_TWIST_PROFILE_CLEAR` and
> perform Screws Tilt Adjust/Z Tilt Adjust/Bed Mesh to compare the difference

## [x_twist_compensation] setup and commands
Configuration options for [x_twist_compensation] can be found in the 
[Config Reference](Config_Reference.md#x_twist_compensation).

Commands for [x_twist_compensation] can be found in the 
[G-Codes Reference](G-Codes.md#x_twist_compensation)

## Reference
The calculations for this module are largely based off those found in 
[Marlin PR #23238](https://github.com/MarlinFirmware/Marlin/pull/23238).

A visualization of the issue can be found in 
[this discussion thread](https://github.com/MarlinFirmware/Marlin/issues/22791).