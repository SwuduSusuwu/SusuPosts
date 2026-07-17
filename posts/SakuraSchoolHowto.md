**\[Preview\] Sakura School Simulator howto**

\[[This post](https://swudususuwu.substack.com/p/sakura-school-island-backdrops-020) allows [all uses](https://creativecommons.org/licenses/by/2.0/).\] \[This post is a work-in-progress.\]

# Table of Contents
- [Intro](#intro)
- [Synopsis + related posts](#synopsis--related-posts)

# Intro
[**Sakura School - Island Backdrops 0.2.0 setup howtos 1/2**](https://swudususuwu.substack.com/p/sakura-school-island-backdrops-020)
    First steps, just shows how to use the Sakura School app to produce small houses.
    \[Notice: this was a visual post, and the [`.mp4`](https://swudususuwu.substack.com/p/ffmpeg-is-floss-no-cost-mux-tool) will not fit into `git`.\]

This post continues into numerous more visual posts:
- [**Sakura School - Island Backdrops 0.2.0 setup howtos 2/2**](https://swudususuwu.substack.com/p/sakura-school-island-backdrops-020-bf7):
    This is an old version of the “_Island Backdrops_” props, was last available to import to Sakura School as prop codes #`7717-0015-7808-22` for version 0.2.0
    Import new props: "`6917-0243-4536-24`" (_Island Backdrops 0.4.3_)
- [**Backdrops 0.2.2 (redoes doors, walls, floors) 1/2**](https://swudususuwu.substack.com/p/sakura-school-island-backdrops-022)
- [**Sakura School - Island Backdrops 0.2.2 (redoes doors, walls, floors) 2/2**](https://swudususuwu.substack.com/p/sakura-school-island-backdrops-022-d95)
- [**Sakura School - Island Backdrops 0.2.2.2 (redoes sakura trees + trapdoors)**](https://swudususuwu.substack.com/p/sakura-school-island-backdrops-0222)
- [**Sakura School howto: 6-axis robots produce house** \[description has howto reuse props\]](https://swudususuwu.substack.com/p/sakura-school-howto-setup-and-use)
  - _Sakura School Simulator_ prop import codes:
    - #"`9417_0676_0249_26`" (*Island Backdrops 0.4.3.4.2*)
    - #"`3517_0711_6043_24`" (*Autonomous Robos 0.2.2.2*)
    - #"`4517_0711_6360_25`" (*Wood Shop Class 0.2.2.4.3*)

New (todo: publish to _SubStack_ + _YouTube_) prop import codes:
- #"`7117_5393_3569_25`" (*Island Backdrops 0.4.6.22*)
- #"`3117_5261_9810_25`" (*Wood Shop Class 0.2.2.4.4*)
- **Sakura School - Wood Shop Class 0.2.4, [z-conflict](https://thecraftsandkitchen.com/how-to-fix-z-fighting-blender/) resolution**
    Import new props: "`21178430147521`" (_Wood Shop Class 0.2.4_)

**Specifics of the tools which those props represent**: the scaffolds use simple linacs, the arms use 2-axis spherical joints socketed into “booms” (cylindrical tubes) with unshown mechanisms to move:
- Recessed orthogonal rubber "rollers" (toothless friction-gears with smooth surfaces) in the tubes can (with torque transferred through friction onto the joints) do those 2-axis motions. Stepper motors (or servos) can cause 1 (or both) rollers to move. If the load requires huge torque, improve the friction-coefficient with: smooth surfaces, plus [_continuous variable transmission_ fluid](https://evolvingsphere.com/understanding-cvt-transmission-fluid-what-you-need-to-know/) (such as [_SantoTrac_](https://santolubes.com/products/santotrac/)).
  - If round (2-axis) rollers are not used; while 1 roller moves, clutches must loosen the 2nd roller (so the 2nd roller does not "stick" (does not do as an automotive calliper on a drum does)).
- Cords (such as those which move puppets) can also do so, but require linear actuators (to mimic myosin, which is fast but more complex) or reels (to extend / retract the cords, which is slow, since fast extension can cause the cords to sag, plus fast retraction causes cord-compression).
- Dual orthogonal 1-axis hinges (such as [*Kuka*'s / *Fanuc*'s tools](https://www.youtube.com/watch?v=hLDbRm-98cs) use) are more simple (direct control of hinge through servo) plus can mimic 2-axis motions, but those look different than the props in this *Sakura School* show. Another problem with those is that the spatial offset (which separates the 2 hinges) prevents true 2-axis moves (although most dual-hinges are so close that this is not an issue for common use).

# Synopsis + related posts
- [Bud, howto setup and use robots shop class](https://swudususuwu.substack.com/p/bud-howto-setup-and-use-robots-shop)
  - [BUD: Arduino/Elegoo Parkour v0.4.6.2, production + walkthrough + hoverboard tour](https://swudususuwu.substack.com/p/bud-arduinoelegoo-parkour-v0462-walkthrough)

- [`./posts/TranscodeMuxHowto.md`](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/TranscodeMuxHowto.md) is simple [`/bin/sh`](https://wikipedia.org/wiki/Bourne_shell) commands for advanced [`ffmpeg`](https://wikipedia.org/wiki/FFmpeg) use.
  - [`https://github.com/SwuduSusuwu/SusuMid.git`](https://github.com/SwuduSusuwu/SusuMid/tree/preview/mid/) has the sounds used.
  - [Programs which give controls to you for 6 (or more) axis moves, through motion capture (camera or IMU) or Bluetooth keyboard](https://swudususuwu.substack.com/p/programs-which-give-6-or-more-axis-controls-to-you)
  - [How to mix Blender with robotics simulators (such as Grasshopper) to produce school classes
@Assistant "Grasshopper versus RoboDK versus V-REP versus Gazebo (plus other such tools)? Which can you use with Blender?"](https://swudususuwu.substack.com/p/how-to-mix-blender-with-robotics)
  - [@Assistant: "Do simulators exist which allow you to move around with the keyboard, but, (as opposed to arrow keys mapped to directions to move + fixed joint/bone animations for the avatar/robot), keys mapped to individual bones?" Yes "Such as?" Unreal Engine, Unity, Virtual Robotics Toolkit, MORSE](https://swudususuwu.substack.com/p/assistant-do-simulators-exist-which)

