---
title: "Master Controller (PC)"
---

{{% controller-page "vok00105" %}}

This controller has one handle (with adjustable notches), a reverser switch with 3 positions (F, N, B) and 4 buttons (S, A, B, C). It was manufactured by Pony Canyon. It requires external power to work, either with an included power supply or 4 AA-sized batteries.

It connects to PC via serial cable, either directly via a DE-9 connector or with a USB adapter.

|                  |       |
|------------------|-------|
| **Baud rate**    | 19200 |
| **Data bits**    | 8     |
| **Parity**       | None  |
| **Stop bits**    | 1     |
| **Flow control** | None  |

Unlike other controllers, the notches in the combined power-brake handle are adjustable. On the underside of the controller there are a sliding switch, as well as a window with dip switches, to change gears. This change can be done with the controller turned off. The notch print beside the handle can also be changed to match the current gear setting.

The are 8 possible gear settings:

|               | **Type A** | **Type B** | **Type C** | **Type D** | **Type E** | **Type F** | **Type G** | **Type H**   |
|---------------|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:----------:|:------------:|
| Power notches | 4          | 3          | 5          | 4          | 4          | 5          | 5          | 6 (no click) |
| Brake notches | 5          | 7          | 5          | 7          | 8          | 8          | 7          | 8 (no click) |

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
