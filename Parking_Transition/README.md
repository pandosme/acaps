# Parking Transition
An ACAP that generates an event when a parking space changes transition between free and occupied.  Typically used for system integration to trigger actions when a specific parking space is free/occupied. 

![Settings](https://files.juhlin.me/image/NMVTRKFYVW)

# [Download (ZIP)](https://files.juhlin.me/acap/Parking)

## Spaces View

### Add parking spaces
For every parking space visiable in the view...
1. Click the green Add button
2. Use mouse mouse to move/resize the the box to define a parking space.  The center of the vehicle must be within the box.
3. Set a name (id) for the parking space.
4. Save

To edit a parking space, click the space in the table below, make adjustments and click save.

### Validation
To verify correct behaviour, each space will be marked red, green or yellow.  Red mean occupied, green means free and yellow means no transition has not been detected.  The table below shows the same information in text.

## Detection View

### Area-of-intrest
If you notice many false detections, click the button "Set detection area" or "Set minumum size" and use mouse to adjust boxes.

### Detection type
Select "Vehicle detection" to use object classification.  If [Axis License Plate verifier](https://www.axis.com/products/axis-license-plate-verifier) is installed on the camera you can use license plate as the detector.  The license plate number will be included in in the event.

### Confidence level
If you notice false detection you could increase the minimum detection confidence level

### Transition period
Moving vehicles or persons may block a parked vehicle for a short time and a transition event may occure.  Select longer transitions period to avoid this.  An event will not be fired until a space is free/occupied for the given time.

## System Integration
An event is fired on every transition.  THis can be used to trigger actions in the camera or a VMS (Video Management System).  A second event that provides the number of vehicles occupiyn parking spaces.

For easy integration to non video systems it is recommeded to use [SIMQTT](https://github.com/pandosme/acaps/tree/master/simqtt) to get data published as MQTT payload.

**simqtt/acap/parking/Space1/true**
The topic that SIMQTT will publish transition /true = occupied, /false = free.  The property "state" will also define occupied (true) or false (free)
```
{
  "name":"Camera 5",
  "location":"Garage 3 level 3",
  "device":"ACCC8EXXXXXX",
  "timestamp":1644442759226,
  "spaceID":"Space1",
  "plate":"",
  "state":true
}
```
**simqtt/acap/parking/vehicles**

The topic that SIMQTT will publish on each transistion with the property "value" that states how how many vehicles is detected in all parking spaces.
```
{
  "name":"Camera 5",
  "location":"Garage 3 level 3",
  "device":"ACCC8EXXXXXX",
  "timestamp":1644442759226,
  "value":4
}
```

# Changelog

### 2.1.0
- Automatic freeware registration 

### 2.0.0  Breaking change
*Uninstall version 1 before installing version 2*

- Support for DLPU cameras
- Occupancy event replaced by unique events for each parking space.  This provides an easy way to trigger unique actions for each parking space.
- User interface updates

### 1.0.0
* Initial version

