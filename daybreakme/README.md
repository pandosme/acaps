# Daybreak Me
ACAP for Axis Cameras that generates  events on dawn, sunrise, sun noon, sunset, dawn and midnight. The typical use case is to adjust camera settings based on day/night.  The sun events can also be used as trigger device actions.

![home](pictures/home.png)

# [Download (ZIP)](https://files.juhlin.me/acap/daybreakme)
*Supported platforms: MIPS, ARMv7hf, AARCH64*

Unzip files and install the eap-file corresponding to your device

# Settings

## Location
Use the mouse to move the marker to the city where the camera is mounted.  Note that if the client browser does not have Internet access you will need to manually set the GPS coordinates (additional inputs will be shown).

## Device time
Make sure the the cameras time zone, DST is correctly set.

### Dawn/Dusk offset
Dawn/dusk maybe be too dark and sunrise/sunset may be too bright for some use cases.  By adding a sun angle offset a few degrees, the dawn/dusk times will be adjuste (brigter).  By setting the value to 2 degrees, the dawn time will be adjusted inbetween the real dawn and the sunrise (the same applies to dusk).

# Day/Night profiles
A list of common camera settings that may need to have different values during day or night.  Note that the predefined list may not work for all camera models.  You may need to edit a profile and set the correct paramter path (check VAPIX documentation).  You can also add your own camera settings bu clicking "Add profile".

# Snapshots
A snapshot will be taken every sun event.  This is a tool that may help to identify the best Dawn/Dusk offset.
