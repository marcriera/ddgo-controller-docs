---
title: "PlayStation 2 cheat codes"
weight: 3
---

## Overview

While **Densha de GO! 3** and **Densha de GO! Shinkansen** officially support the original (non-USB) PlayStation controllers, other games are only compatible with USB controllers. Via cheat codes, it is possible to use the original PlayStation controllers on real hardware, either with retail discs or via OPL.

The codes emulate a Type 2 controller. You will need to connect the controller as follows:

- Port 1: Dualshock or Dualshock 2 (D-pad, **SELECT**)
- Port 2: PlayStation controller (handles and buttons, **SELECT** is mapped to **D**)

{{% notice note %}}
Other controllers may be used like this with an adapter (Titan One/Two + Brook/PADEMU). In this case, buttons are not remapped and the Dualshock on port 1 is not needed. [More information](https://github.com/MarcRiera/ddgo-scripts/tree/main/Densha%20de%20GO!%20(PS1-PS2))
{{% /notice %}}

Each game requires a specific cheat code:

- [Densha de GO! Ryojouhen](controller-cheat_ryojouhen.txt)
- [Densha de GO! Professional 2](controller-cheat_pro2.txt)
- [Densha de GO! Professional 2 (Taito Best)](controller-cheat_pro2best.txt)
- [Densha de GO! Final](controller-cheat_final.txt)

There are also cheat codes available for games in the **Train Simulator** series, emulating a Multi Train Controller (MTC):

- [Train Simulator: Midosuji Line](controller-cheat_midosuji.txt)
- [Train Simulator + Densha de GO!](controller-cheat_tsddgo.txt)

For retail discs, the codes can be loaded with [ps2rd](https://github.com/mlafeldt/ps2rd) or [Cheat Device](https://github.com/root670/CheatDevicePS2). If you are using OPL, it already includes ps2rd and you just need to copy the codes and enable cheats.

## Technical description

These cheat codes have become possible after disassembling and inspecting each game with [Ghidra](https://ghidra-sre.org/) and the [ghidra-emotionengine](https://github.com/beardypig/ghidra-emotionengine) plugin. The format of cheat codes is described [here](https://github.com/root670/CheatDevicePS2/wiki/Code-Types).

Here you can find a commented version of the cheat code for ***Densha de GO! Professional 2 (Taito Best)***. Input data is copied to 0xFE000 (two bytes for button data and one byte for D-pad data) before processing.

```
202D3CAC 00000000 // By default, set number of connected USB devices to 0
D02DBA32 58010001 // If there's a controller connected to P2, run the following 0x58 lines (everything)
502DB9C2 00000002 // Copy button data to 0xFE000
000FE000 00000000
D00FE000 55400050 // If the controller in P2 has UP+DOWN pressed, run the following 0x55 lines (everything)
203790F0 40000202 // Set USB controller model to Type 2
202D3CAC 00000001 // Set number of connected USB devices to 1

// Remapping
D02DB9C1 07010041 // If the controller in P2 is a digital gamepad (PS1 mascon), run the following 0x7 lines
D00FE000 01400001 // Remap SELECT to L3 (for use as "D")
700FE000 00500002
700FE000 00100001 // Clear SELECT
D02DBAC2 01400001 // Remap P1 SELECT to SELECT
700FE000 00500001
502DBAC2 00000001 // Remap P1 D-pad to D-pad
000FE002 00000000
D02DB9C1 09010073 // If the controller in P2 is a Dualshock (mascon connected via adapter or PADEMU), run the following 0x9 lines
000FE002 000000FF // Clear D-pad data
D02DB9C6 01010000 // LEFT
700FE002 00400080
D02DB9C6 010100FF // RIGHT
700FE002 00400020
D02DB9C7 01010000 // UP
700FE002 00400010
D02DB9C7 010100FF // DOWN
700FE002 00400040

// Buttons
2012BDC0 34420000 // ASM patch (disables game function that reads input from P2)
003794C6 00000000 // Clear button data for Type 2 controller
D00FE000 01408000 // A
703794C6 00000002
D00FE000 01404000 // B
703794C6 00000001
D00FE000 01402000 // C
703794C6 00000004
D00FE000 01400002 // D (L3)
703794C6 00000008
D00FE000 01400008 // START
703794C6 00000020
D00FE000 01400001 // SELECT
703794C6 00000010

// D-Pad
D00FE002 010100EF // N
003794C5 00000000
D00FE002 010100CF // NE
003794C5 00000001
D00FE002 010100DF // E
003794C5 00000002
D00FE002 0101009F // SE
003794C5 00000003
D00FE002 010100BF // S
003794C5 00000004
D00FE002 0101003F // SW
003794C5 00000005
D00FE002 0101007F // W
003794C5 00000006
D00FE002 0101006F // NW
003794C5 00000007
D00FE002 010100FF // CENTER
003794C5 00000008

// Power handle
D00FE000 01401000 // P5
003794C3 00000005
D00FE000 01400080 // P4
003794C3 00000004
D00FE000 01401080 // P3
003794C3 00000003
D00FE000 01400020 // P2
003794C3 00000002
D00FE000 01401020 // P1
003794C3 00000001
D00FE000 014000A0 // P0
003794C3 00000000

// Brake handle
700FE000 00300F00 // Bitmask: discard all button data besides the 4 bits for brake notches
D00FE000 01000F00 // EB
003794C2 00000009
D00FE000 01000600 // B8
003794C2 00000008
D00FE000 01000200 // B7
003794C2 00000007
D00FE000 01000D00 // B6
003794C2 00000006
D00FE000 01000900 // B5
003794C2 00000005
D00FE000 01000C00 // B4
003794C2 00000004
D00FE000 01000800 // B3
003794C2 00000003
D00FE000 01000500 // B2
003794C2 00000002
D00FE000 01000100 // B1
003794C2 00000001
D00FE000 01000400 // B0
003794C2 00000000
```

### Memory addresses

|                                    | Professional 2 (Taito Best) | Professional 2 | Ryojōhen  | Final    | Notes                                                                       |
|:-----------------------------------|:----------------------------|:---------------|:----------|:---------|:----------------------------------------------------------------------------|
| **USB mascon count (int32)**       | 0x2D3CAC                    | 0x2C852C       | 0x24B6DC  | 0x2C1464 |                                                                             |
| **USB mascon model (int32)**       | 0x3790F0                    | 0x36EAF0       | 0x2F24E0  | 0x3DEA10 | 0x40000202=Type 2                                                           |
| **Type 2 brake notch (byte)**      | 0x3794C2                    | 0x36EEC2       | 0x2F28C2  | 0x3DF242 | Preprocessed, 0 to 9                                                        |
| **Type 2 power notch (byte)**      | 0x3794C3                    | 0x36EEC3       | 0x2F28C3  | 0x3DF243 | Preprocessed, 0 to 5                                                        |
| **Type 2 D-pad data (byte)**       | 0x3794C5                    | 0x36EEC5       | 0x2F28C5  | 0x3DF245 | Raw USB data                                                                |
| **Type 2 button data (byte)**      | 0x3794C6                    | 0x36EEC6       | 0x2F28C6  | 0x3DF246 | Raw USB data                                                                |
| **P2 controller connected (byte)** | 0x2DBA32                    | 0x2D14F2       | 0x2548F2  | 0x2C8172 | 0x00=Disconnected, 0x01=Connected                                           |
| **P2 controller type (byte)**      | 0x2DB9C1                    | 0x2D1481       | 0x254881  | 0x2C8101 | 0x41=Digital, 0x73=Dualshock                                                |
| **P2 button input (int16)**        | 0x2DB9C2                    | 0x2D1482       | 0x254882  | 0x2C8102 |                                                                             |
| **P2 L-stick input (int16)**       | 0x2DB9C6                    | 0x2D1486       | 0x254886  | 0x2C8106 |                                                                             |
| **P1 button input (int16)**        | 0x2DBAC2                    | 0x2D1582       | 0x254982  | 0x2C8202 |                                                                             |
| **ASM patch**                      | 0x12BDC0                    | 0x12CB60       | 0x135B90  | 0x148928 | Leftover game code binds the C button to the horn and needs to be disabled. |
