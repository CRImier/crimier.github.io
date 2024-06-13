---
layout: post
title: KiKit discontinuous outline unobvious stuff
img: /assets/img/240613_kikit_discont/0.png
---

# KiKit discontinuous outline unobvious stuff

Working with KiKit? It's great, and this problem ain't its fault, I'd hope.

![](/assets/img/240613_kikit_discont/1.png)

If your board has a footprint with origin far outside of the board area, KiKit will not pick it up.
In turn, if this footprint constitutes part of your outline, that's going to generate a "discontinuous outline" problem,
and KiKit will stall before even starting to generate anything, leaving you with an empty page and no hints.

![](/assets/img/240613_kikit_discont/0.png)

Solution? In the Source tab, set tolerance to a higher value than 1mm.

```json
{
    "source": {
        "tolerance": "10mm"
    }
}
```

Of course, there's a few ways that a discontinuous outline bug might happen.
[Read through these issues to learn more.](https://github.com/yaqwsx/KiKit/issues?q=Discontinuous+outline)

If you think that this is bad advice, contact me somehow and let me know. Cheers!
