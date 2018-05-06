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

also gave the same error, and following [these steps](http://wiringpi.com/download-and-install/) (Plan A) I managed to upgrade WiringPi to the correct version:

Now, running

```text
gpio -v
````

gives me:

```text
gpio version: 2.46
Copyright (c) 2012-2018 Gordon Henderson
This is free software with ABSOLUTELY NO WARRANTY.
For details type: gpio -warranty

Raspberry Pi Details:
  Type: Pi 3, Revision: 02, Memory: 1024MB, Maker: Embest
  * Device tree is enabled.
  *--> Raspberry Pi 3 Model B Rev 1.2
  * This Raspberry Pi supports user-level GPIO access.
```

So now I know that the correct version of WiringPi is installed - all looking good so far... but calling

```
sudo node index.js '<YOUR AZURE IOT HUB DEVICE CONNECTION STRING>'
```

still gives me the error

```text
Unable to determine hardware version. I see: Hardware : BCM2835
,

expecting BCM2708 or BCM2709. Please report this to projects@drogon.net
```

So index.js is referencing the wrong version...

From [Pi4J fails with Rpi 4.9.35 kernel - Unable to determine hardware version from wiringpi lib #349](https://github.com/Pi4J/pi4j/issues/349) I understand that 

From [here](https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app/issues/15) I discovered a quick workaround - run

```text
npm install wiringpi-node
```

And now reference this from index.js

```text
cd
cd iot-hub-node-raspberrypi-client-app
nano index.js
```

find where it says require('wiring-pi') and replace with require('wiringpi-node').
If you're not familiar with nano, fear not ... to save the change, type Ctrl-O and press Enter, then Ctrl-X to close the editor

Now when I run it...
...it works!!!

What I want to know is why can't these things ever just work out of the box???
