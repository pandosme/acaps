# xMotion
A camera MQTT client ACAP that publish motion-based analytics data that can be used for a number of different use cases.  Motion detection is a common use case but xMotion is mainly targeting path/flows monitoring, automation, counting and forensic search.  Systems can select different types of payloads depending on use case.  xMotion can run on both cameras and radar.

![overlay](https://files.juhlin.me/image/YWFQGVMLNS)

## [Download xMotion 1](https://files.juhlin.me/acap/xmotion1)
Use xMotion 1 for cameras and radar products that does not required object classification

## [Download xMotion 2](https://files.juhlin.me/acap/xmotion2)
xMotion 2 will include object classification (depending on camera).  Radar products not supported. 

Unzip files and install the eap-file corresponding to your device

*It is recommeded to use device firmware 10.8.x or later for better perfomance*

## Messages view
This page is designed for validation and not as a user client.  The video played is medium size resolution with 5 fps playback.  In order to get detections, trackers and paths to be displayed, the MQTT broker must support connectiion using WebSocket.  Green dots shows where objects are born and red where they died.

At the bottom users can add a name (typicall system id of camera) and group (system grouping) that will be added to every payload.  To suppress short sporadic detections it is possible to set minimum distance an object needs to pass.

For paths it is possible to get an image capture when the object passed the minimum limit.  Images are typically used for validation and forensic search.  Note that payloads will be big.

## Detection
Detection messages are bounding boxes of detected objects.  Bounding boxes is great for real-time visualization but generates a lot of data and hard to consume and process for other use cases.  The same data is part of ONVIF Profile M (XML data over RTP) and targets ONVIF clients.  xMotion targets IT integration and provides the same data in a consumer-friendly structure, standard coordinate system with the ability to filter on area-of-interest, limiting the strain for consuming services.

Messages are published up to 5/s and include all the detected objects in that frame.

### xmotion/detection/DEVICE
*xMotion2:  Classification is not included in detection payload*
```
{
  "device":"ACCC8EXXXXXX",
  "timestamp":1634757165727,
  "detections":[
    {"id":7901,"x":536,"y":270,"w":147,"h":158,"cx":609,"cy":428}
  ]
}
```
- device: \[String] The serial number of the device
- timestamp: \[Number] EPOCH (UNIX) time since January 1 1970 in milli-second resolution
- detections: \[Array] Detected objects (see coordinate system).  If the array is empty, all detection ID are lost.  An empty array will only be published when no objects are detected (all previous object id are lost/dead).
- id: \[Number] Unique tracker id
- x,y,w,h: \[Number] See coordinate system
- cx,cy: \[Number] Center-of-gravity.  Can be bottom-center, middle-center or top-left depending on settings

When running on a Radar device an additional "radar" property will be added
```
"radar": {
  "speed":13.1,
  "direction":313,
  "distance":36,
  "angle":-26.1,
  "type":4
 }
```
- speed: Object speed in meter/second
- direction:  Object direction angle in degrees -180 to 180 where 0 is direction towards the radar
- distance:  Distance in meter between object and radar
- angle: The location angle of the object related to the radar direction (-180 to 180)
- type:  Object classification. 2 = Undefined, 3 = Human, 4 = Vehicle.


## Tracker
Trackers are based on the detections but only published when objects has moved 5% from the past publish. The bandwidth compared to detections is substantial lower and trackers are much easier for services to build use cases around.  Trackers are perfect for real-time processing services such as triggering events, recording controller or system automation.

Trackers includes object id, x, y, width, height, delta x/y movement, distance and age.  Objects needs to pass the area-of-interest before they are tracked.  The distance and age  properties are easy and power filters a subscriber can apply.  Be cautions of using width and height as filters as object size tends to very when objects moves across the scene.  Note that tracker id may be lost while it is moving in the scene and may reappear with a new id.  This depends on various challenges in the scene such as light conditions, weather, size variations, obstructing objects, reflections, and other moving objects.

### xmotion/tracker/DEVICE
```
{
  "device":"ACCC8EXXXXXX",
  "timestamp":1634756482392,
  "id":7966,
  "cx":975,
  "cy":645,
  "x":953,
  "y":557,
  "w":45,
  "h":88,
  "distance":54.1,
  "age":1,
  "dx":446,
  "dy":276,
  "class": "Car",
  "dead":false
}
```
- device: \[String] The serial number of the device
- timestamp: \[Number] EPOCH (UNIX) time since January 1 1970 in milli scond resolution
- id: \[Number] Unique tracker id
- cx,cy: \[Number] Center-of-gravity.  Can be bottom-center, middle-center or top-left depending on settings
- x,y,w,h: \[Number] See coordinate system
- distance: \[Number] The distance in % of view.  May be more than 100% if objects moves back/forth in scene
- age: \[Number] Age in seconds since birth
- dx: \[Number] Delta X movement from birth (See coordinate system). A positive = moving right and negative = moving left.
- dy: \[Number] Delta Y movement from birth (See coordinate system). A positive = moving down and negative = moving up.
- class: \[String] xMotion2 provides classification of Person, Car, Truck, Bus, Vehicle, Bike, Motorcycle (depending on camera model)
- dead: \[Bool] False means the object is being tracked.  True means the object is lost and the ID will not be published any more.

When running on a Radar device an additional "radar" property will be added
```
"radar": {
  "speed": 10.3,
  "direction":313,
  "distance":36,
  "angle":-26.1,
  "type":4,
  "topSpeed":13.1
 }
```
- speed: Object speed in meter/second
- direction:  Object direction angle in degrees -180 to 180 where 0 is direction towards the radar
- distance:  Distance in meter between object and radar
- angle: The location angle of the object related to the radar direction (-180 to 180)
- type:  Object classification. 2 = Undefined, 3 = Human, 4 = Vehicle.
- topSpeed: The object max speed (meter/second) during tracking

## Path
Path are based on trackers and published when an object left the scene (or tracker id is lost).  The bandwidth utilization compared to detection and trackers is very limited.  Paths are perfect for post-processing system and is typically stored in a database that can be queried for counting, flow analysis and forensic search.  A small/medium size image capture can be included if the use case requires image visualization/validation.

### xmotion/path/DEVICE
```
{
  "device":"ACCC8EXXXXXX",
  "id":423,
  "timestamp":1635028199165,
  "death":1635028203972,
  "distance":27.8,
  "age":4.8,
  "class": "Bus",  
  "path":[{"cx":200,"cy":304,"x":156,"y":219,"w":44,"h":85},...],
  "image":{
    "device":"ACCC8EXXXXXX",
    "id":423,
    "resolution":"320x180",
    "jpeg":"/9j/4AAQSkZJRgABAgAAAQAB..."
  }
}
```
- device: \[String] The serial number of the device
- id: \[Number] Unique tracker id
- timestamp: \[Number] Birth time in EPOCH (UNIX)
- death: \[Number] Death time in EPOCH (UNIX)
- distance: \[Number] The distance covered in % of view.  May be more that 100% if objects move back/forth
- class: \[String] xMotion2 provides classification of Person, Car, Truck, Bus, Vehicle, Bike, Motorcycle (depending on camera model)
- age: \[Number] In seconds (death-birth)
- path: \[Array] Object path in 5% increments (see coordinate system)
- image: \[Null or Object] Depends on configuration.  JPEG are Base64 encoded 


## Coordinate system
xMotion use a relative coordinate system from [0,0] to [1000,1000].  Origin is in the top left corner.

## Filter
To optimize the system performance, it may be necessary to filter detections.  This reduces both payload and processing required by the consumer.  It is the objects cx and cy that is checked to area of intrest. Note that cx,cy may be represented as bottom-center, middle-center or top-left depending of the object depending on settings. Default is bottom-center (feet) of an object.

### Set detection area
Use the mouse to mark the area where objects will be detected.  Path and tracker will continue tracking objects outside this area.

### Set minimum size
Use minimum size to suppress small sporadic objects. Once tracking started, tracker and path will continue to track objects once they have met the size limits.  Be cautions with size filter as object sizes will vary in scene.  

### Set ignore area
Use this are if there are parts of the detection area where they may be disturbances such as swaying flags/trees or light reflections.

