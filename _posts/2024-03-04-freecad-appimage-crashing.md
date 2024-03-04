---
layout: post
title: FreeCAD AppImage crashing
---

# FreeCAD AppImage crashing

All recent FreeCAD AppImages started suddenly crashing on Ubuntu with this kind of output:

```
    FreeCAD 0.21.2, Libs: 0.21.2R33771 (Git)
    © Juergen Riegel, Werner Mayer, Yorik van Havre and others 2001-2023
    FreeCAD is free and open-source software licensed under the terms of LGPL2+ license.
    FreeCAD wouldn't be possible without FreeCAD community.
      #####                 ####  ###   ####
      #                    #      # #   #   #
      #     ##  #### ####  #     #   #  #   #
      ####  # # #  # #  #  #     #####  #   #
      #     #   #### ####  #    #     # #   #
      #     #   #    #     #    #     # #   #  ##  ##  ##
      #     #   #### ####   ### #     # ####   ##  ##  ##
    
    MESA-LOADER: failed to open iris: /usr/lib/dri/iris_dri.so: cannot open shared object file: No such file or directory (search paths /usr/lib/x86_64-linux-gnu/dri:\$${ORIGIN}/dri:/usr/lib/dri, suffix _dri)
    failed to load driver: iris
    MESA-LOADER: failed to open iris: /usr/lib/dri/iris_dri.so: cannot open shared object file: No such file or directory (search paths /usr/lib/x86_64-linux-gnu/dri:\$${ORIGIN}/dri:/usr/lib/dri, suffix _dri)
    failed to load driver: iris
    MESA-LOADER: failed to open swrast: /usr/lib/dri/swrast_dri.so: cannot open shared object file: No such file or directory (search paths /usr/lib/x86_64-linux-gnu/dri:\$${ORIGIN}/dri:/usr/lib/dri, suffix _dri)
    failed to load driver: swrast
    WebEngineContext used before QtWebEngine::initialize() or OpenGL context creation failed.
    QGLXContext: Failed to create dummy context
    Failed to create OpenGL context for format QSurfaceFormat(version 2.0, options QFlags<QSurfaceFormat::FormatOption>(), depthBufferSize 24, redBufferSize -1, greenBufferSize -1, blueBufferSize -1, alphaBufferSize -1, stencilBufferSize 8, samples 0, swapBehavior QSurfaceFormat::DefaultSwapBehavior, swapInterval 1, colorSpace QSurfaceFormat::DefaultColorSpace, profile  QSurfaceFormat::NoProfile)
    /tmp/.mount_FreeCA6LHmxP/AppRun: line 43:  6933 Aborted                 (core dumped) ${MAIN} "$@"
```

[This thread](https://forum.freecad.org/viewtopic.php?t=85435&start=10) gave me a good tip for my 11th gen Intel CPU:

```
    LD_PRELOAD=/usr/lib/x86_64-linux-gnu/dri/iris_dri.so ./Your***FreeCAD****.AppImage
```

There's also some more info in [this thread](https://www.linuxquestions.org/questions/slackware-14/freecad-not-starting-4175733563/).

If you think that this is bad advice, contact me somehow and let me know. Cheers!
