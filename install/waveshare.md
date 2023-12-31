# Modchip soldering guide: WaveShare RP2040-Zero/Tiny/One

## Preparation

Pick *one of* the following two options:

* Disconnect the WiFi module from your console and ***never*** reconnect it as
  long as the WaveShare board is installed. Connect your SPI flash chip to the
  corresponding pins of your RP2040 board.
* Desolder the SPI EEPROM from your console's WiFi module and replace it with
  the one used in this guide.

> [!IMPORTANT]
> When picking the second option, make sure that your SPI flash chip has the
> same pinout as the one on the WiFi module!

Then do the following:

1. Cut two 5cm insulated wires from your spool of insulated wire
2. Strip both ends of both wires
3. Solder one end of one wire to pin `GP14` of the WaveShare board
4. Solder one end of *the other wire* to the `GND` pin of the WaveShare board
   *closest to GP14*.
   * For better results, twist these wires in a twisted pair/"spiral" pattern,
     without loosing track of which wire is which.
6. Connect pin `GP0` and a ground pin to your USB-UART converter.

## Soldering the WaveShare RP2040

Connect the following pins with testpoints on the DSi or DSi XL motherboard.
Use regular insulated wire here.

> [!WARNING]
> ***NOTE***: the table contains logical pin numbers (i.e. GP*xx* numbers),
> ***not*** physical pin numbers!

| WaveShare RP2040 | SPI flash | DSi mobo | DSi XL mobo | Comment |
|:---------------- |:--------- |:-------- |:----------- |:------- |
| 3V3              | VDD / VCC | V33 / V3 | TP13        | Power   |
| GND              | VSS / GND | GND      | TP5         | Ground  |
| 3V3              | #WP       | *(N/A)*  | *(N/A)*     | write-protect |
| 27               | SCLK      | SCK / SK | TP73        | SPI clock |
| 28               | COPI / MOSI | MOSI   | TP69        | SPI controller-to-peripheral data |
| 29               | CIPO / MISO | MISO   | TP71        | SPI peripheral-to-controller data |
| 26               | nCS       | CS2 / C2 | TP79        | SPI chip select (CS) |
| 15               |           | RESET / RST | TP85     | DSi reset |
| 0                |           | *(N/A)*  | *(N/A)*     | UART TX, to USB-UART adapter |

## Next

Return to [soldering the glitching MOSFET](../install.md#soldering-the-glitching-mosfet).

