**_Sakura School Simulator_ howto load (plus use) assets**

\[[This post](./SakuraSchoolHowto.md) is [released through *Creative Commons Generic Attribution 2* (which allows all uses)](https://creativecommons.org/licenses/by/2.0/).\] \[This post is a work-in-progress.\] \[**Notice**: am not affiliated to *Sakura School Simulator*, am just a user.\]

# Table of Contents
- [Discussion](#discussion)
- [Synopsis + resources](#synopsis--resources)

******************************************
# Discussion
[**_Sakura School_: how _Island Backdrops 0.2.0_ (ground floor) was produced**](https://swudususuwu.substack.com/p/sakura-school-island-backdrops-020)
    First steps, just shows how to use the Sakura School app to produce small houses.
    \[Notice: this was a visual post, since the [`.mp4`](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/TranscodeMuxHowto.md#produce-mp4) is too large for `git`.\]

******************************************

This post continues into numerous more visual posts:
- [**_Sakura School_: how _Island Backdrops 0.2.1_ (roof) was produced**](https://swudususuwu.substack.com/p/sakura-school-island-backdrops-020-bf7):
    This is an old version of the “_Island Backdrops_” props, was last available to import to Sakura School as prop codes #`7717-0015-7808-22` for version 0.2.0
    Import new props: "`6917-0243-4536-24`" (_Island Backdrops 0.4.3_)
- [**_Sakura School_: how _Island Backdrops 0.2.2_ was produced 1/2 (improves doors, walls, floors)**](https://swudususuwu.substack.com/p/sakura-school-island-backdrops-022)
- [**_Sakura School_: how _Island Backdrops 0.2.2_ was produced 2/2 (roof)**](https://swudususuwu.substack.com/p/sakura-school-island-backdrops-022-d95)
- [**_Sakura School_: how _Island Backdrops 0.2.2.2_ was produced (improves positions of plants + trapdoors)**](https://swudususuwu.substack.com/p/sakura-school-island-backdrops-0222)
- [**_Sakura School_: how to import+use 6-axis tools**](https://swudususuwu.substack.com/p/sakura-school-howto-setup-and-use)
  - _Sakura School Simulator_ prop import codes:
    - #"`9417_0676_0249_26`" (*Island Backdrops 0.4.3.4.2*)
    - #"`3517_0711_6043_24`" (*Autonomous Robos 0.2.2.2*)
    - #"`4517_0711_6360_25`" (*Wood Shop Class 0.2.2.4.3*)

New (todo: publish to _SubStack_ + _YouTube_) prop import codes:
- #"`7117_5393_3569_25`" (*Island Backdrops 0.4.6.22*)
- #"`7917_5946_3840_25`" (*Island Backdrops 0.4.6.24*) *notice*: not asymptotic improve (unlike most new versions), but has "tradeoffs". Will consider to drop this version.
- #"`3117_5261_9810_25`" (*Wood Shop Class 0.2.2.4.4*)
- #"`2317_6982_8591_30`" (*Hous + Shop Class + autonomous*)
- #"`7217_6982_8705_24`" (*Autonomous Robos 0.2.2.2*)

******************************************

**Specifics of the tools which those props represent**: the scaffolds use simple linacs, the arms use 2-axis spherical joints socketed into “booms” (cylindrical tubes) with unshown mechanisms to move:
- Recessed orthogonal rubber "rollers" (toothless friction-gears with smooth surfaces) in the tubes can (with torque transferred through friction onto the joints) do those 2-axis motions. [Stepper motors (or servos)](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md#own-lists) can cause 1 (or both) rollers to move. If the load requires huge torque, improve the friction-coefficient with: smooth surfaces, plus [_continuous variable transmission_ fluid](https://evolvingsphere.com/understanding-cvt-transmission-fluid-what-you-need-to-know/) (such as [_SantoTrac_](https://santolubes.com/products/santotrac/)).
  - If round (2-axis) rollers are not used; while 1 roller moves, clutches must loosen the 2nd roller (so the 2nd roller does not "stick" (does not do as an automotive calliper on a drum does)).
- Cords (such as those which move puppets) can also do so, but require linear actuators (to mimic myosin, which is fast but more complex) or reels (to extend / retract the cords, which is slow, since fast extension can cause the cords to sag, plus fast retraction causes cord-compression).
- Dual orthogonal 1-axis hinges (such as [*Kuka*'s / *Fanuc*'s tools](https://www.youtube.com/watch?v=hLDbRm-98cs) use) are more simple (direct control of hinge through servo) plus can mimic 2-axis motions, but those look different than the props in this *Sakura School* show. Another problem with those is that the spatial offset (which separates the 2 hinges) prevents true 2-axis moves (although most dual-hinges are so close that this is not an issue for common use).

******************************************

Not affiliated to specific vendors/manufacturers; just published thus lists so our world improves
* [Source code for autonomous Arduino or Elegoo tools (includes lists of suitable components, such as servos)](https://github.com/SwuduSusuwu/SubStack/blob/preview/posts/ArduinoElegooTools.md)
* [1000**W** servos for around $162](https://www.amazon.com/s?k=1000w+servo&rh=n%3A16310091) should allow numerous individuals to produce autonomous tools.

******************************************
# Synopsis + resources
- [**_BUD: Create 1.0_, _Arduino/Elegoo Parkour_**](https://swudususuwu.substack.com/p/bud-howto-setup-and-use-robots-shop)
  - [**_BUD_: _Arduino/Elegoo Parkour v0.4.6.2_**, production + walkthrough + hoverboard tour](https://swudususuwu.substack.com/p/bud-arduinoelegoo-parkour-v0462-walkthrough)

- [`./posts/TranscodeMuxHowto.md`](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/TranscodeMuxHowto.md) is simple [`/bin/sh`](https://wikipedia.org/wiki/Bourne_shell) commands for advanced [`ffmpeg`](https://wikipedia.org/wiki/FFmpeg) transcoder use.
  - [`https://github.com/SwuduSusuwu/SusuMid.git`](https://github.com/SwuduSusuwu/SusuMid/tree/preview/mid/) has the sounds used.
- [Programs which give controls to you for 6 (or more) axis moves, through motion capture (camera or **IMU**) or *Bluetooth* keyboard](https://swudususuwu.substack.com/p/programs-which-give-6-or-more-axis-controls-to-you)
  - [How to mix *Blender* with robotics simulators (such as *Grasshopper*) to produce school classes](https://swudususuwu.substack.com/p/how-to-mix-blender-with-robotics)
  - [@Assistant: "Do simulators exist which allow you to move around with the keyboard, but, (as opposed to arrow keys mapped to directions to move + fixed joint/bone animations for the avatar/robot), keys mapped to individual bones?" Yes "Such as?" *Unreal Engine*, *Unity*, *Virtual Robotics Toolkit*, **MORSE**](https://swudususuwu.substack.com/p/assistant-do-simulators-exist-which)

- [Automated modular housing construction by KUKA - representing a social milestone](https://www.youtube.com/watch?v=PyxGis7Pl80) shows some autonomous tools which produce modules of houses. Good to know that a few of us wish the world improves.
