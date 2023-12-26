# DSi modchip installation

If you have properly followed the previous chapters, everything is now ready and
you can now proceed with installing the modchip on your console.

***WARNING***: you are entering the danger zone. Accidents with soldering can
permanently brick your console. You have been warned.

## Soldering

### Opening your console

Please follow the iFixit guide ([DSi](https://www.ifixit.com/Guide/Nintendo+DSi+Motherboard+Replacement/3748),
[DSi XL](https://www.ifixit.com/Guide/Nintendo+DSi+XL+Motherboard+Replacement/3248))

### Purpose-built modchip

1. Cut two 5cm insulated wires from your spool of insulated wire
2. Strip both ends of both wires
3. Solder one end of one wire to the `HAX` testpoint of the modchip
4. Solder one end of *the other wire* to the `GND` testpoint of the modchip
5. Install the modchip in the WiFi daughterboard connector socket

### DIY modchip

First of all, you ***MUST*** do one of the following:
* Disconnect the WiFi module from your console and ***never*** reconnect it as
  long as the modchip is installed. Connect your SPI flash chip to the
  corresponding pins of your RP2040 board.
* Desolder the SPI EEPROM from your console's WiFi module and replace it with
  the one used in this guide. *Make sure that your SPI flash chip has the same
  pinout as the one on the WiFi module!*

Connect the following pins with testpoints on the DSi motherboard (for DSi XL
`TPxx` numbers, see [this page](https://dsibrew.org/wiki/DSi_XL_testpoints)).
Use regular insulated wire here.

For the connections to the MOSFET, wait and do not connect these yet. Connect
`UART TX` to your USB-UART connector, not to the DSi motherboard.

***NOTE***: the table contains logical pin numbers (i.e. GP*xx* numbers),
***not*** physical pin numbers!

| Pico | ItsyBitsy | Xiao | WaveShare | DSi mobo | Comment |
|:---- |:--------- |:---- |:--------- |:-------- |:------- |
| 3V3  | 3V3       | 3V3  | 3V3       | V33 / V3 | Power   |
| GND  | GND       | GND  | GND       | GND      | Ground  |
| 28   | 18        | 2    | 27        | SCK      | SPI clock |
| 27   | 19        | 4    | 28        | MOSI     | SPI controller-to-peripheral data |
| (N/A)| 20        | (N/A)| 29        | MISO     | SPI peripheral-to-controller data |
| 7    | 12        | 3    | 26        | CS2      | SPI chip select (CS) |
| 22   | 24        | 6    | 15        | RESET/RST|DSi reset|
| 21   | 25        | 7    | 14        | (N/A)    | HAX (glitch MOSFET) |
| 0    | 0         | 0    | 0         | (N/A)    | UART TX |

### Soldering the glitching MOSFET

> :warning: This is the difficult part. Do be really careful, don't set your
> soldering iron too hot, or you *will* brick your console.

1. Find the decoupling capacitors of the main SoC on the motherboard. These ar
   on the side of the testpoints, and look like this:
   ![](cpu_twl_rails.png)
   On a DSi, this photo is taken at the same orientation as the text. On a DSi
   XL, this is rotated by 90 degrees.
2. Place the IRFHS8342 MOSFET close to these decoupling capacitors, upside-down
   (that is, with the metal pads/contacts pointing up). Glue the MOSFET in
   place, but do leave the metal contacts open to the air!
3. Connect the positive side of *one* **1V2** decoupling cap to the drain (D)
   of the MOSFET (c.f. [MOSFET datasheet with pinout](https://www.infineon.com/dgdl/Infineon-IRFHS8342-DataSheet-v01_01-EN.pdf?fileId=5546d462533600a401535623992e1f5f)).
   Use very thin enamel wire.
4. Connect the negative side of *the same decoupling cap* to the source (S) of
   the MOSFET. Use very thin enamel wire.
5. From the source (S) of the MOSFET, run a strand of enamel wire that is abou
   one or two cm in length, and roll up the loose end in a spiral form.
6. Fill the loose spiral end of the wire with drops of solder.
7. Connect the ground (GND) of the modchip/RP2040 to the drop of solder you
   just created.
8. Glue the drop of solder in place.
9. Repeat steps 5..8, but starting from the gate (G) of the MOSFET, and to the
   HAX pin of the modchip.
10. Cover everything with kapton tape for protection.

### What about a flex-cable?

This is planned, but these have not yet been designed, let alone fabricated.

## Glitch parameter training

As the modchip firmware does not yet perform any automated glitch parameter
training, this has to be done manually. (This feature is planned, but it's not
there yet, sorry.)

1. Connect your USB-UART converter to the UART pin of your modchip.
2. Turn on the console, and collect the output of the USB-UART converter.
3. Let it run, until the UART output of the modchip says it has stopped.
4. Looking at the output, try to find which combination of glitch offset and
   length resulted in the most glitches.
5. Enter this narrow parameter range in the code [here](https://github.com/dsi-modchip/firmware/blob/main/rp2040/src/twlitf/glitchitf.c#L26-L38).
6. Change [this](https://github.com/dsi-modchip/firmware/blob/main/rp2040/src/twlitf/boothax.c#L62) line of code:
   where it currently says `boothax_train`, change this to `boothax_attack`.
7. Recompile the firmware.
8. **Disconnect the modchip from your console.** (The glitching MOSFET wires can stay connected.)
9. Reflash the firmware on the modchip, and reconnect it to the console.
