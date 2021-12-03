# Parking Spaces
Monitor parking space transitions (free or occupied)

## [Download Parking Space](https://files.juhlin.me/acap/Parking)
*Only supported for cameras based on ARTPEC-7*

### Integration
The ACAP produces following two events
1. parking/occupancy:  When a transition between free/occupied occurs
2. parking/vehicles: The total number of vehicles occupying parking spaces

To get messages over MQTT it is recommeded to install [SIMQTT](https://github.com/pandosme/acaps/tree/master/simqtt).
As these event are published on the ONVIF event stream it can also be integrated with a VMS.

## Spaces
Add parking space and use mouse to select the area.  Spaces will turn green (free), red (occupied) or yellow (no transition detected).

## Detection

### Settings
Select detection type (Vehicle or ALPV).  Set as long transition period as possible in order to reduce unwanted transitions due to faulty detections or scene disturbance such as objects blocking the vehicle for short periods.

*Note: a special version of [ALPV](https://www.axis.com/sv-se/products/axis-license-plate-verifier) needs to be installed on the device if you plan to detect license plates.*

### Set detection area
Only needed for Vehicle detection to reduce possible false detections in areas that you are not interested in.

### Set minimum size
Only needed for Vehicle detection to reduce possible false detections when experiencing false detection due to short/small disturbances.

## Limitations
* The result is only as good as the analytics data produced by the device or ALPV
* DLPU cameras with firmware > 10.5 are not supported
