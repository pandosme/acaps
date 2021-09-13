# Detection
An MQTT client that publish object detections for cameras that have support for object classification.

## Settings
At the top you will find the MQTT topic that messages are published on

### Set detection area
Use mouse to mark the area of interest

### Set minimum size
Suppress small/sporadic unwanted detections

### Throttling
For slow moving scenes, spare your MQTT broker with unnecessary messages

### Classification
Filter on specific object type

### Confidence
Set higher value do suppress unwanted detections

### Overlapping
Suppress when video analytic provides two or more overlapping detections 

### Detection validation (MQTT Client)
If your MQTT broker supports WebSocket you can view/monitor the detection in the image view.

## MQTT

### MQTT Broker
Should be pretty straight forward.

Pre-topic can be used for
1. Use a topic that your MQTT account is authorized to use
2. Add device ID if you have MQTT clients that needs to subscribe to a specific device and cannot parse the payload (e.g. detection/ACCC8EXXXXXX)

### Additional payload properties
Name and Location will be included in every payload as "name" and "location" if they contain any user defined text string. Select format for property "timestamp". Either EPOCH (milliseconds since Jan 1 1970) is ISO (YYYY-MM-DDTHH:MM:SS+ZONE)
