---
layout: post
title: BananaPi M2 Zero Notes
---

[docs link](https://docs.banana-pi.org/en/BPI-M2_Zero/BananaPi_BPI-M2_Zero)
[wiki link](https://wiki.banana-pi.org/Banana_Pi_BPI-M2_ZERO)

I ran [Armbian](https://www.armbian.com/bananapi-m2-zero/). It was alright. Some notes:

* Use `armbian-config` to get more of the hardware exposed
* Serial will not be exposed as ttyAMA0 or whatever - it'll just be ttyS0, ttyS1 and so on. Read `dmesg` and you will see!

## Making SPI exposed in userspace

Solution taken [from here](https://forum.armbian.com/topic/27457-connecting-banana-pi-m2-zero-with-ili9341-display-over-spi-on-latest-armbian-image/)

`armbianEnv.txt`:

```bash
    overlays=spi-spidev 
    param_spidev_spi_bus=0
```

This gets you to `/dev/spidev0.0`. Can try `modprobe spidev` if missing the device.

To be continued, maybe.

If you think that this is bad advice, contact me somehow and let me know. Cheers!
