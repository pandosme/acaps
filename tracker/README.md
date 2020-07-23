# Tracker
ACAP for Axis Camera & Radar that publish events, motion & radar trackers on MQTT. 

- [MIPS](https://github.com/pandosme/acaps/raw/master/tracker/Tracker_mips.eap)
- [ARMv7](https://github.com/pandosme/acaps/raw/master/tracker/Tracker_amrv7.eap)
- [AARCH64](https://github.com/pandosme/acaps/raw/master/tracker/Tracker_aarch64.eap)


# Settings

![home](pictures/tracker_home.png)

## MQTT Broker
Settnings should pretty straight forward.

## MQTT Data settings
### Send birth objects
 Sends message when a new object is detected in the scene that fulfills the birht criteria.  Should be disabled if there are no consumer that requires real-time data.

### Send tracking objects
Sends object update when object moves more than Tracker Sway limit.  Should be disabled if there are no consumer that requires real-time data.

### Send complete tracking objects
After an object left the scene (object death), a message will be send containing birht and deat information.  This is typically used when detected objects are store in a database.  

### Include image in complete objects
Include a JPEG image in the last message (complete tracking) message.  The data will be base64 encoded.

## Object Filter (Optimze the system)
In many cases there are areas where there is no interest in tracking objects. Filtering unnessessery data will optimize the system perfomance.  On the filter tab you can define an area where objectes needs to appear (Birth Area), how old they need to be and how often objects are published. 

A birth message and tracking will start when an object is inside the birth area, is at least X seconds and traveled Y % distance.  Tracking objects will then be published until the object disapears from scene.

A death object will only be published when all filters are fulfilled including minimum age, distance and max speed. 

![filter](pictures/filter.png)

* Tracker Sway limit:  Redcues the number of publishing when tracking. The object needs to move x% before an update is published.   Recommeded value is 3-5%.
* Birth area:  Defines an  area that the object needs to pass before tracking starts.  Click the green button and use mouse to adjust area.
* Birht min age:  Defines the time between an object is detected and when a birth message is posted.  Increase time reduce sporadic detections.
* Birth min distance:  Defines the distance a detected object needs to move before a birth message is posted.  Increase distance to reduce sporadic detections.
* Min age, distance and speed is similar to Birth-settings.

## TLS Certificates
If the MQTT Broker requires client certificate, upload them here.

## Payload
Data structure depends on user selection but will contain the following.
```
{
    "client": string,            //MQTT Client name
    "device": string             //Device serial number
    "timestamp": number,         //EPOCH timestamp ms resolution
    "phase": number,             //0 = new object detected, 1 = object is tracked, 2 = object left scene (dead)
    "id": number,                //Unique tracking ID for each object being tracked
    "x": number,                 //Bounding box x,y,w,h
    "y": number,                 //Coordinate system is [0,0]-[1000,1000].  [0,0] is top left corner
    "w": number,
    "h": number,
    "cx": number,                //Center of gravity 
    "cy": number,         
    "dx": number,                //Total X distance traveled since birth [-1000,1000]
    "dy": number,                //Total Y distance traveled since birth [-1000,1000]
    "age": number,               //Age in seconds since birth
    "speed": number,             //Total distance in percent/second
    "distance": number,          //Distance traveled in percent of view 
    "pause": number,             //The longest pause the object made while beining tracked
    "pauseX": number,            //Location of longest pause
    "pauseY": number,
    "pcx": number,               //Previous CX,CY.  Used for drawing path in live visualization
    "pcy": number,
    "birth": number,             //When object was born.  EPOCH timestamp ms resolution
    "bx":number,                 //Birth x,y
    "by":number,                 
    "bw":number,                 //Birth width & height
    "bh":number,
    "bcx":number,                //Birth center of gravity cx,cy
    "bcy":number
}
```
