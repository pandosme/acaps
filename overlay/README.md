# OVERLAY

Easily add a dynamic text overlay in video that can easily updated using HTTP (GET) or by MQTT message.  The standard camera overlay will not be affected.

![overlay](https://files.juhlin.me/image/KTEOFBZUHZ)

# [Download (ZIP)](https://api.aintegration.team/acap/overlay?source=github)
Unzip the file and install the eap-file on the camera.

*Note that Overlay is only supported for cameras based on ARTPEC-7 and ARTPEC-8 platform*

## Configuration

![config](https://files.juhlin.me/image/ASUDNGPJBZ)

Define the text overlay.  You can use the "Test text" while configuring.

Clear time will automatically clear the text after X amount of time.  Y

## HTTP
If you do not have MQTT clients you can use HTTP to update the text.  
```
http://address/local/xoverlay/update?text=Hello%20World
```
You can copy the HTTP url bly clicking "Get HTTP link" and paste that into your HTTP client.

## MQTT
![config](https://files.juhlin.me/image/WRJPTQLKNQ)

Connect to the broker.  Once connected you will see (or change) the topic the MQTT clients can publish a text string to.  By default the subscription includes the device serial number.  Change the topic to a generic topic if you have many cameras that should have the same text overlay.


