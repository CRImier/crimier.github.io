---
layout: post
title: Va-11 Hall-A Julianna game achievement - 30FPS limit on Linux
---

Ever went for 100% completion on a game? Recently, I've replayed Va11 Hall-A, it's been a joy. I decided to go for 100% - by the way,
[this guide](https://www.trueachievements.com/a314924/employee-of-the-month-achievement#oSolutions) has been genuinely wonderful
and a must-read if you want to 100% it quickly. 

There was just one achievement left - [named `In the name of beauty!`](https://www.trueachievements.com/a314920/in-the-name-of-beauty-achievement),
requiring a win in the Model Warrior Julianne game. It's a tough one to win if you don't play those kinds of games.

There's [a video](https://www.youtube.com/watch?v=WqaXkjp0pDU) that shows you a way to cheese the game.

However, if you were to try it, you'd quickly find that you need to set the video playback speed to 2x to match the game rate.
Why's that? Apparently, VA11 Hall-A sped up the game from 30FPS to 60FPS at some point. A welcome development for the game, but,
this change 2x sped up the Julianna game, too, as the comments point out. This is obviously not fair.

There's a fix to limit game FPS on Proton games - put `DXVK_FRAME_RATE=30 %command%` in your launch options. Problem?
The game runs on Linux [natively](https://www.protondb.com/app/447530?device=steamDeck), which means Proton is not involved.
By default, when you install the game on Linux, it uses one of the uhhh native Steam runtimes? Something something `scout` or `soldier`.

You can switch it to run on Proton in settings, and it runs beautifully. Even the 30FPS limit works! Last problem? Your saves
will not appear in the game main menu, which'd normally mean that you'd need to replay the whole game up until you can buy the PC and cartridges. Not good!

Worry not, you haven't lost your saves. It's simply that native Linux version stores them in your home directory, 
and the Proton version stores them in the Wine prefix. Here's a console command to solve this:

```bash
cp ~/.config/VA_11_Hall_A/saves/* ~/.steam/steam/steamapps/compatdata/447530/pfx/drive_c/users/steamuser/AppData/Local/VA_11_Hall_A/saves/
```

Naturally, your Proton saves will not get synced back. For what it's worth, maybe a symlink will work here - this exercise left up to the reader.

This was the last thing I needed to to limit game FPS to 30 and finally get the Model Warrior Julianna completion achievement on Linux
without fighting the game at 2x speed.

If you think that this is bad advice, contact me somehow and let me know. Cheers!
