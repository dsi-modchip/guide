# DSi modchip payload

Once you have flashed the firmware, the next step is to compile and flash the
exploit payload.

## Prerequisites

* A GCC ARM toolchain (GNU or Linaro `arm-none-eabi-gcc`, devkitARM, Wonderful `toolchain-gcc-arm-none-eabi`, ...)
* A native C compiler
* Meson
* Python 3
* Make
* If using a purpose-built modchip: `dfu-util` or a different DFU flashing utility
* If using a DIY modchip: `flashrom` and an external programmer (e.g. FTDI
  FT2232 adapter, or a Pico using [pico-serprog](https://github.com/stacksmashing/pico-serprog)).

## Instructions

### Compiling

1. Get the source code of the [exploit payload](https://github.com/dsi-modchip/payload)
  * Do a recursive clone, the submodules are needed
2. Run `make`

### Flashing - purpose-built modchip

If you use `dfu-util`: just run `make dfu`.

If you don't have `dfu-util`: go to the `build` directory inside the exploit
payload source code folder. It should contain a file called `payload.bin`. Flash
this file using your DFU flashing program of choice.

### Flashing - DIY modchip

With a DIY modchip, two options are possible:
* Use an external SPI flash programmer, using `flashrom`.
* Use an external SPI flash programmer using another program. You're on your
  own for that.

For the first option: after connecting the external programmer, run the
following command: `FLASHROM_PRGM=<flashrom programmer setting> make flash`.
Consult the [flashrom documentation](https://www.flashrom.org/) and maybe their
[old wiki](https://wiki.flashrom.org/Flashrom) on what to fill in for the
`<flashrom programmer setting>`. This depends on which external programmer you
are using.
* For an FTDI dongle, using Linux, use:
  `FLASHROM_PRGM=ft2232_spi:type=<model>,port=<interface>`. `<model>` is
  `2232H`, `4232H`, `232H`, etc. `<interface>` is `/dev/ttyUSBx` for some value
  of `x`.
* For pico-serprog, using Linux, use:
  `FLASHROM_PRGM=serprog:dev=/dev/ttyACMx:115200` for some value of `x`.

> [!TIP]
> A method of flashing the SPI memory directly using the modchip RP2040 is
> planned. This will make this step as easy as for the purpose-built modchip.

## Next

Continue to [Installing the modchip](./install.md).
