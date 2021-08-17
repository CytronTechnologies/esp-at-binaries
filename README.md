# Custom Compiled ESP-AT Firmware Binaries
These are the AT command firmwares for ESP8266 compiled from [Espressif ESP-AT Source Code](https://github.com/espressif/esp-at).<br>
The firmwares have two different sizes:
  - **Cytron_ESP-01S_AT_Firmware** - For ESP8266 with 1MB flash size (eg: ESP-01), doesn't support OTA update.<br>This firmware is preloaded in:
    - [Cytron ESP-01S](https://www.cytron.io/p-wif-trx-esp8266)
  - **Cytron_ESP-12F_WROOM-02_AT_Firmware** - For ESP8266 with flash size 2MB or above (eg: ESP-12E, ESP-12F, WROOM-02).<br>This firmware is preloaded in:
    - [Cytron ESP8266 WiFi Shield](https://www.cytron.io/p-shield-esp-wifi)
    - [Cytron ESP8266 WiFi Grove Module](https://www.cytron.io/p-grv-wifi-8266)

## What is NONOS-AT and ESP-AT?
NONOS-AT is the legacy AT Firmware from Espressif up to v1.7.x. This firmware is based on Non-OS SDK and no longer supported by Espressif. It's not recommended to use it anymore in new design.

ESP-AT is Espressif's AT firmware v2.0.0 and above. It's developed with OS based SDK and it's still actively supported by Espressif.<br>
However, the supported AT Commands are not fully compatible with the legacy AT firmware. Thus this is only recommended for new design.

For more info, please refer to:
- [ESP-AT User Guide](https://docs.espressif.com/projects/esp-at/en/release-v2.2.0.0_esp8266/index.html)
- [AT Command Set Comparison between NONOS-AT and ESP-AT](https://docs.espressif.com/projects/esp-at/en/release-v2.2.0.0_esp8266/AT_Command_Set/AT_Command_Set_Comparison.html)

## Cytron's Firmware vs Espressif's Firmware?
Since v2.0.0, Espressif has changed the UART port for AT Command to pin GPIO15 and GPIO13. However, most of the hardware for ESP8266 available in the market is still using GPIO1 and GPIO3 as its UART port. This makes extra wiring is needed in order to use the ESP-AT firmware.

Thus, we have configured the ESP-AT firmware and compiled it on our own so that we can use back pin GPIO1 and GPIO3 as its UART port. The rest of the features are exactly the same with Espressif's firmware.

| Function of Connection | Espressif Firmware                                             | Cytron Firmware                                              |
| ---------------------- | -------------------------------------------------------------- | ------------------------------------------------------------ |
| Update Firmware        | **UART0**<br><ul><li>GPIO3 (RX)</li><li>GPIO1 (TX)</li></ul>   | **UART0**<br><ul><li>GPIO3 (RX)</li><li>GPIO1 (TX)</li></ul> |
| AT Command/Response    | **UART0**<br><ul><li>GPIO13 (RX)</li><li>GPIO15 (TX)</li></ul> | **UART0**<br><ul><li>GPIO3 (RX)</li><li>GPIO1 (TX)</li></ul> |
| Log Output             | **UART1**<br><ul><li>GPIO2 (TX)</li></ul>                      | **UART1**<br><ul><li>GPIO2 (TX)</li></ul>                    |

## How to Update the Firmware?
Please download the latest version of [Espressif Flash Download Tool](https://www.espressif.com/en/support/download/other-tools).

### ESP-01S
1. A USB to UART converter is needed to update the firmware of ESP-01S. We recommend to use this [ESP01 USB Programmer Adapter](https://www.cytron.io/p-esp01-usb-programmer-adapter) as it will enter the boot mode automatically without the needs of pressing the boot button.
2. Run the Flash Download Tool and select "Developer" mode.
3. Select the firmware binary file and enter 0x0 as its target address.
4. Make sure all the settings are as follow:<br>
   - CrystalFreq: 26M
   - SPI SPEED: 40MHz
   - SPI MODE: DIO
   - FLASH SIZE: **8Mbit**
   - "DoNotChgBin" is selected<br>
   ![ESP-01 Settings](/images/ESP8266_Download_Tool_ESP01.png)
5. Select the correct COM according to your system. Make sure the baud rate is 115200 or below.
6. Press the START button and wait until it finishes.

### Cytron ESP8266 WiFi Shield
1. Stack the WiFi shield on an Arduino UNO. We will use the USB to UART converter onboard the Arduino UNO.
2. Upload the "Blink" Sketch to the Arduino UNO (File -> Examples -> 01.Basics -> Blink). This is to make sure the Arduino program doesn't use the serial function and interfere the upload process.
3. Push the slide switch to "Flash" and change the Tx Rx jumpers to "USB".
4. Press the "ESP RESET" button to reset the ESP8266 into boot mode.
5. Run the Flash Download Tool and select "Developer" mode.
6. Select the firmware binary file and enter 0x0 as its target address.
7. Make sure all the settings are as follow:<br>
   - CrystalFreq: 26M
   - SPI SPEED: 40MHz
   - SPI MODE: DIO
   - FLASH SIZE: **32Mbit**
   - "DoNotChgBin" is selected<br>
   ![ESP12F_WROOM02 Settings](/images/ESP8266_Download_Tool_ESP12F_WROOM02.png)
8. Select the correct COM according to your system. Make sure the baud rate is 115200 or below.
9. Press the START button and wait until it finishes.
10. Push the slide switch back to "RUN" and reset it again before start using the WiFi shield.
