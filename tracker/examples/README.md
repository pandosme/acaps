# Node-Red examples
[Node-Red](https://nodered.org) is a simple and fantastic web-based tool to integrate anything with everything.  You do not need to be a software developer.  With a the node-Red dashborad you can easily build web applications and web services.  If you are not familiar with node-red, watch the video on their home page.

The following are some simple flow examples how to use Tracker for various tasks.

# MQTT Broker
It is assumed that you have a MQTT broker.  If not, you have a number of options:
- Install a local [Mosquitto](https://mosquitto.org/) MQTT broker on Windows, Linux, RasPi...
- Install a local [MQTT broker](https://flows.nodered.org/node/node-red-contrib-aedes) node in Node-Red.
- Setup a paid account on [CloudMQTT](https://www.cloudmqtt.com/), [IBM Blumix](https://cloud.ibm.com), or any other MQTT provers
- Use [HIVEMQ free public broker](https://www.hivemq.com/public-mqtt-broker) by connecting to address broker.hivemq.com:1883 (no user/password required).  Note that everyone else will be able to subscribe to what you publish.

## Basic motion filter
The following example collects tracker data, filters on objects going downwords with an age of at least 5 seconds.
![home](pictures/filter.png)

[Copy the flow](flows/filter.json) and import into your node red.

## Dashboard visualizations
Takes  snapshot of the camera and display bounding boxes and paths (in real-time) of objects passing the scene.

![home](pictures/visualize.png)

You need to install the following additional nodes into you Node-Red. Click the 3-line-icon top right and select Manage Pallet, click install and write
- [node-red-contrib-axis-camera](https://flows.nodered.org/node/node-red-contrib-axis-camera)
- [node-red-dashboard](https://flows.nodered.org/node/node-red-dashboard)

[Copy the flow](flows/visualization.json) and import into your node red.
