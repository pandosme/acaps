# Detection
An MQTT client that publish object detections (classifications) for cameras that supports for object classification.

### [Download (ZIP)](https://api.aintegration.team/acap/detection?source=github)
*Supported platforms: ARMv7hf*

## Messages View
The message view is primarily for installation and trouble-shooting.  In order to visualize detections, the MQTT broker must support WebSocket connections, typically port 1884.

![messages](https://github.com/pandosme/acaps/raw/master/detection/images/detection-messages.jpeg)

* MQTT topic:  The topic that message will be published on.  You can copy/paste this into your MQTT client
* Name:  If you have many cameras, you can set a name that will be included in the payload
* Group:  If you have cameras on multiple locations, you can add a group name that will be included in the payload
* Overlapping:  The analytics may multiple detections that overlap.  Select if you want them or not
* Throttling:  Controls often messages will be published.  For slow changing scenes you reduce the strain on the system.  Setting to 1 message every 10 second will include all detections under that time.

## Filter
To reduce the strain for a system it is a good practice to remove as much unnecessary data.

![messages](https://github.com/pandosme/acaps/raw/master/detection/images/detection-filter.jpeg)

* Set detection area:  Use the mouse and define the area of interest.  It is the center of the object that needs to be inside the area.
* Minimum size:  Use mouse to set minimum width and height.  Use with caution.
* Maximum size:  Some false detections may be very big.  Use this filter to remove them.
* Set ignore area:  If there are areas withing the area-of-interest that generates disturbance detections.
* Classification types:  Select the classifications you want (or do not want).  It is possible to change the name that will be published in the payload.

## MQTT
Should be pretty straight forward.

![messages](https://github.com/pandosme/acaps/raw/master/detection/images/detection-mqtt.JPG)

* TLS: Select if you connect over TLS (typically on port 8883).  Select "Trust certificate" if the broker is using a self-signed certificate.
* Set client certificate:  For MQTT broker that requires a client TLS certificate for authentication
