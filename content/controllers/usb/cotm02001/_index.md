---
title: "Train Mascon (Sony PlayStation 2)"
---

{{% controller-page "cotm02001" %}}

This controller has one handle (5 power notches and 8+emergency brake notches), a D-Pad and 7 buttons (Select, Start, A, B, C, Close, ATS). The A button can distinguish between "soft" and "hard" presses. In addition, the controller has four lamps: doors, ATS, 45 and 15.

Internally, it is a HID device with a vendor-specific class. The reported data depends on the notch cartridge inserted. 

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | *Unavailable*                             |
| **Manufacturer**            | *Unavailable*                             |
| **Vendor ID**               | 0x1C06                                    |
| **Product ID**              | 0x77A7                                    |
| **Serial number**           | *Unavailable*                             |
| **USB standard descriptor** | *Unavailable*                             |
| **HID report descriptor**   | [Link](/controllers/usb/descriptors/cotm02001_hid-report-descriptor.txt) (recreated, not provided by actual device) |

### Input

The controller sends reports to the host (PS2) formed by 4 bytes:

| Byte 1 | Byte 2          | Byte 3    | Byte 4    |
|:------:|:---------------:|:---------:|:---------:|
| 0x01   | Reverser+handle | Buttons 1 | Buttons 2 |

The reverser+handle byte combines two values representing the state of the reverser and the power/brake handle. The handle notch is represented sequentially starting from **0x1** (Emergency), brake notches from highest to lowest, *N* and power notches from lowest to highest.

| Forward | Neutral | Backwards |
|:-------:|:-------:|:---------:|
| 0x2X    | 0x0X    | 0x1X      |

The first button byte uses six bits to represent the state of the physical buttons. **0** means that the button is released and **1** that it is pressed. A bitmask can be used to retrieve the buttons.

| Button 1 | Button 2 | Button 3 | Button 4 | Button 5 | Button 6 |
|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| ATS      | Close    | A (soft) | A (hard) | B        | C        |

The second button byte also uses six bits to represent the state of the physical buttons.

| Button 1 | Button 2 | Button 3 | Button 4 | Button 5 | Button 6 |
|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| START    | SELECT   | UP       | DOWN     | LEFT     | RIGHT    |

### Output

No details are known regarding internal functioning. 


