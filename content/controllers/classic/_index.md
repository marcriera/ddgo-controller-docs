---
title: "Classic consoles"
weight: 1
alwaysopen: false
---

The information in this section applies to the following controllers:

- **SLPH-00051:** two-handle controller (Sony PlayStation)
- **TC-5175290:** two-handle controller (Sega Saturn)
- **TCPP-20001:** single-handle controller (Sony PlayStation)
- **TCPP-20002:** gamepad controller (Sony PlayStation)
- **TCPP-20003:** two-handle controller (Nintendo 64)
- **TCPP-20004:** two-handle controller (Sega Dreamcast)
- **TCPP-20008:** two-handle controller, golden (Sony PlayStation)

These controllers all have five physical buttons (**SELECT**, **START**, **A**, **B**, **C**) and two handles (with the TCPP-20001 combining them into one). Internally, they use the same protocol as a standard controller for the corresponding console and input is reported in the data bytes corresponding to buttons (where each bit reports the state of a single button). Only the regular physical buttons have dedicated bits for them; the handles combine three and four bits for the power notches and brake notches, respectively (you can find an example with the Nintendo 64 [here](https://sites.google.com/site/consoleprotocols/home/nintendo-joy-bus-documentation/n64-specific/train-controller)).

## Power handle bit usage

The power handle uses a combination of three bits (buttons) to represent each notch. When using the TCPP-20001 controller, the equivalent of **N** is reported for power whenever a brake notch is applied.

| Position   | POWER 1 | POWER 2 | POWER 3 |
|:----------:|:-------:|:-------:|:-------:|
| N          | -       | X       | X       |
| P1         | X       | -       | X       |
| P2         | -       | -       | X       |
| P3         | X       | X       | -       |
| P4         | -       | X       | -       |
| P5         | X       | -       | -       |
| Transition | -       | -       | -       |

## Brake handle bit usage

The brake handle uses a combination of four bits (buttons) to represent each notch. When using the TCPP-20001 controller, the equivalent of **Released** is reported for brake whenever a power notch is applied.

| Position   | BRAKE 1 | BRAKE 2 | BRAKE 3 | BRAKE 4 |
|:----------:|:-------:|:-------:|:-------:|:-------:|
| Released   | -       | X       | X       | X       |
| B1         | X       | -       | X       | X       |
| B2         | -       | -       | X       | X       |
| B3         | X       | X       | -       | X       |
| B4         | -       | X       | -       | X       |
| B5         | X       | -       | -       | X       |
| B6         | -       | -       | -       | X       |
| B7         | X       | X       | X       | -       |
| B8         | -       | X       | X       | -       |
| Unmarked 1 | X       | -       | X       | -       |
| Unmarked 2 | -       | -       | X       | -       |
| Unmarked 3 | X       | X       | -       | -       |
| Unmarked 4 | -       | X       | -       | -       |
| Unmarked 5 | X       | -       | -       | -       |
| Emergency  | -       | -       | -       | -       |
| Transition | X       | X       | X       | X       |

The unmarked positions can be found between **B8** and **Emergency** and produce no click when moving the handle. When using the TCPP-20001 or the TCPP-20002, only the first and fourth unmarked positions are available.

## Button mapping to a standard controller

Because they use the same data bytes, the input between a Densha de GO! controller and a standard controller for each console can be matched as follows:

| Densha de GO! | Nintendo 64 | Sony PlayStation 1 | Sega Dreamcast | Sega Saturn |
|:-------------:|:-----------:|:------------------:|:--------------:|:-----------:|
| SELECT        | R           | SELECT             | D              | ??          |
| START         | START       | START              | START          | ??          |
| A             | B           | SQUARE             | A              | ??          |
| B             | A           | CROSS              | ??             | ??          |
| C             | L           | CIRCLE             | C              | ??          |
| POWER 1       | RIGHT       | TRIANGLE           | Z              | X           |
| POWER 2       | UP          | LEFT               | Y              | Y           |
| POWER 3       | Z           | RIGHT              | X              | Z           |
| BRAKE 1       | C RIGHT     | L1                 | UP             | L           |
| BRAKE 2       | C LEFT      | L2                 | DOWN           | R           |
| BRAKE 3       | C DOWN      | R1                 | LEFT           | DOWN        |
| BRAKE 4       | C UP        | R2                 | RIGHT          | LEFT        |

This is useful when using a USB adapter to read the controller input from a PC.

## PlayStation-specific information

The controllers report the same data amount and structure as a standard digital PlayStation controller. UP and DOWN are pressed permanently. The games detect the controllers with these two buttons, as it is an impossible combination with a standard  digital controller.
