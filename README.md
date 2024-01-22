# Whammy-MIDI-Controller-V2.3 (Public)
A programmable controller for the Digitech whammy using Arduino with a touchscreen interface

The code for this project is being kept private but can be shown by request. 
Email: robert.wilkinson1@tiscali.co.uk

## Updates:
- Multiple save files and a config file.
- Developed a case for the system.
- Added a 1/4 jack for a removeable footswitch for play/pause. This connects to the button circuitry.
- Plan to add a TRS jack for a second footswicth for the other button functionality. This will also include start/stop to prevent need for 2 footswitches.
- More code optimisations to reduce program size to fit on the arduino uno with the additional features (More required as this is still at 98-99%!)

![20231020_150332](https://github.com/RWilko31/Whammy-MIDI-Controller-V2-Public/blob/main/Pictures/MidiController%20w_case.jpg)

## Load presets:

The ability to load presets during run time has now been added.
This allows the user to have multiple presets saved to the SD card which can be swapped out with the load menu.

https://github.com/RWilko31/Whammy-MIDI-Controller-V2/assets/92086002/5e81e842-1c03-480f-a094-79ac1b673126

Menu options:
- Load: loads the current preset (The selected preset can be changed with the < > buttons)
- New: creates a new blank save file. This will have the name of the current number of save files .txt e.g 3.txt
- Delete: this deletes the selected save file (The selected preset can be changed with the < > buttons)
- Cancel: returns to the sequencer
  
The load menu can be exited by selecting cancel, pressing the load button again or by pressing the center menu button (which displays "Files" while in the load menu).

## Config file:

With the addition of loading files some new options are now available:

- Directory: The config file specifies the location the presets are stored in case the user wishes to move the location
- Default preset: The user can specify which preset file is loaded when the device powers on (this is 1.txt by default)
- Reset : An option to switch the pedal to a specified mode when the sequencer is stopped (0 or 1) (this is 1 by default)
- Reset mode: The mode to switch to when the sequencer is stopped if Reset is 1 (this is 67 by default)

The user can now edit the config.txt file to change these additional functions. The config file is read when the device boots up, due to this the file must be at the root of the SD card and named Config.txt.

Due to the limitations of code size, the file is layed out in a simple to process layout.
Each line must only contain the value required, any extra text in the file will cause read issues as the file is read a full line at a time.
The data must be presented as listed above each on a new line. 

The default Config.txt can be found here:

## Reset Mode:

While testing the sequencer it became apparant that it can be difficult to switch it off at the right time to keep the correct mode active or that the mode needs to be switched to a different one when stopped.
To accomodate this the reset mode function has been added to allow the user to specify a mode to switch to when the sequencer is stopped. This can be editted in the Config.txt file and its settings apply to all presets (Eventually this will be moved to the preset file so it can be adjusted for each preset)
By default this switches to mode 67 (pedal off +1oct).
The config file provides the option to turn this function on or off and to change the mode it switches to.

## Presets:

The user can use preset files to save the device settings and load them again later. This prevents the need to set up the device every time it is used.
Multiple presets can be saved to the SD card and then selected during use with the load menu. The preset loaded when powered on can also be changed in the config.txt file.

The user can use the load menu to create a new blank preset and then save the current settings to it with the save button.
Preset files can also be created on a computer by making a .txt file and then adding the settings in the correct layout.

Layout:
- Button 1 mode
- Button 2 Mode
- Button 3 Mode
- Number of sequence steps
- mode,time

The number of sequence steps tells the device how many steps to create and then fills these steps with the data beneath it. This means for 3 steps there must be 3 lines under it stating the mode and time for each step e.g:
- 3
- 10,20
- 10,20
- 10,20
  
This would create 3 steps with values 10,20 for each. If only 2 steps are given but data for more is provided the device will only load the first 2 steps and ignore the rest.

An example preset can be found here:

## Demo:

https://github.com/RWilko31/Whammy-MIDI-Controller-V2/assets/92086002/0300b552-f534-40fb-8c4b-cd9e725e9ace

## Background
The Digitech whammy is a pitch shifting pedal allowing its audio input to be shifted up or down. The pedal features a MIDI port that allows the pedal to be controlled external providing the ability to change its settings with a sequencer providing more possibilites than normal.
MIDI controllers can be quite expensive and so this project implements an arduino to replicate the functionality at a low cost.

## About
This version of the arduino MIDI controller is based around a simpler design utilising a touch screen for input and display allowing for the same functionality with more expandability and a simpler to use UI. This version utilises more complex code and so for modification V1 remains easier to work with. 

V1: https://github.com/RWilko31/Whammy-MIDI-Controller

## Buttons

The function buttons allow the user to easily start/stop the sequencer with a footswitch instead of using the touch screen. An additional 3 buttons can be programmed by the user to change the whammy to a specific mode when pressed. 

A jack has been added to allow the start/stop button to use a footswitch, however a TRS jack is required to allow the extended functionality of the other 3 buttons and so has not yet been implemented. A space for this is present in the case and so will be wired in when possible.


![image](https://github.com/RWilko31/Whammy-MIDI-Controller-V2/blob/V2.3/Pictures/MidiController%20w_case%20side.jpg)

These buttons use a resistor to set the voltage produced when pressed allowing all buttons to function from a single analog input on the arduino. This allows further buttons to be potentially added if the voltages are provided, however due to limitations in program size this can not yet be added. Eventually the button resistance will be specified in the save file on the sd card allowing the user to program in any additional buttons.

## Parts List
- Arduino UNO
- ILI9486 Touch screen module
- MIDI port
- 220 ohm resistor

## Schematic:

- MIDI port
  
![image](https://github.com/RWilko31/Whammy-MIDI-Controller-V2-Public/blob/main/Pictures/Schematic2.PNG)

- Buttons
  
![20231020_150332](https://github.com/RWilko31/Whammy-MIDI-Controller-V2-Public/blob/main/Pictures/Schematic3.PNG)
