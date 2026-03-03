# LoRaM3-D experiments

BSFrance provided IDE Templates for their 
[LoRaM3-D board](https://www.thingiverse.com/thing:3078966) to work with
SW4STM32 (System Workbench for STM32) and STLink debugger. The main() in app.c
didn't do much and was buggy.  But I use Linux; so this has been converted into
a project that I can build on the command line, which does a little more. 

How to build and flash on the command line:

```
cd LoRaM3_F303_HAL_OLED_LORA/Debug
make LoRaM3_F303_HAL_OLED_LORA.elf
dfu-util --alt 0 --dfuse-address 0x08000000 -D LoRaM3_F303_HAL_OLED_LORA.bin 
```
Before the dfu command, the board has to be put into DFU mode by flipping the
Run/ISP switch to the down position (closer to the button).  And then flip it
back up to run the code.  The firmware that it shipped with could also enter
DFU mode by pressing the button twice quickly, but that doesn't seem to work
now.

I test it by simultaneously running a transmitter or receiver on the Raspberry
Pi 3 with an old Dragino LoRa hat, for which code is provided at 
<https://github.com/gwendal-lv/dragino_rpi-lora-tranceiver> (a fork of the
original <https://github.com/dragino/rpi-lora-tranceiver> which was lacking a
README but at least didn't seem to be too buggy).  After flashing, plug in the
BSFrance board in Run mode (leftmost switch flipped upwards), and a USB serial
port will appear.  Connect to it:

```

$ screen /dev/ttyACM11 115200
```
Then if the raspberry pi sends a message, it will be copied to the serial
output from the STM32; if the raspberry pi is receiving, it can see the
messages that this code is sending.  And you also see test messages on the OLED
display.

The channel, spreading factor etc. are arbitrarily hard-coded, but they match
between the rpi and the STM32 for now.

