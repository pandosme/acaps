# Publisher 1.3-0
An ACAP that can publish data from Analytics ACAP to MQTT, Influx Database or a HTTP Server with simple and usable payloads.

# Overview
Integerating data from one service to another can be done in different ways.  Publisher simplifies getting analytics data to Influx,
a time-series database.  This provides simplification for use-cases such as logging, counting, data analysis and forensic search.

# Requirements
1. An Axis Camera
2. Select, download and install the file (mips.eap or armv7hf.eap) depending on your camera.
3. Any of the supported analytics intalled and running (see Data Producers)
4. An Influx server or HTTP server that cameras can access.


# Configuration

![home](pictures/target.PNG)

## Target Type
Select MQTT, Influx or HTTP depending on what server you may have.

## Address
Set IP address or FQDN and port number.

Examples
```
  mqtt.server.com:1883"
  web.server.com/my/end/point
  influx.server.com:8086
```
## Database
Set the name of the database (only applicable for Influx).  Note that you need to create the database first.  Setting up an Influx server is easy with the [Influx Docker](https://hub.docker.com/_/influxdb).



![home](pictures/data.PNG)

## Device Name
Publish property/tag "name"

## Data Producers
* AXIS License Plate Verifier
* AXIS Direction Detector
* Axis Motion Detection (VMD)

### Topic
For Influx the is the name of the Influx measurement that data will be stored.
For HTTP this will be added as a property

### User Tags
Sometimes it is needed to add additional tags that are not part of the data producer payload.
> Note that you may not use any spaces in the key or value field (if needed, use '-' or '_')

Examples
```
location=New-York
country=France,city=Paris,store=some-id
```
For Influx the names will be added a tags.
For HTTP the names will be added as properties in JSON payload.

### Image
Sometimes you want to store an image when detection occured.  Setting Image will append a JPEG image on published data.  Leave blank if you do not want an image.  The image will be base64 encoded.

> Note that images takes up a lot of storage space.  It is recommended to use a medium size resolution, typical 640x360 (16:9), 640x480 (4:3) or 640x640 (1:1) depending on the camera aspect ration.

Image syntax
```
resolution=640x360
```
Influx: The image will be stored on Influx with value name "image".
HTTP: The image will have JSON property name "image".

![home](pictures/security.PNG)

## HTTPS/TLS
If the server requires HTTPS, set value other than "No".  This will append "https://" to the address.
If the server has a self-signed or private CA certificate, select "Accept untrusted certificate".
If the server has a certificate signed by a public CA (e.g. LetsEnrypt), select "Validate certificate"

## Authentication
* None - No authentication will be done regardless if user/password is set
* Basic -  Influx supports basic
* Digest (encrypted passwords) - Many web servers supprts digest authentication.
* Beare/Token.  Set you token in the password field.  This will append HTTP header "Authorization: Bearer myToken"
