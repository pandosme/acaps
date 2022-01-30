# Head detection
Detect heads in scene supported by cameras with DLPU (Deep-Learning Processor).  Heads generates camera events when detected and can be integrated to VMS.  By using MQTT it can easily be integrated with other IT systems.

## [Download](https://files.juhlin.me/acap/heads)

### Typical use cases
- Head counting
- Recording controller "while heads are detected in scene"
- System automation
- Que management integration

### Features
- Head presence event
- Head occupancy event
- Transition filter to reduce event toggling on sporadic detections
- Ability to apply user-defined filters (Area-of-intrest & Head size limits)
- Live video with augmentation for installation, configuration and validation.

## Filter settings
Select filter and use mouse do adjust box
- Detection area
- Minimum head size
- Maximum head size
- Ignore area (if needed within the detection area)

# Changelog

### 1.2.0
- Changed name from "Heads" to "Head Detection"
- Minor adjustment
- Automatic freeware registration

### 1.1.0
- Improved detection filter
- Adjusted event declarartions
 
### 1.0.0
- Initial commit

