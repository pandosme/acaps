# Publisher
ACAP that can publish data from Analytics ACAP directly to an Influx Database or a HTTP Server.

# Overview
Integeating data from one service to another can be done in different ways.  Publisher simplifies getting data into Influx
(a time-series database).  This provides simplification for use-cases such as logging, counting and forensic search.


# Changle log
April 13,2020 Version 1.0.0
- First version

# Targets
![home](pictures/target.PNG)

### Target Type
Select Influx or HTTP depending on what server you may have.  MQTT is not yet implemented.

### Address
Set IP address or FQDN and port number.

Examples
```
  web.server.com
  influx.server.com:8086
  10.11.12.13:50000
```
### Database
Set the name of the database (only applicable for Influx).  Note that you need to create the database first.  Setting up an Influx server is easy with the [Influx Docker](https://hub.docker.com/_/influxdb).

# Data
![home](pictures/data.PNG)

### Device ID
For Influx this will create a tag
```
device=theName
```
For HTTP this will create a property in the POST payload
```
{ 
  "device": "theName",
  ...
```

## Data Producers
Current supported data producers

### AXIS License Plate Verifier (ALPV)
Publish the license plate captured by ALPV
Influx
```
URL: http://address/write?db=myDatabase&precision=ms
BODY: myTopic,device=camera1 plate="ABC123" 1586794095057
```
HTTP
```
URL: http://address
BODY: {
	"topic": "myTopic",
	"device": "camera1"
	"plate": "ABC123",
	"timestamp":1586794095057
}

```

## AXIS Direction Detector (Direction)
Capture when people are coning in ot leaving.  

Influx
Querying the sum of the value over a period of time will give occupancy.
```
URL: http://address/write?db=myDatabase&precision=ms
BODY In: myTopic,device=camera1,direction=in value=1 1586793127914
BODY Out: myTopic,device=camera1,direction=out value=-1 1586793127914
```
HTTP
```
URL: http://address
BODY: {
	"topic": "myTopic",
	"device": "camera1"
	"direction": "in" | "out",
	"value": 1 | -1
	"timestamp":1586794095057
}

```

### AXIS Video Motion Detection (VMD)
Messages will only be sent on motion start as the primary use-case is logging, not controling actions.

Influx
```
URL: http://address/write?db=myDatabase&precision=ms
BODY: myTopic,device=camera1 value=1 1586793127914
```
HTTP
```
URL: http://address
BODY: {
	"topic": "myTopic",
	"device": "camera1"
	"value": 1
	"timestamp":1586794095057
}
```

### Topic
For Influx the is the name of the Influx measurement that data will be stored.
For HTTP this will be added as a property

### User Tags
Sometime it is needed to add additional tags that are not part of the data producer payload.  Note that you may not use an space in key or value.

Examples
```
location=New-York
location=New-York,building=A
```
For Influx the names will be added a tags.
For HTTP the names will be added as properties in JSON payload.

# Security
![home](pictures/security.PNG)

### HTTPS/TLS
If the server requires HTTPS, set valur other than "No".  This will append "https://" to the address.
If the server has a self-signed or private CA certificate, select "Accept untrusted certificate".
If the server has a certificate signed by a public CA (e.g. LetsEnrypt), select "Validate certificate"

### Autnentication
* None - No authentication will be done regardless if user/password is set
* Basic -  Influx supports basic
* Digest (encrypted passwords) - Many web servers supprts digest authentication.
* Beare/Token.  Set you token in the password field.  This will append HTTP header "Authorization: Bearer myToken"

