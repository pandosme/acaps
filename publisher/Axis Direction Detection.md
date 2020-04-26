# AXIS Direction Detection
Publish the captured license plate

## Tags
device: "SERIAL NUMBER"
name: "Device Nice Name"
direction: "in" | "out"
userTags: [OPTIONAL]

## Values
value: 1 (in) or -1 (out)
image: null or a base64 encoded JPEG
clock: seconds since midnight
timestamp: epoch/Unix timestamp

## Influx payload example
```
someMeasurement,device=ACCCxxxxx,name=Camera1,direction=in value=1,image="null" 1587884000000
```

## HTTP and MQTT payload example
```
{
  "tags":{
    "name":"Camera1",
    "device":"ACCC8Exxxxx",
    "direction":"in"
   },
   "values":{
     "value":1
     "image": null
   },
   "timestamp":1587884000000,
   "image":"JPEG base64 encoded" | null,
   "database":"someDatabase",
   "topic":"direction",
   "clock":32250,
   "localTime":"2020-04-26 08:57:30"
}
```

