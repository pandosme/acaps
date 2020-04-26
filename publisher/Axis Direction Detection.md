# AXIS Direction Detection

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
direction,name=Office,device=ACCC8Exxxxxx,direction=out value=-1,clock=36360,localTime="2020-04-26 10:06:00" 1587888358061"
```

## HTTP and MQTT payload example
```
{
  "tags":{
    "name":"Office",
    "device":"ACCC8Exxxxx",
    "direction":"in"
   },
   "values":{
     "value":1
     "image": null
   },
   "timestamp":1587888358061,
   "image":"JPEG base64 encoded" | null,
   "database":"someDatabase",
   "topic":"direction",
   "clock":36420,
   "localTime":"2020-04-26 10:07:00"
}
```

