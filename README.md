# RaspberryPi-IoT
Setting up a Raspberry Pi 3 B with Azure IoT

Following the instructions laid out at  [Connect Raspberry Pi to Azure IoT Hub (Node.js)](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started)

The first time, I used an existing Raspbian install that I had previosuly used and I got the following error:

```text
Unable to determine hardware version. I see: Hardware : BCM2835
,

expecting BCM2708 or BCM2709. Please report this to projects@drogon.net
```

I did some googling and re-read the instructions and saw the note:

```text
Please use above link to download raspbian-2017-07-5 zip image. The latest version of Raspbian 
images has some known issues with Wiring-Pi Node, which might cause failure in your next steps.
```

So I started again from scratch with the raspbian-2017-07-5 image, but this made no difference :(

I noticed that running

```text
gpio -v
````

also gave the same error, and following these steps I managed to upgrade WiringPi to the correct version.

