# Tracker
ACAP for Axis Camera & Radar that publish events, motion & radar trackers on MQTT. 

# History
February 22,2020 Version 1.2.3
- Added Root Topic
- Added Setting: image.publish to control publishing image on connect
  Images will not be automatically published by default on connect
- Added Setting: sensors.cpu & sensors.network to control publishing sensors
- Stopped publishing settings

March 4, 2020 Version 1.2.5
- Removed auto-subscription set/<client>/settings

March 21, 2020 Version 1.2.7
- Fixed crash for Axis D2050 Radar

March 22, 2020 Version 1.2.8
- Minor fixes


## MQTT Settings
![home](pictures/home.jpeg)

## Monitor - MQTT Visualization
In the monitor tab you can validate published data as bounding boxes and/or paths
![home](pictures/monitor.jpeg)

# MQTT Topics

### connect/MQTT_Client_ID  [RETAINED]
Annoucement when connecting to broker
```
{
  connected: true,
  client: string,          //MQTT client ID
  model: string,           //Axis product model
  type: string,            //Example "Network Camera"
  serial: string,          //Example "ACCCxxxxxxx"
  mac: string,             //Example "AC:CC:xx:xx:xx:xx"
  IPv4: string,            //IP address
  firmware: string         //Firmware version
  chip: string,            //HW platform
  aspect: string,          //Aspect ration "16:9","4:3","1:1"
  rotation: number         //0,90,180,270 degrees rotation
}
```

### connect/MQTT_Client_ID [RETAINED]
Last-will testamanet when disconnecting from broker
```
{
  connected: false,
  client: string,          //MQTT client ID
}
```
### tracker/MQTT_Client_ID
```
{
  source: string,       //MQTT Client ID
  id: number,           //Unique tracking ID for each object being tracked
  phase: number,        //0: new object detected, 1: object is tracked, 2: object left scene
  timestamp: number,    //UTC ms resolution
  x: number,            // X coordinate [left to right 0 – 1000]
  y: number,            // Y coordinate [top to bottom 0 – 1000]
  w: number,            // Width [0-1000].  Always 10 on radar
  h: number,            // Height [0-1000].  Always 10 on radar
  cx: number            //Center of gravity (x + w/2)
  cy: number,           //Center of gravity (y + h)
  class: {              //Object classifications.
    human: false,       //
    vehicle: false,     //
    face: false         //
  },
  radar: {              //Only relavent for radar
    speed: number,      //Object speed [m/s]
    direction: number,  //Object placement angle from radar center [-180 to 180 degrees]
    distance: number,   //Object distance from radar [meters]
    angle: number       // Object traveling direction related to radar center [-180 to 180 degrees]
    class: number       // Object classification. 2: Undefined, 3: Human, 4: Vehicle
  },
  age: number,          //ms from birth
  distance: number,     //Distance traveled from birth place [0-1000]
  speed: number,	      //Average speed from birth [% distance per second]
  dx: number,           //X Movement from birth [0-1000]
  dy: munber,           //Y movement from birth [0-1000]
  birth: {              //Birth time & place
    timestamp: number,
    x: number,
    y: number,
    w: number,
    h: number,
    cx: number,
    cy: number
  },
  previous: {           //Previous published cx,cy.  Used for drawing path line
    cx: number,
    cy: number
  },
  pause: {              //Longest place where object paused during tracking
    time : number,      //Amount of ms spent in the location
    cx: number,
    cy: number
  }
}
```
### class/MQTT_client_ID/[face, vehicle, human]
Object classifictions is published when installed on a camera with ARTPEC-7 running firmware 9.20 or later.
```
{
  source: string,       //MQTT Client ID
  id: number,           //Unique tracker ID if "motion required" is set.  Otherwise 0
  timestamp: number,    //UTC ms resolution
  x: number,            // X coordinate [left to right 0 – 1000]
  y: number,            // Y coordinate [top to bottom 0 – 1000]
  w: number,            // Width [0-1000].  Always 10 on radar
  h: number,            // Height [0-1000].  Always 10 on radar
  cx: number,           //Center of gravity (x + w/2)
  cy: number,           //Center of gravity (y + h)
  type: number,         //Internal use
  confidence : number,  //Some sort of confidence.  Not predictable
  class: string         //Classification "human", "face" or "human"
}
```
