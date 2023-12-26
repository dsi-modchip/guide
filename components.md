# DSi modchip components

Two types of modchips exist: purpose-built ones, and DIY ones.

In either case, a good surface-mount soldering station will be needed --- see
for example the [Picofly guide](https://gbatemp.net/download/a-definitive-picofly-install-guide.37968/)
on what might be necessary. A DSi modchip is slightly easier to install, though.

## Purpose-built modchip

A purpose-built modchip has a "WiFi interposer" form-factor which can be
plugged into the DSi's [WiFi module](https://dsibrew.org/wiki/WiFi_Module)
connector.

These modchips are currently still in the prototyping stage, and are not
publicly available.

![Photo of a purpose-built modchip. It's a small PCB of about 3 by 6
cm.](img/modchip-photo-600px.jpg)

### Component list

You will need:

* A purpose-built modchip
* An Infineon IRFHS8342 MOSFET
* Thin insulated copper wire
* Very thin enamel wire
* Kapton tape and glue
* A USB-UART converter

The IRFHS8342 is available from many wholesale electronics stores (like
Digikey, Farnell, Mouser, Arrow, ...), and is the same MOSFET as used in the
Picofly modchips for the Nintendo Switch.

## DIY modchip

A DIY modchip uses an existing Raspberry Pi RP2040 devboard. These are readily
available and cheap, but require more installation work.

### Component list

You will need:

* A Raspberry Pi RP2040 devboard. Acceptable ones are:
  * Raspberry Pi Pico (**Non-W, Non-H!**)
  * Adafruit ItsyBitsy RP2040
  * Seeed Xiao RP2040
  * WaveShare RP2040-Zero
  * WaveShare RP2040-Tiny
* A SPI flash chip, with the following requirements:
  * Compatible with a 3.3V supply
  * SPI interface (i.e. no I2C or parallel), 8 pins
  * Clock frequency of at least 8 MHz
  * At least 2 Mbit (128 kilobyte) and at most 128 Mbit (16 megabyte) in size.
  * A package smaller than SOIC/SOP or DIP --- TSSOP, MSOP, WSON, UDFN are OK.
    BGA or WLCSP are probably too impractical.
* An Infineon IRFHS8342 MOSFET
* Thin enamel wire
* Kapton tape and glue
* A USB-UART converter
* An external SPI flash programmer

The IRFHS8342 is available from many wholesale electronics stores (like
Digikey, Farnell, Mouser, Arrow, ...), and is the same MOSFET as used in the
Picofly modchips for the Nintendo Switch.

Two examples of good SPI flash chips are the Winbond W25Q80DVZPIG, and the
Renesas AT25DF021A-XMHN-T. Do note that these are two random suggestions, it's
probably more worthwile to look for ones that are cheaper or more readily
available, in case these are out of stock. Using a SPI EEPROM from the WiFi
module of a DS (***not** a DSi!*) would also work. DS game cartrige SPI chips
might work but won't necessarily be large enough.

An FTDI FT2232/FT4232 dongle can be used as both USB-UART converter and
external SPI flash programmer. Another option is using *another* RP2040/Pico
devboard and using different firmware for USB-UART and SPI flashing functionality
([example](https://github.com/stacksmashing/pico-serprog)).

## Next

Continue to [Compiling and flashing the modchip firmware](./firmware.md).
