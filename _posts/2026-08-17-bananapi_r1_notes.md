---
layout: post
title: Banana Pi R1 Armbian notes
---

Armbian no longer seems to offer BPi R1 images for download, but they're still compileable using the builder. You can get a modern Armbian image for a BPi R1 (also known as Lamobo R1) by doing this:

```bash
sudo apt install docker.io docker-buildx
git clone https://github.com/armbian/build
cd build
sudo usermod -aG docker $USER # fixes docker access permission as regular user
newgrp docker # applies the change; can also reboot. see https://stackoverflow.com/questions/48957195/how-to-fix-docker-permission-denied
docker run --rm --privileged multiarch/qemu-user-static --reset -p yes # works around a bug. see https://github.com/armbian/build/issues/8480
./compile.sh BOARD=lamobo-r1 RELEASE=trixie BUILD_DESKTOP=no BUILD_MINIMAL=yes KERNEL_CONFIGURE=no
```

Find the board image in `output/images/`. Surface-level tested, seems to work well enough.

If you think that this is bad advice, contact me somehow and let me know. Cheers!
