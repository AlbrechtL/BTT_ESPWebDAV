# Custom BTT TF Cloud V1.0 Firmware
This is a custom firmware for the BTT TF Cloud V1.0 (https://github.com/bigtreetech/BTT-SD-TF-Cloud-V1.0) devices.

**Changes from the original BTT TF Cloud V1.0 firmware**

* Fixed SSID and password
* SD card is used only when a connection via WebDAV is established

**Top**

![Example Schematic](pics/BTT_TF_Cloud_Top.jpg)

**Bottom**

![Example Schematic](pics/BTT_TF_Cloud_Bottom.jpg)

This repository is based on the work of ardyesp (https://github.com/ardyesp/ESPWebDAV). Thanks! 


# Building
PlatformIO (https://platformio.org/) is recommended but also the classic Arduino IDE should work. You need to install the [Arduino esp8266 libraries](https://github.com/esp8266/Arduino). PlatformIO should install it automatically.

## How to
1. Open PlatformIO

2. Open the folder with this repository

3. Adapt `WiFiSettings.h`to your WiFi settings

4. Build it

5. Connect your PC to the device  
**WARNING: Don't insert the BTT device the same time in a SD slot because of back feeding the voltage or remove the LM1117 voltage regulator (see below)!**

6. Upload it to the device
7. When PlatformIO (esptool) is trying to connect to the BTT device press and hold the BOOT switch and hit the RESET switch a shot of time.

```
Uploading .pio/build/esp12e/firmware.bin
esptool.py v2.8
Serial port /dev/ttyUSB0
Connecting........_____..
```

8. Wait until the flash process is done

9. Reset the device again with the RESET switch.

# Technical Stuff

## WebDAV Server 
This project is a WiFi WebDAV server using ESP8266 SoC. It maintains the filesystem on an SD card.

Supports the basic WebDav operations - *PROPFIND*, *GET*, *PUT*, *DELETE*, *MKCOL*, *MOVE* etc.

Once the WebDAV server is running on the ESP8266, a WebDAV client like Windows can access the filesystem on the SD card just like a cloud drive. The drive can also be mounted like a networked drive, and allows copying/pasting/deleting files on SD card remotely.


## Pinout

BTT TF Cloud hardware uses the following SD card connections:

ESP Module|SD Card
---|---
GPIO13|MOSI   
GPIO12|MISO   
GPIO14|SCK    
GPIO4|CS   
GPIO5|CS Sense

Here is a sample schematic which is similar to the BTT TF Cloud devices. The real BTT TF Cloud schematic is not fully documented and may different form the following schematic.
![Example Schematic](pics/PrinterHookup2.jpg)

The card should be formatted for Fat16 or Fat32

To access the drive from Windows, type ```\\esp_hostname_or_ip\DavWWWRoot``` at the Run prompt, or use Map Network Drive menu in Windows Explorer.


## Developing
When removing the LM1117 voltage regulator it is possible to connect to the ESP8266 to USB and let the device connected via SD. 

![Example Schematic](pics/BTT_TF_Cloud_Removed_LM1117.jpg)
