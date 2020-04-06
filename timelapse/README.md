# Timelapse Me
Axis Camera ACAP that produces timelapse videos (AVI) triggered by timer, camera events or on sun noon.

# History
Version 20.2.1
- Published on GIThub

## Installation
1. Download the appropriate EAP-file (mips or arm7hf)
2. Install the ACAP in the camera
3. Before starting the ACAP, mount SD Card or Network Share
4. Start Timelapse Me
5. Go to Timelapse user interface
6. If you want to trigger on sun noon events, set the cameras GPS coordintates in the tab "Sun Events"

## Creating Timelapse
You can have a number of ongoing timelpase recordings at the same time.  Note that at least three images needs to be in a recording  before the recording is show in the recording list.

1. Click "Add Timelapse"
2. Give the recording a descriptive name
3. Slsect Storage device (SD Card or Network Share).  They need to be mounted before starting Timelapse Me.
4. Select the event that will trigger image capture.  Note that timers or sun events needs to be configured before shown in the Event Select list whan adding timelapse.
5. Select aspect ration and resolution.  Resolution cannot be changed after recording started.  Large resolutions will generate very large recording files.
6. Select the Playback FPS.  Playback can be changed after recording started.
7. Set light conditions Light conditions to only capture images when sun is up.
8. Click Save

## Sun Events
Sun events control the "Light Conditions" and triggers an event a sun noon for daily image captures.
1. On left side, move the marker to the cameras position.
2. Set the Timezone setting.
3. CLick Save

The event is presented under "ACAP" | "Timelapse Me" | "Sun Noon"

## Timers
Add user-defined timers to trigger on.

# Recording List
A list that shows all timelapse recordings

## Actions
- Edit timelpase settings.  Not all properties can be changed after recording started.
- Disable temporarily pauses recording
- Archive (manual archive) 
- Reset flushes recording but continues to capture images
- Delete removes settings and recording

## Download
CLick on the timelapse name to down load it to the computer.  You can download the recording while it is active.  If you are not satisfied with the playback FPS, edit FPS playback in the timelapse settings and download it again.

## Frames
View each captured image in the recording

## Archving
In order to reduce the risk of filling up storage, recordings should be automaticially archived with a retention period.  The retention period gives you time to download recording before it is automatically removed.  Archiving frequency should be defined by how often images are captured.  A recording triggered by an image every minute should be archived daily.  Images capture once per day should be archived between 6-12 months.
