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

| ESP-01        | USB TTL       |
| ------------- |:-------------:|
| TX            | RX            |
| RX            | TX            |
| GND           | GND           |
| 3V3           | 3V3           |
| EN            | 3V3           |

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


# TROUBLESHOOT
## SET ESP-01 BAUD RATE TO 9600 VIA AT COMMAND (Recommended)
The default baud rate for ESP8266-01 is 115200. You maybe need to set it to 9600.
```text
AT
AT+UART_DEF=9600,8,1,0,0
```

