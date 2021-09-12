# SIMQTT

An MQTT Client for Axis devices that simplifies monitoring events over MQTT. All common events are automatically published. Users may add additional properties in payload such as name, location and various time formats.

## Installation

Install appropriate EAP-file depending on your device paltform

## Common topics

### simqtt/acap/\[ID\]/\[EVENT\]/\[STATE\]
All events produced by ACAPs are publish on /simqtt/acap.  The payload may vary depending on events as additional properties may be specific to that event.

ID = ACAP id

EVENT = event id

STATE = true or false

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628697522589,
  "state": true,
  "name": "Device nicename",
  "location": "Somewhere"
}
```

### simqtt/motion/\[DEVICE\]/\[STATE\]
Published when selected motion detection services toggles. This provides a way to get motion detection regardless what triggered the motion.
- VMD
- ObjectAnalytics
- MotionGuard
- PIR

DEVICE = Device serial number
STATE = true or false

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628697522589,
  "state": true,
  "name": "Device nicename",
  "location": "Somewhere"
}
```


### simqtt/audio/detection/\[STATE\]
Published when audio volume (selected productes) toggles between threshold level

STATE = true or false

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628697524191,
  "state": false,
  "channel": 1,
  "name": "Device nicename",
  "location": "Somewhere"
}
```
### simqtt/connect/DEVICE-ID    
Published when device connects to broker and disconnects (Last-will testament).  May be used to build and monitor system inventory.

*This topic is retained on the broker.*

DEVICE-ID = Device device number
```
{
  "connected": true,
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628697562588,
  "model": "AXIS P3227-LVE",
  "firmware": "10.6.0",
  "IPv4": "1.2.3.4",
  "name": "Device nicename",
  "location": "Somewhere"
}
```
Last-will testament
```
{
  "connected": false,
  "device": "ACCC8EXXXXXX"
}
```

### simqtt/day/\[STATE\]
Published when camera toggles between day and night, enabling/disabling IR-cut filter (color/bw).

STATE = true (day) or false (night)
```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628697562588,
  "state": true,
  "name": "Device nicename",
  "location": "Somewhere"
}
```
### simqtt/heater/\[HEATER\]/\[STATE\]
Published when heater starts/stops (supported in selected products)

HEATER = Heater Id

STATE = true or false

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628697562588,
  "heater": 0,
  "state": false,
  "id": 0
}
```

### simqtt/port/\[PORT-ID\]/\[STATE\]
Published when digital input toggles between high/low (selected products).

PORT-ID = Device input port.  Index starts a 0 for port 1;

STATE = true (high/active) or false (low/inactive) depending how the ports are configured

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628697524115,
  "state": false,
  "port": 0,
  "event": "Device/IO/Port",
  "name": "Device nicename",
  "location": "Somewhere"
}
```

### simqtt/ptz/moving/\[ID\]/\[STATE\]
Published when PTZ toggles between moving and stopped.

ID = PTZ Id (typically 0)

STATE = true (moving) or false

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628697524190,
  "channel": 1,
  "state": false,
  "name": "Device nicename",
  "location": "Somewhere"
}
```

### simqtt/ptz/preset/ID
Publish when PTZ lands on a preset

ID = Preset ID

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628697524209,
  "channel": 1,
  "preset": "Home",
  "name": "Device nicename",
  "location": "Somewhere"
}
```

### simqtt/recording/\[STATE\]
Published when SD Card recording starts/stops.

STATE = true (recording) or false

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628698370897,
  "state": false,
  "name": "Device nicename",
  "location": "Somewhere"
}
```

### simqtt/relay/\[RELAY\]/\[STATE\]
Published when device relay toggles high/low

RELAY = Relay id

STATE = true or false

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628697524064,
  "state": false,
  "relay": 4,
  "name": "Device nicename",
  "location": "Somewhere"
}
```

### simqtt/status/\[device\]
Published every 15 minutes.  Typically used for monitoring device performance.

Device = Serial number

```
{
  "device": "ACCC8EXXXXXX",
  "model": "AXIS P1375",
  "IPv4": "1.2.3.4",
  "firmware": "10.5.2",
  "network": 1696.5,
  "cpu": 0.93,
  "timestamp": 1628698625417,
  "name": "Device nicename",
  "location": "Somewhere"
}
```

### simqtt/storage/SD/\[STATE\]
Published when SD Card is available for recording (mounted and no disruptions)

STATE = true or false

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628698370873,
  "state": true,
  "name": "Device nicename",
  "location": "Somewhere"
}
```

### simqtt/video/streaming/\[STATE\]
Published when any client streams video(or not).

STATE = true or false

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628698370870,
  "state": true,
  "name": "Device nicename",
  "location": "Somewhere"
}
```

### simqtt/tampering/\[TYPE\]

TYPE:
- video: Published when camera is redirected, blocked or de-focused
- port: Published when tampering supervised ports is detected (selected products)
- casing: Published when someone opens the caseing (selected products)
	
```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628650145654,
  "name": "Device nicename",
  "location": "Somewhere"
}
```

### simqtt/temperature/\[THRESHOLD\]/\[SENSOR\]/\[STATE\]
Published when device temperture is above or below acceptable threshold limits

THRESHOLD = high or low

SENSOR = Internal sensor id

STATE = true (outside acceptable limit) or false (within acceptable limit)

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628650145654,
  "sensor": 0,
  "threshold": "high",
  "state": true,
  "name": "Device nicename",
  "location": "Somewhere"
}
```

### simqtt/pir/\[STATE\]
Published when PIR sensor (selected productes) toggles

STATE = true or false

```
{
  "device": "ACCC8EXXXXXX",
  "timestamp": 1628697524191,
  "state": false,
  "channel": 1,
  "name": "Device nicename",
  "location": "Somewhere"
}
```
