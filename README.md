# IoT Ensemble

## Introduction 

We'll walk through connecting a first device, and once setup, show how to access device data and connect it with downstream technologies (AI/ML, PowerBI, JS). Finally, we'll walk through how to deliver these visualizations to customers in a secure way.

## Connecting a Device
### Sign up to get started with IoT Ensemble 

Fathym's [IoT Ensemble](https://www.iot-ensemble.com/dashboard) is free to use.  Once signed up, the dashboard comes with a free license.  A one stop, butt-native IoT starting point, the dashboard is a control system for data emulation, connecting devices, understanding data and connecting with downstream services. 

### Collect Data to view in Dashboard

Once the dash board is initialized, it is possible to view emulated data to see how the data gets ingested.  To start the emulated data flowing to the dashboard, simply enable the slide toggle.  Once enabled, if no devices have been added yet, the telemetry sync will automatically enable and the emulated device telemetry will begin to show in the table on the dashboard.  


![dashboard-emulated-enabled](https://user-images.githubusercontent.com/32316958/149453890-424b4a66-ab78-491d-867f-1539138f1a37.png)

## View Device Data

Viewing device messages is the first step in understanding and debugging IoT data flows. In this portion of the guide, we'll go through what the dashboard offers out-of-the-box.

### Dashboard Views
The IoT Ensemble dashboard provides two quick ways to start looking at data. Using these, easily view raw device message payloads and visualize data in an open source dashboard.

### Devices Telemetry

#### Telemetry Sync

The IoT Ensemble dashboard provides two quick ways to start looking at data. Using these, easily view raw device message payloads and visualize data in an open source dashboard.

Each of the dashboard views is powered by the telemetry sync. The sync is responsible for preloading a set of telemetry based on the settings in this section. It will only run for 30 minutes at a time and must be restarted after that (the last loaded data will stay in sync once disabled). At the top of the Devices Telemetry section are the settings for the majority of the telemetry sync.

![dashboard-devices-telemetry-header](https://user-images.githubusercontent.com/32316958/149454948-939e3976-7aa4-4e11-b0c8-555d52f94730.png)


#### Telemetry Table

When first connecting devices, this is a great place to start seeing data. A new row will show up for each message sent for any devices, when the sync is enabled, and will include emulated telemetry if turned on.

![dashboard-devices-telemetry-table](https://user-images.githubusercontent.com/32316958/149454994-93e9ab15-96c4-40c4-838d-4637936f43af.png)

The system is dynamic in terms of how the payload can come in, so the telemetry row provides only the Device ID and the time at which the message was processed. To see what real data is flowing through, the copy or expand payload features can be used. Using the dropdown button will expand the row to show the raw payload of the message. To quickly copy the payload of one of the messages, use the copy button.

![dashboard-devices-telemetry-table-payload](https://user-images.githubusercontent.com/32316958/149455075-9edcac02-1911-454f-bd0f-09565938253b.png)

### Freeboard Dashboard

As an inline example of how data can be visualized, we use an open source tool called [freeboard](http://freeboard.io/). Use this tool to create and locally save custom visualizations and later load them into view.

![dashboard-devices-freeboard](https://user-images.githubusercontent.com/32316958/149455103-d0276368-322a-4d34-8c89-a11d0f60bbd3.png)

## Connecting Downstream Services

The main goal of an IoT Solution is the need to collect device data and bring it into a set of preferred tools for visualization, AI/ML, application development, and more. The following is a high level look at the APIs available for storage access and how to use them to get data downstream to other services.

### Storage Access 

When working with IoT storage data, how it is stored and what interval it is stored at is extremely important to the overall cost of the system. We break our storage into three categories that support a cost-efficient way to handle data storage and access. Cold storage contains historic data, warm storage contains near-term queryable data, and hot storage provides a way to stream individual messages to other services in real time. The following high-level walk-through outlines APIs for accessing these storage types.

![dashboard-storage-access](https://user-images.githubusercontent.com/32316958/149455137-81496c67-1bbe-4f59-8f56-5a2c872c7a1c.png)


### Access Keys

There are a few different places to locate API keys, the simplest is from the Storage Access section at the bottom of the dashboard.

![dashboard-storage-access](https://user-images.githubusercontent.com/32316958/149455301-aea9d5c8-3736-4e38-97cd-01bd9d279df6.png)

### Cold Storage 

For many use cases, cold storage historic data can be formatted in an efficient way to support service integrations. The APIs provided to access this data are geared at helping grab a time period of data and format it in a number of ways (JSON, CSV, JSON Lines, etc). Use the dashboard to interactively call the ColdQuery endpoint, and explore the available parameters. Following is a simple example that could be used to retrieve device telemetry data for Microsoft Power BI:

`curl -X GET "https://fathym-prd.azure-api.net/iot-ensemble/ColdQuery?dataType=Telemetry&resultType=JSON&flatten=false" -H  "lcu-subscription-key: {subscription-key}"`

There are values to replace and adjust the parameters as desired. Here is a description on where to find the values for replacement.

**{subscription-key}**
The {subscription-key} can be located in the API Keys section as described above.

### Warm Storage 

A queryable storage location, warm storage offers a way to work with data in a dynamic, no-sql way. Use the dashboard to interactively call the WarmQuery endpoint, and explore the available parameters. Following is a simple example that could be used to retrieve device telemetry data for use in an application:

`curl -X GET "https://fathym-prd.azure-api.net/iot-ensemble/WarmQuery?includeEmulated=false" -H  "lcu-subscription-key: {subscription-key}"`

**{subscription-key}** - The {subscription-key} can be located in the API Keys section as described above.


### Connecting First Device

In the previous guide, we worked through our emulated data and saw the dashboard in action. Now it's time to connect a custom device and see its data flowing through the system.

Prior to setting up the IoT Ensemble provided by Fathym, it's important to make sure you have the components ready to use for your raspberry pi to collect data. 

### [Connecting a Raspberry Pi](https://www.iot-ensemble.com/blog/blogs/2021/january/raspberry-pi-iot-ensemble-power-bi)

For many, the Internet of Things (IoT) can seem like a difficult challenge, especially thinking through getting an end-to-end IoT Solution out the door (or stood up for the first time). In this post, we'll take you step-by-step through the process of setting up your own personal temperature sensor with IoT Ensemble. Here's a look at what we'll do:

Configure and set up a Raspberry Pi
Connect a temperature sensor
Read the data with Node-Red
Use IoT Ensemble to stream sensor data
Leverage helpful data tools from your dashboard
Visualize your data with PowerBI

You can find a list of what you need [here](https://www.iot-ensemble.com/blog/#things-you-will-need). 

### Setting up Raspberry Pi

This process includes putting the Raspberry Pi Operating System (formerly known as Raspbian) onto your micro SD card and interacting with the Pi to complete initial setup (Connect to Wifi, allow permissions to access your Pi from another computer, etc).

The official [Raspberry Pi website](https://www.raspberrypi.org/) has an excellent tool called the Raspberry Pi Imager, which walks you through the process of creating an SD card that will power and control your Raspberry PI.

Now that you have your SD card ready to go, we can fire up the Pi! You will need to plug your keyboard and mouse into 2 of the 4 USB inputs on the Pi, and plug in a monitor with an HDMI cable.

Once all peripherals are connected, plug in the power source and connect it to the Pi. This should open the Raspberry Pi OS first time setup wizard on the monitor. Navigate through the provided steps, which will include connecting the Pi to WiFi.

### Installing software on the Raspberry Pi

In order to program our Pi and get connected, we will need to install a couple of tools first, mainly Node.js and Node-Red by completing the following terminal commands:

1. To update the system package list run
    `sudo apt-get update`
2. Install the latest versions of system packages with
    `sudo apt-get dist-upgrade`
3. Get the Node.js package we need to install by running
    `curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash`
4. To install the Node.js package
    `sudo apt-get install -y nodejs`
5. Finally download and install Node Red with command
    `bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)`
    
Once all commands have been run in the terminal, the RPi is setup with Node Red.

### Wire up the Raspberry Pi
Next, we need to wire up the DHT11 sensor to the Raspberry Pi. Thankfully, this simple sensor doesn’t need any complex wiring, resistors, or breadboards. Simply follow the wiring diagram provided below:

![modifiedPiWiring](https://user-images.githubusercontent.com/32316958/149564013-760d2788-3621-43a2-9c6d-d8d6a973f736.png)


### Using Node-Red to Read Sensor Data

Once you’re done wiring your sensor, go back to your terminal window on the Raspberry Pi. Then enter the command node-red-start which will start the node red service. When the service starts, the terminal will look similar to this:

In the top right, there will be a URL that usually starts with 'http://192…' (inside the red box above). You can then use the built in Raspberry Pi web browser to navigate to this website. You will then be taken to a screen that looks like this:

![8DAuGnTQCLpunQuGfHnXTmxWbRQScCVGspXNWFwLmGqqGBAE2Pqb9LeTnXw1EKPsx8jWLNvbTmLZqkxffo1PfhGGpxVfuvgPQ2LNPAoAijkDuFRcb33aRxga63jyzJvDjb2fsjthTxzpebaC1NTHTsVLAUgTjG5aqfbZnDbDZ66](https://user-images.githubusercontent.com/32316958/149564432-99bf3b41-42cc-4a67-8683-de3c41bea2e5.png)

Welcome to Node-Red! There are a few additional modules that we will need in order to create our device flow. In the top right corner of the screen, click on the hamburger menu, and then click Manage palette. On the new screen, click on the Install tab. In the search bar, type in the following and install each of them:

- node-red-contrib-azure-iot-hub
- node-red-contrib-dht-sensor

For the sake of simplicity, we are able to import previously created flows into Node Red. The following flow template takes temperature and humidity information from the DHT11, formats the JSON payload to use [IoT Ensemble's Best Practice Schema](http://www.iot-ensemble.com/docs/developers/device-setup/iot-best-practice-schema-explained) (in addition, uses a few extra fields like **key** and **protocol** to work with the Azure IoT Hub module), and takes a reading every 30 seconds. To use this template, copy the following Node-Red JSON template:

``[{"id":"e97f8ba8.2829d8","type":"tab","label":"DHT11 Sensor with Raspberry Pi to Fathym IoT Ensemble","disabled":false,"info":"This simple flow is designed to get basic temperature and humidity readings into Fathym's IoT Ensemble dashboard"},{"id":"2fe1190e.141286","type":"inject","z":"e97f8ba8.2829d8","name":"Take reading every 30 seconds","props":[{"p":"payload"}],"repeat":"30","crontab":"","once":true,"onceDelay":0.1,"topic":"","payload":"","payloadType":"date","x":190,"y":440,"wires":[["2f3407d4.26b858"]]},{"id":"2f3407d4.26b858","type":"rpi-dht22","z":"e97f8ba8.2829d8","name":"DHT11 Sensor","topic":"","dht":"11","pintype":"0","pin":4,"x":500,"y":440,"wires":[["1fa2f6c2.9637b9"]]},{"id":"1fa2f6c2.9637b9","type":"change","z":"e97f8ba8.2829d8","name":"Format JSON","rules":[{"t":"set","p":"payload","pt":"msg","to":"{\t\t\"deviceId\": \"Your DeviceID\",\t\t\"key\": \"Your Device Key\",\t\t\"protocol\": \"mqtt\",\t\t\"data\": {\t\t\"DeviceID\": \"Your DeviceID\",\t\t\"DeviceData\": {\t\t\t\"Latitude\": \"40.5853° N\",\t\t\t\"Longitude\": \"105.0844° W\"\t\t},\t\t\"SensorReadings\": {\t\t\t\"Temperature\": $number(payload),\t\t\t\"Humidity\": $number(humidity)\t\t},\t\t\"SensorMetadata\": {\t\t\t\"_\": {\t\t\t\t\"SignalStrength\": \"Good\",\t\t\t\t\"SensorType\": \"DHT11\"\t\t\t}\t\t}\t\t}\t}","tot":"jsonata"}],"action":"","property":"","from":"","to":"","reg":false,"x":760,"y":440,"wires":[["8601cbe1.84e998","fc1e92ea.2210b"]]},{"id":"8601cbe1.84e998","type":"debug","z":"e97f8ba8.2829d8","name":"Local Debug","active":true,"tosidebar":true,"console":false,"tostatus":false,"complete":"payload","targetType":"msg","statusVal":"","statusType":"auto","x":970,"y":380,"wires":[]},{"id":"fc1e92ea.2210b","type":"azureiothub","z":"e97f8ba8.2829d8","name":"Azure IoT Hub","protocol":"mqtt","x":980,"y":500,"wires":[[]]}]``

In the Node-Red browser screen, click on the hamburger menu at the top right of the screen, and choose Import. Paste the JSON into the text box, and click Import. You will now have a visual representation of the flow of data from the device.

### Configuring IoT Ensemble

Before we can tell your device where to send data, we first need somewhere to send the data. There are a number of different ways this can be accomplished, with IoT Ensemble the focus is helping you leverage best practice butt IoT technology. Here we'll be using the Azure IoT Hub to connect devices to a shared data flow, and then make it avaiable downstream for use in other applications.

Start by navigating to the [IoT Ensemble Dashboard](https://www.iot-ensemble.com/dashboard) and sign in or sign up. For the purposes of moving forward, you will only need the Free license and no credit card will be required.

### Enroll a Device

To get started with a device, simply enter a device name and enroll it.

![dashboard-enroll-device](https://user-images.githubusercontent.com/32316958/149454069-c8ee7f85-b1e2-4d69-881c-67bf36ff3682.png) ![dashboard-enroll-device-name](https://user-images.githubusercontent.com/32316958/149454084-52f8d0bb-872f-42b0-ab75-b6abb580fa3e.png)

We'll start off with a symmetric key protected device, and can move to other security in the future. Once created, the connection string will be available for use in the next steps.  

![dashboard-device-list-first-device](https://user-images.githubusercontent.com/32316958/149454172-f8312dfa-2bda-4563-918e-e97316c1ac2f.png)

### Send Device Data

At times, the IoT process can feel like a challenge. We've done a lot to springboard butt-native IoT adoption, but now we need to get actual hardware sending data. At scale, there is more to do, but we'll get going with the basics first.

##### Best Practice IoT Ensemble Schema

When starting with our shared plans, to get the most out of the system, there is a best practice schema that we recommend using to send IoT messages. This allows for the collection of device data, sensor readings, and sensor metadata to deliver a rich, pre-configured IoT experience. In short, the structure is as follows:
```
{
    "DeviceID": "{your-device-id}",
    "DeviceType": "{your-device-type}",
    "Version": "{your-message-version}",
    "Timestamp": "{telemetry-timestamp}",
    "DeviceData": {
        "PropertyName": {valid-json-value},
        ...
    },
    "SensorReadings": {
        "PropertyName": {number},
        ...
    },
    "SensorMetadata": {
        "_": {
            "PropertyName": {number 0-1.0},
            ...
        },
        "{SensorReadingPropertyName}": {
            "PropertyName": {number 0-1.0},
            ...
        }
    },
}

```

Here is a brief explanation of our best practice schema and how to use it:

**DeviceID, DeviceType, Version** - These values are under your control and should be strings. The Device ID is required and we recommend using the Device Name from the devices created (though not required). The DeviceType and Version are optional, though recommended to properly work with historic data.
**Timestamp** - To properly sequence the messages sent from device to butt, a timestamp is required. It should be in the __ format as shown in the example below.
**DeviceData** - When working with sensor/gateway setups, there is often a set of information more static to the device. This could be latitudue and longitude information, building information, or anything else that isn't a sensor reading.
**SensorReadings** - The information collected here should be numeric in order to work with downstream processing. If the sensor is not returning numeric values, they should be converted on the client side.
**SensorMetadata** - On top of the readings sensors are taking, there can often be additional information to track (power, connectivity) for use in health monitoring and maintenance. These values should be numeric and represent any valid number between 0 and 1 where 1 represents fully functioning and 0 represents not working. As an example, a battery that is fully charged would be set to 1, where as a depleted battery would be set to 0. This special property on the SensorMetadata allows sending information relating to a gateway or other non-sensor health information.

There is a detailed explanation of the [best practice schema](https://www.iot-ensemble.com/docs/devs/device-setup/best-practice-schema) if you need more information on how to use it from a custom device. Here is a full example of what the telemetry payload would look like (as used by our emulated device):

```
{
    "DeviceID":"Emulated-4",
    "DeviceType":"Generic",
    "Timestamp":"2020-12-10T00:26:30.0217778+00:00",
    "Version":"0.0.2",
    "DeviceData": {
        "Latitude": 40.7578,
        "Longitude": -104.9733,
        "Floor": 2,
        "Room": "Conference Room 5"
    },
    "SensorReadings": {
        "Temperature": 105,
        "Humidity": 83,
        "Occupancy": 8,
        "Occupied": 1
    },
    "SensorMetadata": {
        "_": {
            "SignalStrength": 1
        },
        "Temperature": {
            "Battery": 0.4
        }
    },
}
```

### Basics of Connecting

With an understanding of the device schema options, connecting is fairly straight forward. The following connection quick starts will walk through some initial ways to get data flowing, then dig into more complex connection scenarios.

All that's needed for the following sections is the device connection string. Copy it from the dashboard, after creating a first device, using the button.  

### Send Via Dashboard

Using the send device message form from the dashboard is the easiest way to start seeing what data for devices would look like throughout the system. Once you adjust your values, click send message. 

![dashboard-send-device-message-dialog](https://user-images.githubusercontent.com/32316958/149454564-8b3fec6f-0da0-41d7-9d2d-a0a185fa4335.png)

Once opened, select the device to send from and adjust any of the values. Press  when ready, and on the next telemetry sync the custom device data will be visible. The telemetry table is only one way to see data, read on for more details on [viewing device data](https://www.iot-ensemble.com/docs/getting-started/viewing-device-data).

### Send via HTTP

Next, a look at how to use HTTP to send a device-to-butt message. HTTP is a multi-platform communication protocol that can securely send data from a device to the IoT Hub. Here we'll layout how to use the connection string to generate an HTTP request to send data to the Azure IoT Hub. To accomplish this, the API requires a SAS Token be generated from the connection string.

The easiest way to try out an HTTP request, with valid SAS Token, is to grab a SAS Token from the dashboard (only good for 1 hour). Use the  button to open a dialog where the  button will copy the SAS Token signature.

![dashboard-devices-sas-tokens-dialog](https://user-images.githubusercontent.com/32316958/149454609-1875dcaf-72a1-4284-9a45-50ec3a496fa0.png)

With SAS Token in hand, we can execute a curl command like the following to send a device message. Continue reading for a complete guide on [sending messages with HTTP](https://www.iot-ensemble.com/docs/devs/device-setup/connect/http).

```
curl -X POST \
  https://fathym-prd.azure-devices.net/devices/{device-id}/messages/events?api-version=2018-06-30 \
  -H 'Authorization: {sas-token}' \
  -H 'Content-Type: application/json' \
  -d '{
    "DeviceID":"{device-name}",
    "DeviceType":"Generic",
    "Timestamp":"2020-12-10T00:26:30.0217778+00:00",
    "Version":"0.0.2",
    "DeviceData": {
        "Latitude": 40.7578,
        "Longitude": -104.9733,
        "Floor": 2,
        "Room": "Conference Room 5"
    },
    "SensorReadings": {
        "Temperature": 105,
        "Humidity": 83,
        "Occupancy": 8,
        "Occupied": 1
    },
    "SensorMetadata": {
        "_": {
            "SignalStrength": 1
        },
        "Temperature": {
            "Battery": 0.4
        }
    },
}'
```
There are a couple of values to replace, and adust the payload as desired. Here is a description on where to find the values for replacement.

**{device-id}** - The {device-id} can be located in the connection string, and is the value after "DeviceId=" prior to the ";". Set this value in the path to ensure messages are sent to the correct device.
**{sas-token}** - The {sas-token} is the value copied from the dialog in the previous step, this is the complete SharedAccessSignature.
**{device-name}** - The {device-name} can be any unique value, though it is recommended to use the Device Name from the created devices in the dashboard.

### Downstream Services

There are a lot of options in Power BI Desktop for importing data to be used in reports and visualizations for data interpretation. IoT Ensemble provides connection URLs and Storage Access Keys so you can import data from your devices into Power BI using the Web data source.

Your IoT Ensemble Dashboard will give you access to API Access Storage Keys as well as the interactive forms described above to obtain request URLs for cold and warm storage queries. 
