---
layout: post
title: KiKit (and other plugins) failing to load on Kicad 8.0.0/8.0.1, Debian/Ubuntu 
---

# KiKit (and other plugins) failing to load on Kicad 8.0.0/8.0.1, Debian/Ubuntu 

pcbnew module not found kinda error when you try `kikit --help` in commandline.

the pcbnew.py file [is misplaced.](https://forum.kicad.info/t/kicad-8-on-ubuntu-modulenotfounderror-no-module-named-pcbnew/49029/),
so is its corresponding compiled file.

```bash
sudo cp /usr/lib/python3.8/site-packages/pcbnew.py /usr/local/lib/python3.8/dist-packages/
sudo cp /usr/lib/python3.8/site-packages/_pcbnew.so /usr/local/lib/python3.8/dist-packages/
```

also, you might need to yeet the old `pcbnewTransition.py` files.

```bash
rm -vr .local/lib/python3.8/site-packages/pcbnewTransition*
```

now `import pcbnew` will fail cuz missing pcbnewTransition, but you can do

```bash
python3 -m pip install kikit
```

and that will reinstall the deleted file lol.

also, cheat: reinstalling kikit from repo is as simple as `make install`, it appears.

TODO: socially acceptable ways to rant about problems with open-source software bs
