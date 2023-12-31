# DSi modchip guide

This document provides a complete overview on how to *hardmod* your Nintendo
DSi to run homebrew code using a bootrom exploit.

This guide is ***not*** aimed at total beginners. If you only want to run
custom software on your DSi, I suggest you try [this
guide](https://dsi.cfw.guide/) first.

> [!IMPORTANT]
> ***READ THIS GUIDE ALL THE WAY THROUGH BEFORE ATTEMPTING ANYTHING.***

> [!NOTE]
> As everything is still very much a work in progress, the installation
> procedure is far from being the smoothest possible. Sorry about that.

## Why would I want this?

* Your DSi freezes, crashes, or shows an error screen on boot, but you still
  want to play games on it.
* The eMMC NAND of your DSi is corrupted, but you still want to play games on
  your console.
* Your DSi can't be modded using the Memory Pit, Stylehax or Flipnote Lenny
  exploits.
* You don't want to use Unlaunch, but still want a cold boot exploit.
* You want to dump the full, unredacted DSi boot ROMs, or want to play around
  with the DSi hardware at a very early boot stage.

## Why would I **not** want this?

* One of the pre-existing exploits (Memory Pit, Stylehax, Flipnote Lenny, Unlaunch)
  or a flashcart suit all your needs.
* You don't want to hardmod your DSi.
* You can't solder --- hardmodding your DSi means you will have to solder.

## Prerequisites

Throughout this guide, you will need to:

* Solder **surface-mount** components. Installing the modchip will require
  handling tiny SMT components. If you have never soldered using flux and
  tweezers, please do not attempt to install this modchip.
* Compile software from source on your computer. This means you will need to
  have a development environment installed.

> [!TIP]
> Once the software is stable, binary releases will be provided so this second
> requirement can be relaxed.

## Installation steps

1. [Obtaining the modchip components](./components.md)
2. [Compiling and flashing the modchip firmware](./firmware.md)
3. [Compiling and flashing the payload](./payload.md)
4. [Installing the modchip](./install.md)

