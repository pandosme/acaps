# OVERLAY

Easily add a dynamic text overlay in video that can easily updated using HTTP (GET) or by MQTT message.

![overlay](https://files.juhlin.me/image/KTEOFBZUHZ)

## [Download](https://files.juhlin.me/acap/overlay)
*Note that Overlay is only supported for cameras based on ARTPEC-7 platform*

## Configuration

![config](https://files.juhlin.me/image/ASUDNGPJBZ)

Define the text overlay to your liking.  You can use the "Test text" to set a string while configuring.
* Placement
* Size (width & height)
* Background color
* Text color
* Transperancy

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


