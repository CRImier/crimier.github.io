---
layout: post
title: UGREEN CM578 enclosure and WD SN770M incompatibility
img: /assets/img/250629_nvme/0.png
---

# UGREEN CM578 enclosure and WD SN770M incompatibility

![](/assets/img/250629_nvme/0.png)

I was helping a friend set up a WD BLACK SSD (SN770M 2TB, 2230) with a Steam Deck. We put it into a UGREEN enclosure to clone the original drive
onto the new drive. However, the enclosure didn't recognize the drive - the enclosure wouldn't show up as a USB device for about 10-20 seconds, and then,
it'd enumerate as a 0-byte storage device.

This was weird - the drive was newly purchased, it was quite unlikely it'd be broken. However, it didn't work in (identical, same UGREEN) enclosures.

As a hail mary, we put it into the Steam Deck - and the drive showed up properly in BIOS settings overview.
Mind you - the Steam Deck booted into a black screen, seemingly, because the drive was empty; we had to press some buttons to have it
boot into BIOS UI to see the drive show up.

Enclosure `lsusb`:

```
0bda:9210 Realtek Semiconductor Corp. RTL9210 M.2 NVME Adapter
```

Enclosure name: `UGREEN NVMe M.2 USB 3.2 SSD Enclosure Adapter with Cooling Pad` ; model number seems to be CM578

So, tl;dr if this NVMe enclosure (or some other enclosure based on similar chip) doesn't work for you, fret not -
it might be that it's just not up to date enough to support your NVMe drive.

If you think that this is bad advice, contact me somehow and let me know. Cheers!
