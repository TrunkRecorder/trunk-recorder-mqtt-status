# Trunk Recorder MQTT Status Plugin

This is a plugin for Trunk Recorder that publish the current status over MQTT. External programs can use the MQTT messages to display what is going on.

## Install

1. **Build and install the current version of Trunk Recorder** following these [instructions](https://github.com/robotastic/trunk-recorder/blob/master/docs/INSTALL-LINUX.md). Make sure you do a `sudo make install` at the end to install the Trunk Recorder binary and libaries systemwide. The plugin will be built against these libraries.

2. Now, **install the Paho MQTT C & C++ Libraries**. The full documentation for that is [here](https://github.com/eclipse/paho.mqtt.cpp#unix-and-linux)... but the basic commands are as follows:

*Install Paho MQTT C*
```bash
git clone https://github.com/eclipse/paho.mqtt.c.git
cd paho.mqtt.c
git checkout v1.3.8

cmake -Bbuild -H. -DPAHO_ENABLE_TESTING=OFF -DPAHO_BUILD_STATIC=ON  -DPAHO_WITH_SSL=ON -DPAHO_HIGH_PERFORMANCE=ON
sudo cmake --build build/ --target install
sudo ldconfig
```

*Install Paho MQTT C++*
```bash
git clone https://github.com/eclipse/paho.mqtt.cpp
cd paho.mqtt.cpp

cmake -Bbuild -H. -DPAHO_BUILD_STATIC=ON  -DPAHO_BUILD_DOCUMENTATION=TRUE -DPAHO_BUILD_SAMPLES=TRUE
sudo cmake --build build/ --target install
sudo ldconfig
```

3. Build and install the plugin:

```bash
mkdir build
cd build
cmake ..
sudo make install
```

## Configure

| Key       | Required | Default Value | Type   | Description                                                  |
| --------- | :------: | ------------- | ------ | ------------------------------------------------------------ |
| address   |    ✓     |               | string | IP address to send this audio stream to.  Use "127.0.0.1" to send to the same computer that trunk-recorder is running on. |
| port      |    ✓     |               | number | UDP or TCP port that this stream will send audio to. |
| TGID      |    ✓     |               | number | Audio from this Talkgroup ID will be sent on this stream.  Set to 0 to stream all recorded talkgroups. |
| sendTGID  |           |    false     | boolean | When set to true, the TGID will be prepended in long integer format (4 bytes, little endian) to the audio data each time a packet is sent. |
| shortName |          |              |string  | shortName of the System that audio should be streamed for.  This should match the shortName of a system that is defined in the main section of the config file.  When omitted, all Systems will be streamed to the address and port configured.  If TGIDs from Systems overlap, each system must be sent to a different port to prevent interleaved audio for talkgroups from different Systems with the same TGID.  
|  useTCP   |        |   false     |boolean | When set to true, TCP will be used instead of UDP.




/opt/homebrew/sbin/mosquitto -c /opt/homebrew/etc/mosquitto/mosquitto.conf

https://docs.microsoft.com/en-in/azure/iot-hub/iot-hub-mqtt-support

https://github.com/eclipse/paho.mqtt.c/issues/461#issuecomment-667559214

The user name must look like:
tr-hub.azure-devices.net/test/?api-version=2018-06-30

The password must be a shared access signature in this form (including SharedAccessSignature at the start of the password:
SharedAccessSignature sr=<your-hub-name>.azure-devices.net%2Fdevices%2F<your-device-name>&sig=<sig>%3D&se=<timestamp>


