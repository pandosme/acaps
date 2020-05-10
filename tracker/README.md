# Tracker 2.0-0
ACAP for Axis Camera & Radar that publish events, motion & radar trackers on MQTT. 

**Big breaking changes in 2.0-0.  Check changelog**

## MQTT Settings
![home](pictures/home.png)

Settnings should  pretty straight forward.  Note that only TCP/MQTT is support, not TLS nore WebSocket.
- Tracker Publish version defines the data structure for the structure.  Version 1 is deprecated and should only be used for integration. 

## Filter - Optimze the system
In many cases there are areas where there is no interest in tracking objects. Filtering unnessessery data will optimize the system perfomance.  On the filter tab you can define an area where objectes needs to appear (Birth Area), how old they need to be and how often objects are published. 

* Publish: Depending on use-case.  "Birht" and "Tracking" should be enabled fo real-time application (e.g. visualization). "Death" should be used for post-processing application.  An JPEG immage may also be included (in Death publish).
* Treaacker Sway limit:  Redcues the number of publishing when tracking. THe object needs to move x% before an update is publioshed.   Recommeded value is 3%.
* Birth area:  Defines an  area that the object needs to appear or pass before tracking starts.  Click the green button and use mouse to adjust area.
* Birht min age:  Defines the time between an object is detected and when a birth message is posted.  Increase time reduce sporadic detections.
* Birth min distance:  Defines the distance a detected object needs to move before a birth message is posted.  Increase distance to reduce sporadic detections.
* Min age, distance and spped is similar to Birth-settings.

![filter](pictures/filter.png)



# MQTT Topics

### connect/MQTT_Client_ID [RETAINED]
Last-will testamanet when disconnecting from broker
```
{
  connected: false,
  client: string,          //MQTT client ID
  serial: string,          //Example "ACCCxxxxxxx"
}
```
### tracker
Data structure is optimized for post-processing (Time Series Database).
```
{
  "tags": {
    "client": string,            //MQTT Client name
    "device":"ACCC8Exxxxxx"      //Device serial number
  }
  "values": {
    "timestamp": number,         //EPOCH timestamp ms resolution
    "birth": number,             //When object was born
    "phase": number,             //0 = new object detected, 1 = object is tracked, 2 = object left scene (dead)
    "id": number,                //Unique tracking ID for each object being tracked
    "x": number,                 //Bounding box x,y,w,h
    "y": number,                 //Coordinate system is [0,0]-[1000,1000].  [0,0] is top left corner
    "w": number,
    "h": number,
    "cx": number,                //Center of gravity 
    "cy": number,         
    "dx": number,                //Total X distance traveled since birht -1000 - 1000
    "dy": number,                //Total Y distance traveled since birht -1000 - 1000
    "age": number,               //Age in seconds since birth
    "speed": number,             //Total distance in percent/per second
    "distance": number,          //Distance traveled in percent of view 
    "pause": number,             //The longest pause the object made while beining tracked
    "pauseX": number,            //Location of longest pause
    "pauseY": number,
    "pcx": number,               //Previous CX,CY.  Used for drawing path in live visualization
    "pcy": number,
    "bx":342,                    //Birt x,y,w,h,cx,cy
    "by":292,
    "bw":647,
    "bh":246,
    "bcx":665,
    "bcy":538
  }
}
```
