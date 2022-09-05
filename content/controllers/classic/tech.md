---
title: "Classic controllers - Technical details"
weight: 1
hidden: true
---

Internally, these controllers use the same protocol as a standard controller for the corresponding console and input is reported in the data bytes corresponding to buttons (where each bit reports the state of a single button). Only the regular physical buttons have dedicated bits for them; the handles combine three and four bits for the power notches and brake notches, respectively (you can find an example with the Nintendo 64 [here](https://sites.google.com/site/consoleprotocols/home/nintendo-joy-bus-documentation/n64-specific/train-controller)).

## Power handle bit usage

The power handle uses a combination of three bits (buttons) to represent each notch.

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

The brake handle uses a combination of four bits (buttons) to represent each notch.

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

The unmarked positions can be found between **B8** and **Emergency** and produce no click when moving the handle.

## Button mapping to a standard controller

Because they use the same data bytes, the input between a Densha de GO! controller and a standard controller for each console can be matched as follows:

| Densha de GO! | Nintendo 64 | Sony PlayStation 1 | Sega Dreamcast | Sega Saturn |
|:-------------:|:-----------:|:------------------:|:--------------:|:-----------:|
| SELECT        | R           | SELECT             | D              | ??          |
| START         | START       | START              | START          | START       |
| A             | B           | SQUARE             | A              | A           |
| B             | A           | CROSS              | ??             | B           |
| C             | L           | CIRCLE             | C              | C           |
| POWER 1       | RIGHT       | TRIANGLE           | Z              | X           |
| POWER 2       | UP          | LEFT               | Y              | Y           |
| POWER 3       | Z           | RIGHT              | X              | Z           |
| BRAKE 1       | C RIGHT     | L1                 | UP             | L           |
| BRAKE 2       | C LEFT      | L2                 | DOWN           | R           |
| BRAKE 3       | C DOWN      | R1                 | LEFT           | DOWN        |
| BRAKE 4       | C UP        | R2                 | RIGHT          | LEFT        |

This can be used with a USB adapter to read the controller input from a PC.
