## 1.2.0

- Breaking Changes: Payload property "serial" changed to "device"
- New UI Look & Feel
- Added support for Supervised ports, PIR and casing tampering detection
- Added message "motion/\[DEVICE\]/\[true | false\]" when any of motion detection services such as VMD, ObjectAnalytics, MotionGuard or PIR toggles.  This eliminate the need to monitor a specific service.
- Status message topic changed from "status" to "status/DEVICE_SERIAL_NUMBER"
- The post topic "/true" is no longer added tp ACAP events that are not states.

## 1.1.3
- Made it possible to install SIMQTT on all Axis devices, not just cameras

## 1.1.2
- Fixed a bug that caused respawn when lost connection to broker.
 
## 1.1.1
- Fix a bug in "Publish" that prevented data to be displayed.

## 1.1.0
- Adjusted a number of topics to make them more intuative
- Added sub-topic **/STATE** för all statefull events
- Disabled MQTT Client ID so people will know they are not required to set.  The CLient ID is already unique

## 1.0-2
- Initial version

