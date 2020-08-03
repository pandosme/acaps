# Daybreak Me
ACAP for Axis Cameras that generates  events on dawn, sunrise, sun noon, sunset, dawn and midnight. 

## Download
- [MIPS](https://github.com/pandosme/acaps/raw/master/daybreakme/files/Daybreak_Me_2_4_0__mips.eap)
- [ARMv7hf](https://github.com/pandosme/acaps/raw/master/daybreakme/files/Daybreak_Me_2_4_0__armv7hf.eap)
- [AARCH64](https://github.com/pandosme/acaps/raw/master/daybreakme/files/Daybreak_Me_2_4_0__aarch64.eap)


# Settings

![home](pictures/home.png)

## MAP
Move the marker to the place of the camera.






r (Birth Area), how old they need to be and how often objects are published. 

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
