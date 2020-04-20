## AXIS License Plate Verifier
Publish the captured license plate

Influx
```
URL: http://address/write?db=myDatabase&precision=ms
BODY: myTopic,device=ACCCxxxxx plate="ABC123" 1586794095057
```
MQTT & HTTP
```
{
  "topic": "myTopic",
  "device": "ACCCxxxxx",
  "name": "Some Name"
  "plate": "ABC123",
  "image": null || base64,
  "localTime": "2020-01-01 12:23:34",
  "clock": Seconds from midnight
  "timestamp":1586794095057
}
```

## AXIS Direction Detector

Influx

```
URL: http://address/write?db=myDatabase&precision=ms
BODY In: myTopic,device=camera1,direction=in value=1 1586793127914
BODY Out: myTopic,device=camera1,direction=out value=-1 1586793127914
```

MQTT & HTTP
```
{
  "topic": "myTopic",
  "device": "ACCCxxxxx",
  "name": "Some Name",
  "direction": "in" | "out",
  "value": 1 | -1
  "image": null || base64,
  "localTime": "2020-01-01 12:23:34",
  "clock": Seconds from midnight,
  "timestamp":1586794095057
}

```

## AXIS Video Motion Detection

Influx
```
URL: http://address/write?db=myDatabase&precision=ms
BODY: myTopic,device=camera1 value=1 1586793127914
```
MQTT & HTTP
```
{
  "topic": "myTopic",
  "device": "ACCCxxxxx",
  "name": "Some Name",
  "value": 1
  "timestamp":1586794095057
}
```
