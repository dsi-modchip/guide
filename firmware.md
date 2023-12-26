# DSi modchip firmware

Once you have obtained the modchip components, the next step is to compile and
flash the firmware of the modchip.

## Prerequisites

* The [Raspberry Pico SDK](https://www.raspberrypi.com/documentation/microcontrollers/c_sdk.html)

## Instructions

1. Get the source code of the [modchip firmware](https://github.com/dsi-modchip/firmware).
2. Run the following commands in a terminal:
  ```
  cd rp2040
  mkdir build
  cd build
  cmake .. -DPICO_BOARD=<YOUR_MODCHIP_BOARD_TYPE_HERE> -DCMAKE_BUILD_TYPE=RelWithDebInfo
  make -j$(nproc)
  ```
  Replace `<YOUR_MODCHIP_BOARD_TYPE_HERE>` with one of the following, depending
  on the modchip hardware you have obtained in the previous step:
  * `haxboard_r2`: a prototype of the purpose-built modchip.
  * `pico`
  * `seeed_xiao`
  * `waveshare_rp2040_one`
  * `waveshare_rp2040_zero`
  * `waveshare_rp2040_tiny`
  * `adafruit_itsybitsy_rp2040`
3. Connect the modchip into the USB port of your computer, **while holding the
   BOOT button pressed**.
4. Upload the firmware, either by copying the resulting `dsihaxfw.uf2` file to
   the virtual USB drive of the RP2040, or running the following command:
   `picotool load -f -v -x dsihaxfw.uf2`.

## Next

Continue to [Compiling and flashing the payload](./payload.md).
