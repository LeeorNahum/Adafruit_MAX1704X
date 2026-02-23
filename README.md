> # Fork: two bug fixes from the original Adafruit library
>
> **1. `isDeviceReady()`: overly strict version check**
> The original code required the VERSION register (`0x08`) to match `0x001X`. The datasheet documents this register as simply "IC production version" and lists its default as `0x001_`, but never states that `0x001X` is the only valid production range. Chips with versions like `0x0003` are legitimate. The correct "no battery" sentinel is `0xFFFF`: since the IC is powered directly from the battery, a missing battery causes the I2C bus to float high. Fixed to check `version != 0xFFFF`.
>
> **2. `begin()`: unconditional Power-On Reset command**
> The original `begin()` always wrote `0x5400` to the CMD register. The datasheet describes this as a command that "causes the device to completely reset as if power had been removed," and explicitly warns it should "only [be used] when the battery is fully relaxed" because it triggers a quick-start and restores all registers to their defaults. Calling it on every `begin()` unconditionally discards accumulated fuel gauge state. Fixed: `begin(wire, doReset = false)`, reset is now opt-in.

---

Adafruit_MAX1704X [![Build Status](https://github.com/adafruit/Adafruit_MAX1704X/workflows/Arduino%20Library%20CI/badge.svg)](https://github.com/adafruit/Adafruit_MAX1704X/actions)[![Documentation](https://github.com/adafruit/ci-arduino/blob/master/assets/doxygen_badge.svg)](http://adafruit.github.io/Adafruit_MAX1704X/html/index.html)
================

<a href="https://www.adafruit.com/product/5580"><img src="https://cdn-shop.adafruit.com/970x728/5580-00.jpg" width="500px"></a>

# Adafruit MAX1704X Lipo Monitor / Fuel Gauge Library
This library is for the Adafruit MAX17048 or MAX17049 Breakouts

Tested and works great with Adafruit's MAX17048 Breakout Boards
* https://www.adafruit.com/product/5580

This chip uses I2C to communicate, 2 pins are required to interface

Adafruit invests time and resources providing this open source code, please support Adafruit and open-source hardware by purchasing products from Adafruit!

## About the MAX1704X ##

The MAX17048/MAX17049 ICs are tiny, micropower current
fuel gauges for lithium-ion (Li+) batteries in handheld
and portable equipment. The MAX17048 operates with
a single lithium cell and the MAX17049 with two lithium
cells in series.

More information on the MAX1704X can be found in the datasheet: https://www.maximintegrated.com/en/products/power/battery-management/MAX17048.html

## About this Driver ##

Written by ladyada for Adafruit Industries.
BSD license, check license.txt for more information
All text above must be included in any redistribution

To install, use the Arduino Library Manager and search for "Adafruit MAX1704X" and install the library.
