# Ok Google with Arduino and ESP8266
Control your electronics with an Google Assistant + Arduino UNO + ESP8266



## Contents
- [REQUIREMENTS](#requirements)
- [PINOUT](#pinout)
  - [PINOUT FINAL](#pinout-final)
  - [PINOUT FLASHING ESP-01](#pinout-flashing-esp-01)
  - [PINOUT AT COMMAND MODE ESP-01](#pinout-at-command-mode-esp-01)
- [FLASHING ESP8266 (Optional)](#flashing-esp8266-optional)
  - [FLASH ESP-01 WITH ESPTOOL](#flash-esp-01-with-esptool)  
- [INSTALLATION](#installation)
  - [Setting up Blynk](#setting-up-blynk)
  - [Setting up IFTTT](#setting-up-ifttt)
  - [Upload Code and Test](#upload-code-and-test)
- [TROUBLESHOOT](#troubleshoot)
  - [SET ESP-01 BAUD RATE TO 9600 VIA AT COMMAND (Recommended)](#set-esp-01-baud-rate-to-9600-via-at-command-recommended)

<p align="center">
  <img src="https://raw.githubusercontent.com/anwareset/OkGoogleArduino/master/1.jpeg">
</p>



# REQUIREMENTS:
* Android phone Marsmallow or higher or Apple phone (for Google Assistant)
* IFTTT Account
* Blynk App Account
* Arduino UNO
* ESP8266 (ESP-01) WiFi Module
* Some Jumper Cables
* Relay SRD-05VDC-SL-C (Optional)
* USB TTL Serial (Optional)
* 5V to 3.3V Logic Converter (Optional)




# PINOUT
Use the PINOUT FINAL is you done with anything in this project.
## PINOUT FINAL
The basic pinout of this project.

| UNO           | ESP-01        |
| ------------- |:-------------:|
| D2 (as TX)    | RX            |
| D3 (as RX)    | TX            |
| GND           | GND           |
| 3V3           | 3V3           |
| 3V3           | EN            |

| UNO           | LED           |
| ------------- |:-------------:|
| D7            | ANODE (+)     |
| GND           | CATHODE (-)   |

| UNO           | RELAY         |
| ------------- |:-------------:|
| D8            | IN            |
| 5V            | VCC           |
| GND           | GND           |



## PINOUT FLASHING ESP-01
Use this pinout only when you need to flash your ESP-01 Firmware

| ESP-01        | USB TTL       |
| ------------- |:-------------:|
| TX            | RX            |
| RX            | TX            |
| GND           | GND           |
| IO2           | GND           |
| 3V3           | 3V3           |
| EN            | 3V3           |


## PINOUT AT COMMAND MODE ESP-01
Use this pinout when you need to interact with AT Command only

| ESP-01        | USB TTL       |
| ------------- |:-------------:|
| TX            | RX            |
| RX            | TX            |
| GND           | GND           |
| 3V3           | 3V3           |
| EN            | 3V3           |

Then use Serial Monitor from Arduino IDE to interact with AT




# FLASHING ESP8266 (Optional)
Use this if your ESP8266 have old or deprecated firmware installed.
## FLASH ESP-01 WITH ESPTOOL

FIRMWARE ESP-01 :
1) AT  V1.6.2 from https://www.espressif.com/sites/default/files/ap/ESP8266_AT_Bin_V1.6.2_0.zip
2) SDK V2.2.1 from https://codeload.github.com/espressif/ESP8266_NONOS_SDK/zip/v2.2.1

Flash SDK First > Then Flash AT Afterward

```text
esptool.py --port /dev/ttyUSB0 --baud 115200 write_flash --flash_size 1MB --flash_mode dio <MEMORY ADDRESS 0> <FILE-0.BIN> <MEMORY ADDRESS 1> <FILE-1.BIN> <MEMORY ADDRESS N> <FILE-N.BIN>
```

Memory Address :

| File                      | Address           |
| ------------------------- |:-----------------:|
| boot_v1.2.bin             | 0x00000           |
| user1.1024.new.2.bin      | 0x01000           |
| esp_init_data_default.bin | 0xfc000           |
| blank.bin                 | 0x7e000 & 0xfe000 |




# INSTALLATION
## Setting up Blynk
1) Follow instruction on http://blynk.cc/getting-started/
2) Download and install Blynk App for Android or IOS
3) Install Blynk Library for Arduino IDE
4) Open Blynk App
5) Create 'New Project'
6) Choose 'Arduino UNO' and 'WiFi' then click 'Create'
7) Get the Blynk Auth Token. Note it
8) Click on + sign on the top and one Button
9) Click on Button and set the pin to 'Digital' and 'D7'. Set pin values to 1 and 0. Set switch to 'Push'
10) Create same as step 5 for D8 pin


## Setting up IFTTT
1) Register IFTTT account
2) Create Trigger (IF)
3) Search Google Assistant
4) Select 'Say a phrase with a text ingredient'. Enter everything you need.
5) Choose Action (THEN)
6) Search Webhooks
7) Click on 'Make a web Request'
8) Set the action
### URL
```text
http://blynk-cloud.com/update/D7
```
### Method
```text
PUT
```
### Content Type
```text
application/json
```
### Body
```text
["1"]
```
and accept etc.
That body part decides what you put in D7 pin. Apparenly this will make the led light up. Then you can define another IFTTT Applet to write ["0"] on the pin to turn it off. And create again for D8 pin.

## Upload Code and Test
Don't forget to import the Blynk library to your Arduino IDE. You can read https://www.arduino.cc/en/Guide/Libraries#toc4. Then you can follow https://www.arduino.cc/en/main/howto for upload the sketch code to your Arduino UNO.
Use <b>OkGoogleArduino.ino</b> sketch code. Don't forget to edit it.
```text
char auth[] = "8f180320xxxxxxxxxc458c50faa";
char ssid[] = "iPhone 5S";
char pass[] = "11211111";
```
Edit it with your Blynk auth key, WiFi access point, and password. If your WiFi has no password, then use this.
```text
char pass[] = ""
```

### Result
[![MIKHMON OpenWrt Installer](https://raw.githubusercontent.com/anwareset/OkGoogleArduino/master/0.jpg)](https://www.youtube.com/watch?v=ebIpf0-m83k "Google Assistant with Arduino UNO and ESP8266")


# TROUBLESHOOT
## SET ESP-01 BAUD RATE TO 9600 VIA AT COMMAND (Recommended)
The default baud rate for ESP8266-01 is 115200. You maybe need to set it to 9600.
```text
AT
AT+UART_DEF=9600,8,1,0,0
```
