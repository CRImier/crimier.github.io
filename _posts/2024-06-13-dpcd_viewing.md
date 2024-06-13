---
layout: post
title: DPCD viewing on Linux
---

# DPCD viewing on Linux

You can read DPCD registers from Linux like this: 

```bash
sudo xxd /dev/drm_dp_aux0 |head -n128|grep -v "0000 0000 0000 0000 0000 0000 0000 0000"
```

of course, substitute the number as needed.

Does this give you an Input/output error, like on a Framework laptop's display? Try this then,
this example reads the 0x100 register to see the DP link state:

```bash
sudo dd if=/dev/drm_dp_aux0 bs=1 skip=256 count=16 |xxd
```

Want register descriptions? Page 16
[in this Intel doc](https://www.intel.com/content/dam/support/us/en/programmable/support-resources/fpga-wiki/asset02/displayport-rx-and-tx-desgin-example-an-r1.pdf)
is a good start, and so is a document you can find by searching `ug_displayport.pdf filetype:pdf`.

Surely, you can also use the same interface to poke at DPCD and do AUX stuff;
this article is just "how to get DisplayPort link values like current and possible link width".

If you think that this is bad advice, contact me somehow and let me know. Cheers!
