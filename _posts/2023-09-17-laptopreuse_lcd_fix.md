---
layout: post
title: Laptop with missing internal LVDS screen won't output console to external screen properly
img: /assets/img/230917_laptopscrfix/0.jpg
---

# Laptop with missing internal LVDS screen won't output console to external screen properly

You take a laptop motherboard that doesn't have a screen, then connect it to an external screen. Then, you decide you'd rather run a framebuffer application - like `tmux` or `irssi`. However, the text's stretched out or just takes a part of the screen. You could even say that, even though the original LCD panel is no longer connected, it still impacts the image on the external monitor in the same way. What gives?

Other symptoms:

- `vga=` parameter not working anymore
- screen resolution is limited to the panel's original resolution
- it's probably a limitation that's either coded into the BIOS or into the built-in graphics processor firmware (through the BIOS)
- Linux GUI recognizes the externally connected screen and the missing internal screen as a single device
- so, resolution is limited to 640x480 or 800x600 or 1280x800 or something

Solutions that don't work:

- changing framebuffer drivers might not help you there - I haven't tried
- `GFXMODE` will not help you there
- neither will `vga=` , and it's also outdated
- X server switches to the right resolution for the external screen
- Linux framebuffer is not as sophisticated and will not work with the right resolution, though

Here's how it might look:

~{}(/assets/img/230917_laptopscrfix/0.jpg)

Other possibility is that your console will be scaled way up compared to the acttual resolution of your external screen.

Here's an explanation: your laptop expects a screen that's not there but the firmware pretends it's there. Framebuffer console uses the lowest possible resolution out of all available screens, so it ends up being limited to the hardcoded resolution of the internal screen.

[The fix](https://irlp.groups.io/g/IRLP/topic/19796361#70934) is to disable the built-in panel interface using a kernel parameter:

```video=LVDS-1:d```

Add this to your `GRUB_CMDLINE_LINUX=` and regenerate grub config, or append it to kernel params while booting in the grub menu, boot with it, voila.

Tested on:

- some Toshiba Satellite motherboard with missing screen
- EEE PC 701 motherboard
- DN2800MT motherboard (built-in graphics prevent the external screens from even initializing if you don't blacklist the LVDS panel)

eDP screens don't tend to suffer from this because the AUX connection is required for the panel to function, and it can also provide autodetection. The EDID mechanism is optional for LVDS panels, however, so laptop manufacturers often hardcode the panel resolution.
