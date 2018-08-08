# Experimenting with the MiP
This is a place to organize all my thoughts and experimation on [WowWee's MiP](https://www.wowwee.com/mip/) robot.  Most of what is collected here relates to interfacing with  MiP using various microcontrollers connected via the internal hardware universal asynchronous receiver transmitter (UART) port.  This readme contains information I've gathered while working on MiP.  My experiments can be found in the [wiki](https://github.com/Tiogaplanet/Experimenting-with-the-MiP/wiki).

## Acknowledgement
Thanks go out to [adamgreen](https://github.com/adamgreen) for breathing new life into this project.  Without his help in correcting a design flaw in the original [ProMini-Pack](https://github.com/sparkfun/MiP_ProMini-Pack) I'd probably still be wondering why I can't get an Arduino to talk to the MiP.  He revised the ProMini-Pack to use the 5V, 16MHz version of the ATmega328P and subsequently ported his [MiP C API](https://github.com/adamgreen/MiP-Capi) to the ProMini making it incredibly easy to write Arduino sketches to control MiP. His revised and working board along with its supporting library are available for [download](https://github.com/adamgreen/MiP_ProMini-Pack). You can read [the issue](https://github.com/WowWeeLabs/MiP-BLE-Protocol/issues/18) that broke through my stagnant effort to connect an Arduino to MiP which, while posted to one of WowWee's repositories, was ultimately found to be a problem on the original ProMini-Pack.

## Links
Here in no particular order are the sites I recommend reviewing to before diving into hacking your MiP.
* [Hacking the MiP](https://learn.sparkfun.com/tutorials/hacking-the-mip---promini-pack?_ga=2.116106246.1689750351.1531221450-408871298.1525958450) - SparkFun's guide to adding a ProMini Pack to MiP. Applies to adamgreen's successor pack too.
* WowWee's Bluetooth Low Energy (BLE) [command list](https://github.com/WowWeeLabs/MiP-BLE-Protocol/blob/master/MiP-Protocol.md) for  MiP.  Works over UART too.
* [ESP8266 Over The Air (OTA) Updates with Arduino IDE](https://randomnerdtutorials.com/esp8266-ota-updates-with-arduino-ide-over-the-air/)
* [How to upgrade your ESP8266 memory to 4MB (in under 2 minutes)](https://www.youtube.com/watch?v=7Q6ABad7U6o)
* A [prototyping shield](https://github.com/Tiogaplanet/MiP_ProtoPack) for adamgreen's ProMini-Pack.
* An [adapter board](https://github.com/Tiogaplanet/MiP_D1-mini-Pack) to connect a D1 mini to MiP.

## Control boards
While this project started with an Arduino ProMini-compatible board, other microcontrollers or single board computers are able to tap MiP's UART connector.  The pros on cons of some of the most likely candidates are recorded here.

### ProMini-like Arduinos including the ProMini-Pack

#### Pros
* Several analog and digital input/output (IO) lines.
* Easy to build custom-shaped boards to fit outside the MiP case.
* Flexible options for power conservation.
* Lots of available documentation.

#### Cons
* No internet connectivity.
* Bulky.

### ESP-01 (ESP8266-based)

#### Pros
* Very small form factor.
* Internet connectivity.

#### Cons
* Limited number of IO lines (four if you re-purpose the serial port).
* Limited ability to conserve power.
* Not easily programmed.

### ESP-12 (ESP8266-based)

#### Pros
* Small form factor.
* Internet connectivity.
* Good balance between size and connectivity.

#### Cons
* Gives up the convenient break-outs of the NodeMCU for smaller packaging.
* Small packaging requires some skill to solder unless a break-out board is used.
Not easily programmed.

### NodeMCU (ESP8266-based)

#### Pros
* Plenty of IO lines.
* Internet connectivity.
* Can be programmed over the air (OTA).

#### Cons
* Too big to store inside MiP.

### Wemos D1 mini and compatible boards (ESP8266-based)

### Pros
* Internet connectivity.
* Adequate number of IO lines to include a single analog line.
* Small size allows it to be mounted in MiP's head.
* Easy to program.
* USB connector permits external power when D1 mini is mounted externally.
* Can be programmed OTA.

### Cons
* Primary RX/TX pair is electrically shared with USB input which interferes with programming when MiP is attached.
* Secondary UART is TX only.
