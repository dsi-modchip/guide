# Modchip soldering guide: purpose-built modchip

## Preparation

1. Cut two 5cm insulated wires from your spool of insulated wire
2. Strip both ends of both wires
3. Solder one end of one wire to the `HAX` testpoint of the modchip
4. Solder one end of *the other wire* to the `GND` testpoint of the modchi
   * For better results, twist these wires in a twisted pair/"spiral" pattern,
     without loosing track of which wire is which.
5. Connect the UART TX pin (part of the SOICbite footprint) and
   the ground pin next to it to your USB-UART converter.

## Installation

Install the modchip by inserting it in the WiFi daughterboard connector socket.

## Next

Return to [soldering the glitching MOSFET](../install.md#soldering-the-glitching-mosfet).

