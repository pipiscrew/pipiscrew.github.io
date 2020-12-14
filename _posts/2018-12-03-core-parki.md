---
title: Core Parking Options in Advanced Power Options
author: PipisCrew
date: 2018-12-03
categories: [news]
toc: true
---

Changing Parking Settings Using PowerCfg.exe

You can also change these settings via Window’s Powercfg.exe. You must run this utility with elevated rights, so be sure to open an elevated console window by right-clicking ‘cmd.exe’ and selecting ‘Run as Administrator’.

Note that these commands adjust the currently active power profile. You can adjust specific ones by using their GUID, or switching to them prior to running these commands.

First, backup ALL your Power Settings by creating a dump of everything to a TXT file. It is unlikely you will ever need this, but…

`powercfg /qh > powerconfig.txt`

To mandate 50% of available cores always remain unparked, run:

`powercfg -setacvalueindex scheme_current sub_processor 0cc5b647-c1df-4637-891a-dec35c318583 50`

To adjust it so that only 25% of available cores remain active at all times, allowing 75% of available cores to be parked, you’d run:

`powercfg -setacvalueindex scheme_current sub_processor 0cc5b647-c1df-4637-891a-dec35c318583 25`

‘0’ <zero> indicates to park as many CPU cores as possible.

To enable maximum use of CPU Parking for the power profile you are currently using:

`powercfg -setacvalueindex scheme_current sub_processor 0cc5b647-c1df-4637-891a-dec35c318583 0`

To disable CPU Parking completely for the power profile you are currently using, you’d want to run:

`powercfg -setacvalueindex scheme_current sub_processor 0cc5b647-c1df-4637-891a-dec35c318583 100`

All the above configure core parking while the system is plugged into AC power. For DC (battery) power, core parking is usually forced, but to configure it you would instead use ‘-setdcvalueindex’.

APPLY New Settings, NOW!

After changing the power scheme settings for CPU Parking as desired, you then want to make the changes active by running the command:

`powercfg -setactive scheme_current`

With ParkControl, a reboot is NOT required for these changes to take effect – in contrast to direct registry edits or other core parking software.

After applying tweaks, check the Windows Resource Monitor (resmon.exe) and verify that CPU Parking is indeed as you intend.

Execute the following commands to hide or un-hide the primary ON/OFF switch for core parking in the power plans.

Show Core Parking Settings:

`powercfg -attributes SUB_PROCESSOR cc5b647-c1df-4637-891a-dec35c318583 -ATTRIB_HIDE`

Hide Core Parking Settings:

`powercfg -attributes SUB_PROCESSOR cc5b647-c1df-4637-891a-dec35c318583 +ATTRIB_HIDE`

Core Parking and Intel Skylake and Above

Due to the inefficiencies of OS managed core parking, Intel took over core parking in Skylake and above. These thus have different core parking settings. The most important may simply be the ON/OFF switch of it’s Autonomous Mode, though there is also an aggressiveness %.

Autonomous Mode turns on/off the CPU’s ‘smart parking’, but does NOT turn off OS managed core parking. To do that, use ParkControl or the usual ways.

Unhide Skylake+ Core Parking Settings without direct registry edits (real-time, no reboot required!):

    powercfg -attributes SUB_PROCESSOR 8baa4a8a-14c6-4451-8e8b-14bdbd197537 -ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 36687f9e-e3a5-4dbf-b1dc-15eb381c6863 -ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 4e4450b3-6179-4e91-b8f1-5bb9938f81a1 -ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR cfeda3d0-7697-4566-a922-a9086cd49dfa -ATTRIB_HIDE

Re-hide Skylake+ Core Parking Settings without direct registry edits (real-time, no reboot required!):

    powercfg -attributes SUB_PROCESSOR 8baa4a8a-14c6-4451-8e8b-14bdbd197537 +ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 36687f9e-e3a5-4dbf-b1dc-15eb381c6863 +ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 4e4450b3-6179-4e91-b8f1-5bb9938f81a1 +ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR cfeda3d0-7697-4566-a922-a9086cd49dfa +ATTRIB_HIDE

Execute the following commands to hide or un-hide the primary ON/OFF switch for core parking in the OS:

Show Unresearched Advanced Options

    powercfg -attributes SUB_PROCESSOR 06cadf0e-64ed-448a-8927-ce7bf90eb35d -ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 12a0ab44-fe28-4fa9-b3bd-4b64f44960a6 -ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 40fbefc7-2e9d-4d25-a185-0cfd8574bac6 -ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 4b92d758-5a24-4851-a470-815d78aee119 -ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 7b224883-b3cc-4d79-819f-8374152cbe7c -ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 943c8cb6-6f93-4227-ad87-e9a3feec08d1 -ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 619b7505-003b-4e82-b7a6-4dd29c300971 -ATTRIB_HIDE

Hide Unresearched Advanced Options

    powercfg -attributes SUB_PROCESSOR 06cadf0e-64ed-448a-8927-ce7bf90eb35d +ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 12a0ab44-fe28-4fa9-b3bd-4b64f44960a6 +ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 40fbefc7-2e9d-4d25-a185-0cfd8574bac6 +ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 4b92d758-5a24-4851-a470-815d78aee119 +ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 7b224883-b3cc-4d79-819f-8374152cbe7c +ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 943c8cb6-6f93-4227-ad87-e9a3feec08d1 +ATTRIB_HIDE
    powercfg -attributes SUB_PROCESSOR 619b7505-003b-4e82-b7a6-4dd29c300971 +ATTRIB_HIDE

ref- [https://bitsum.com/parkcontrol/](https://bitsum.com/parkcontrol/)</zero>

origin - https://www.pipiscrew.com/?p=14478 core-parking-options-in-advanced-power-options