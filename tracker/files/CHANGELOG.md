## 2.7.0
* Added MQTT publish for object classification (vehicles & humans).  Publishing can be controlled in the new menu option "Classifictions"

## 2.6.4
- Added support for radar AXIS D2110-VE (only applicaple for platform ARMv7hf)

## 2.6-3
- Fixed a bug that reset the publish checkboxes when saving filters
- Fixed a bug that only sent a birth object when image publish was enabled
- Fixed bug that impacted image publishing

## 2.6-0
- Added support for AXIS D2050 Radar
- JSON Payload is now always flat.  Removed the user selection of JSON structure.
- Added ability to set user properties for payload.  Typpical used for "nide name" and  "locatiion"
- Added Web client to visualize the tracker data.  The web client needs to connect to the Broker  WebSocket port
- Added support for Object classification "human" and "vehicles" (requires ARTPEC-7 devices)

## 2.5-0
- Support for TLS w/o client certificates
- UI restructuring

## 2.0-1
Version 2 is optimzed for post processing of video analytics tracker data.  All other features has been removed and may appear in other future ACAP.
- Tracker payload has a new structure
- An image capture of birth detection may be included in the payload
- Event publish is removed
- Subscribe/Action is removed
- Object classifications (ARTPEC-7) is removed

## 1.3-0
- Added property device to MQTT payload that contains the device serial number
- Adjusted payload for topic connection (and LWT)

## 1.2-8
- Minor fixes

## 1.2-7
- Fixed crash for Axis D2050 Radar

## 1.2-5
- Removed auto-subscription set/<client>/settings

## 1.2-3
- Added Root Topic
- Added Setting: image.publish to control publishing image on connect
  Images will not be automatically published by default on connect
- Added Setting: sensors.cpu & sensors.network to control publishing sensors
- Stopped publishing settings



