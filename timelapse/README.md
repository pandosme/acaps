# Timelapse Me
Axis Camera ACAP that generate timelapse videos triggered by timer, analytic events or sun noon.

# History
Version 20.2.1
- Published on GIThub

## Installation
1. Download the appropriate EAP-file (mips or arm7hf)
2. Install the ACAP in the camera
3. Before starting the ACAP, mount a SD Card or Network Share
4. Start Timelapse Me
5. Go to Timelapse user interface
6. If you want to trigger on sun noon events, set the cameras GPS coordintates in the tab "Sun Events"

## Creating Timelapse
You can have a number of timelpase recording at the same time.  At least three images in a reqcording is required before the recording is show in the list.

1. Click "Add Timelapse"
2. Give the recording a descriptive name
3. Slsect Storage device (SD Card or Network Share).  They need to be mounted before starting Timelapse Me.
4. Select the event that will trigger image capture.  Note that timers or sun events needs to be configured before shown in select list.
5. Select aspect ration and resolution.  Resolution cannot be changed after recording started.
6. Select the Playback FPS.  Playback can be changed after recording started.
7. Set light conditions Light conditions to only capture images when sun is up.
8. Click Save

## Sun Events
Sun events control the "Light Conditions" and triggers an event a sun noon for daily image captures.
1. On left side, move the marker to the cameras position.
2. Set the Timezone setting.
3. CLick Save

## Timers
Add user-defined timers to trigger on.

# Recording List
A list that shows all timelapse recordings

## Actions
- Edit timelpase settings.  Not all properties can be changed.
- Disable temporarily pauses recording
- Archive (manual archive) 
- Reset flushes recording but continues to capture images
- Delete removes settings and recording

## Download
CLick on the timelapse name to down load it to the computer.

## Frames
View each captured image in the recording

## Archving
In order to reduce the risk of filling up storage, recprdongs should be automaticially archived with a retention period.  The retention period is to give you enough time to download recording before it is removed.  Archiving frequency should de befined on how often images are capture.  A recording triggered by an image per minute should be archived daily.  Images capture once per day should be archived on 9-12 months.






