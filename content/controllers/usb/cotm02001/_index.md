---
title: "Train Mascon (Sony PlayStation 2)"
---

{{% controller-page "cotm02001" %}}

This controller has one handle (5 power notches and 8+emergency brake notches), a D-Pad and 7 buttons (Select, Start, A, B, C, Close, ATS). The A button can distinguish between "soft" and "hard" presses. In addition, the controller has four lamps: doors, ATS, 45 and 15.

Internally, it is a vendor-specific class device. 

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | *Unavailable*                             |
| **Manufacturer**            | *Unavailable*                             |
| **Vendor ID**               | 0x1C06                                    |
| **Product ID**              | 0x77A7                                    |
| **Serial number**           | *Unavailable*                             |
| **USB standard descriptor** | [Link](/controllers/usb/descriptors/sotp031201-P5B5_standard-descriptor.txt) from Multi Train Controller |
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

| Bit 0 | Bit 1 | Bit 2    | Bit 3    | Bit 4 | Bit 5 |
|:-----:|:-----:|:--------:|:--------:|:-----:|:-----:|
| ATS   | Close | A (soft) | A (hard) | B     | C     |

The second button byte also uses six bits to represent the state of the physical buttons.

| Bit 0 | Bit 1  | Bit 2 | Bit 3 | Bit 4 | Bit 5 |
|:-----:|:------:|:-----:|:-----:|:-----:|:-----:|
| START | SELECT | UP    | DOWN  | LEFT  | RIGHT |

### Output

The controller supports receiving data via a control transfer to turn on/off the lamps. The setup packet is as follows:

| bmRequestType | bRequest | wValue    | wIndex | wLength |
|:-------------:|:--------:|:---------:|:------:|:-------:|
| 0x40          | 0x50     | Lamp data | 0x0000 | 0x0000  |

Changing *wValue* controls the lamps with the logic below.

* **Door lamp:** **0x0X** is **Off**, **0x1X** is **On**.
* **Signal lamp:** **0xX0** is **Off**, **0xX1** is **ATS**, **0xX2** is **45**, **0xX3** is **15**.
