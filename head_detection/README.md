# Heads
An ACAP that detects human heads in the scene and generates an precense and occuppancy events.


## Prerequisite
An Axis camera that supports deep-learning w/o TPU module.

## [Download](https://files.juhlin.me/acap/heads)

## Settings
Adjust and validate head detection.  To optimize detections, set detection area, max/min head size and ignore area.

## Integration
Two events are fired based on detection.

### Presence
A stateful (true/false) when any heads are detected in scene.  This event is availble in the cameras event/action as a condition (e.g. record while heads are detected).

### Occupancy
And event is fired when the number of detected heads changes.  The event payload includes the number of heads currently being detected.  This event is targeting applications that monitors the number of detected heads (e.g. queue monitoring).  The occupancy event is not availabe in the cameras event/action to trigger an action. 

The easiest integration is by using MQTT ACAP [SIMQTT](https://github.com/pandosme/acaps/tree/master/simqtt)

Topic: 
```
simqtt/acap/heads/occupancy
```

Payload:
```
{
  "device":"ACCC8Exxxxx",
  "timestamp":1655668037429,
  "json":"[{\"id\":15125,\"x\":318,\"y\":500,\"w\":89,\"h\":206,\"cx\":362,\"cy\":604,\"class\":6,\"type\":\"Head\"}]",
  "value":1,
  "event":"acap/heads/occupancy"
}
```
The value property tates how many heads are currently in the scene.  The json property defines an array of where in the view the heads were detected (coordintate system is [0,0]-[1000,1000] origo is top-left.

# Changelog

### 1.3.0
- Moved filters to settings page.

### 1.2.0
- Changed name from "Heads" to "Head Detection"
- Minor adjustment
- Automatic freeware registration

### 1.1.0
- Improved detection filter
- Adjusted event declarartions
 
### 1.0.0
- Initial commit
