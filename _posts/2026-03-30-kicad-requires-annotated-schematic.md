---
layout: post
title: KiCad "Updating the pcb requires a fully annotated schematic"
---

This error will show up when you try to update PCB from schematic (for instance, using the F8 key). This usually happens when you copy pieces
of schematic between projects - which is kickass and everyone should do more of that! However, if you end up with duplicate reference designators,
this error will happen every time you try to sync to PCB, preventing any updates from happening.

To fix this - in schematic, run ERC, and in Error list, find the duplicated reference designators error -
it'll point out which reference designators specifically are duplicated, info that's otherwise not straightforward to find.
You might need to run ERC multiple times over to find all of them, if I'm not mistaken?

If you think that this is bad advice, contact me somehow and let me know. Cheers!
