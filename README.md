# Custom Compiled ESP-AT Firmware Binaries
These are the AT command firmwares for ESP8266 compiled from [Espressif ESP-AT Source Code](https://github.com/espressif/esp-at).<br>
The firmwares have two different sizes:
  - **Cytron_ESP-01S_AT_Firmware** - For ESP8266 with 1MB flash size (eg: ESP-01), doesn't support OTA update.<br>This firmware is preloaded in:
    - [Cytron ESP-01S](https://www.cytron.io/p-wif-trx-esp8266)
  - **Cytron_ESP-12F_WROOM-02_AT_Firmware** - For ESP8266 with 2MB and above flash size (eg: ESP-12F, WROOM-02).<br>This firmware is preloaded in:
    - [Cytron ESP8266 WiFi Shield](https://www.cytron.io/p-shield-esp-wifi)
    - [Cytron ESP8266 WiFi Grove Module](https://www.cytron.io/p-grv-wifi-8266)

## What is NONOS-AT and ESP-AT?
NONOS-AT is the legacy AT Firmware from Espressif up to v1.7.x. This firmware is based on Non-OS SDK and no longer supported by Espressif. It's not recommended to use it anymore in new design.

ESP-AT is Espressif's AT firmware v2.0.0 and above. It's developed with OS based SDK and it's still actively supported by Espressif.<br>
However, the supported AT Commands are not fully compatible with the legacy AT firmware. Thus this is only recommended for new design.

For more info, please refer to:
- [ESP-AT User Guide](https://docs.espressif.com/projects/esp-at/en/release-v2.2.0.0_esp8266/index.html)
- [AT Command Set Comparison between NONOS-AT and ESP-AT](https://docs.espressif.com/projects/esp-at/en/release-v2.2.0.0_esp8266/AT_Command_Set/AT_Command_Set_Comparison.html)

## What is the different between Cytron's Firmware and Espressif's Firmware?
Since v2.0.0, Espressif has changed the UART port for AT Command to pin GPIO15 and GPIO13. However, most of the hardware for ESP8266 available in the market is still using GPIO1 and GPIO3 as its UART port. This makes extra wiring is needed in order to use the ESP-AT firmware.

Thus, we have configured the ESP-AT firmware and compiled it on our own so that we can use back pin GPIO1 and GPIO3 as its UART port. The rest of the features are exactly the same with Espressif's firmware.

| Function of Connection | Espressif Firmware                                             | Cytron Firmware                                              |
| ---------------------- | -------------------------------------------------------------- | ------------------------------------------------------------ |
| Update Firmware        | **UART0**<br><ul><li>GPIO3 (RX)</li><li>GPIO1 (TX)</li></ul>   | **UART0**<br><ul><li>GPIO3 (RX)</li><li>GPIO1 (TX)</li></ul> |
| AT Command/Response    | **UART0**<br><ul><li>GPIO13 (RX)</li><li>GPIO15 (TX)</li></ul> | **UART0**<br><ul><li>GPIO3 (RX)</li><li>GPIO1 (TX)</li></ul> |
| Log Output             | **UART1**<br><ul><li>GPIO2 (TX)</li></ul>                      | **UART1**<br><ul><li>GPIO2 (TX)</li></ul>                    |
