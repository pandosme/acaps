# SIMQTT

An MQTT Client for Axis devices that simplifies monitoring events over MQTT. All common events are automatically published. Users may add additional properties in payload such as name, location and various time formats.


![config](https://files.juhlin.me/image/UYJMBDEHGD)

# [Download (ZIP)](https://api.aintegration.team/acap/simqtt?source=github)
Unzip the file and install the eap-file on the camera.

## Installation

Install SIMQTT for devices with firmware 10.x.x or later.  Install SIMQTT_Legacy for devices with firmware less  than 10.x.x. _Note that SIMQTT Legacy only supports MQTT connection over TCP and not TLS._

### MQTT Broker
Should be pretty stright forward.

### Additional payload properties
Name and Location will be included in every payload as "name" and "location" if they contain any user defined text string.
Select format for property "timestamp".  Either EPOCH (milli seconds since Jan 1 1970) is ISO (YYYY-MM-DDTHH:MM:SS+Zone-offset)

## Messages (Topics & Payload)
[List of topics and payload](https://github.com/pandosme/acaps/blob/master/simqtt/topics.md)
