---
title: "Master Controller II (PC)"
---

{{% controller-page "vok00106" %}}

This controller has two handles (power and brake, both with adjustable notches), a reverser switch with 3 positions (F, N, B) and 4 buttons (S, A, B, C). It was manufactured by Pony Canyon. It requires external power to work, either with an included power supply or 4 AA-sized batteries. It also supports connecting an included pedal.

It connects to PC via serial cable, either directly via a DE-9 connector or with a USB adapter.

|                  |       |
|------------------|-------|
| **Baud rate**    | 19200 |
| **Data bits**    | 8     |
| **Parity**       | None  |
| **Stop bits**    | 1     |
| **Flow control** | None  |

Unlike other controllers, the notches in the two handles are adjustable. There are two knobs, one on each side of the controller, to adjust the number of power and brake notches. This change can be done with the controller turned off. Next to the power handle there is a LED screen showing the current notch, and the notch print beside the brake handle can also be changed to match the current gear setting.

The power handle supports 3 to 6 notches, plus *EX* (6 notches without click). The brake handle supports 5 to 8 notches, plus *EX* (8 notches without click).

The two handles are interlocked; it is only possible to move one handle at a time.

### Input

The controller sends 5-character events separated by a carriage return (ASCII *0xD*).

Events for the handle are the following.

| Emergency | B8    | B7    | B6    | B5    | B4    | B3    | B2    | B1    |
|:---------:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
| TSB20     | TSB30 | TSB40 | TSE99 | TSA05 | TSA15 | TSA25 | TSA35 | TSA45 |

| N     | P1    | P2    | P3    | P4    | P5    | P6    |
|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|
| TSA50 | TSA55 | TSA65 | TSA75 | TSA85 | TSA95 | TSB60 |

Events for the reverser are the following.

| Backwards | Neutral | Forward |
|:---------:|:-------:|:-------:|
| TSG00     | TSG50   | TSG99   |

Events for the buttons are the following. The first event is reported when the button is pressed, and the second one when the button is released.

| S           | A           | B           | C           |
|:-----------:|:-----------:|:-----------:|:-----------:|
| TSK99/TSK00 | TSX99/TSX00 | TSY99/TSY00 | TSZ99/TSZ00 |

