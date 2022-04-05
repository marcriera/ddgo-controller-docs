---
title: "Adapters and hacks"
weight: 3
---

Besides the official compatibility, it is possible to use unofficial adapters, tools and hacks to use controllers with games which is unsupported officially.

## Converter tool by Autotraintas

[Autotraintas](https://autotraintas.hariko.com) has created a tool that makes it possible to use nearly any Densha de GO! controller with the PC versions of the games. This includes the classic console controllers (USB adapter required) and the USB controllers for the PlayStation 2. The tool patches the game memory on the fly to reflect the input from the controller.

## PlayStation 2 cheat codes for PlayStation controllers

While **Densha de GO! 3** and **Densha de GO! Shinkansen** officially support the original (non-USB) PlayStation controllers, other games are only compatible with USB controllers. Via cheat codes, it is possible to use the original PlayStation controllers on real hardware, either with retail discs or via OPL.

The codes emulate a Type 2 controller. You will need to connect the controller as follows:

- Port 1: Dualshock or Dualshock 2 (D-pad, **SELECT**)
- Port 2: PlayStation controller (handles and buttons, **SELECT** is mapped to **D**)

**Note:** Other controllers may be used like this with an adapter (Titan One/Two + Brook/PADEMU). In this case, buttons are not remapped and the Dualshock on port 1 is not needed. [More information](https://github.com/MarcRiera/ddgo-scripts/tree/main/Densha%20de%20GO!%20(PS1-PS2))

Each game requires a specific cheat code:

- [Densha de GO! Ryojouhen](cheats/controller-cheat_ryojouhen.txt)
- [Densha de GO! Professional 2](cheats/controller-cheat_pro2.txt)
- [Densha de GO! Professional 2 (Taito Best)](cheats/controller-cheat_pro2best.txt)
- [Densha de GO! Final](cheats/controller-cheat_final.txt)

There are also cheat codes available for games in the **Train Simulator** series, emulating a Multi Train Controller (MTC):

- [Train Simulator: Midosuji Line](cheats/controller-cheat_midosuji.txt)
- [Train Simulator + Densha de GO!](cheats/controller-cheat_tsddgo.txt)

For retail discs, the codes can be loaded with [ps2rd](https://github.com/mlafeldt/ps2rd) or [Cheat Device](https://github.com/root670/CheatDevicePS2). If you are using OPL, it already includes ps2rd and you just need to copy the codes and enable cheats.

## Input plugins for BVE Trainsim/OpenBVE

BVE Trainsim and OpenBVE both support **input plugins**, which allow expanding the controllers compatible with the program.

BVE Trainsim requires installing external input plugins, depending on the controller:

- [Classic controllers](http://saha209kame.web.fc2.com/BVE_ATSPI.html) (電GO PS - JC_PS101Uインターフェイス/電GO PS - JC_PS201Uインターフェイス by saha209, USB adapter required)
- [DGC-255/DGOC-44U/DRC-184](http://saha209kame.web.fc2.com/BVE_ATSPI.html) (電GO PCインターフェイス by saha209)
- [TCPP-20009/TCPP-20014/MTC with P5/B8 cassette](http://saha209kame.web.fc2.com/BVE_ATSPI.html) (電GO PS2インターフェイス by saha209)
- [MTC (other cassettes)](http://saha209kame.web.fc2.com/BVE_ATSPI.html) (TrainSimulator PS2 MultiTrainController(MTC)インターフェイス by saha209)
- [ZKNS-001](http://saha209kame.web.fc2.com/BVE_ATSPI.html) (電GO SWインターフェイス by saha209)
- [OHC-PC01](http://www.konkyu.net/SanYingControllerInterface.aspx)

OpenBVE includes built-in input plugins for all classic and USB Densha de GO! controllers, the MTC with P5/B8 cassette and the OHC-PC01. They can be enabled and configured in the program's settings. Note that a USB adapter is required for classic controllers.
