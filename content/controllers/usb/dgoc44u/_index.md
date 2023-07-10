---
title: "Two handle controller (PC)"
---

{{% controller-page "dgoc44u" %}}

This controller has two handles (5 power notches and 8+emergency brake notches) and 6 buttons (Select, Start, A, B, C, D).

Internally, it is a HID-compliant joystick with two axes and 6 buttons (the handle positions are reported via axes).

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | 電車でGO! コントローラ USB版                  |
| **Manufacturer**            | TAITO                                     |
| **Vendor ID**               | 0x0AE4                                    |
| **Product ID**              | 0x0003                                    |
| **Serial number**           | TCPP20009                                 |
| **USB standard descriptor** | [Link](/controllers/usb/descriptors/dgoc44u_standard-descriptor.txt) |
| **HID report descriptor**   | [Link](/controllers/usb/descriptors/dgoc44u_hid-report-descriptor.txt) |

The controller sends reports to the host (PC) formed by 6 bytes:

| Byte 1 | Byte 2 | Byte 3 | Byte 4  | Byte 5 | Byte 6 |
|:------:|:------:|:------:|:-------:|:------:|:------:|
| Brake  | Power  | Null   | Buttons | Null   | Null   |

The values for the brake notch byte are the following. There are 5 unmarked positions between **B8** and **Emergency**, but unlike classic controllers, they are all report the value for **Emergency**.

| Released | B1   | B2   | B3   | B4   | B5   | B6   | B7   | B8   | Emergency | Transition |
|:--------:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:---------:|:----------:|
| 0x79     | 0x8A | 0x94 | 0x9A | 0xA2 | 0xA8 | 0xAF | 0xB2 | 0xB5 | 0xB9      | 0xFF       |

The values for the power notch byte are listed below.

| N    | P1   | P2   | P3   | P4   | P5   | Transition |
|:----:|:----:|:----:|:----:|:----:|:----:|:----------:|
| 0x81 | 0x6D | 0x54 | 0x3F | 0x21 | 0x00 | 0xFF       |

The button byte uses six bits to represent the state of the physical buttons. **0** means that the button is released and **1** that it is pressed.

| Button 1 | Button 2 | Button 3 | Button 4 | Button 5 | Button 6 |
|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| B        | A        | C        | D        | SELECT   | START    |
