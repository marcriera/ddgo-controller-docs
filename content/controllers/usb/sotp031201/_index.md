---
title: "Multi Train Controller (Sony PlayStation 2)"
---

{{% controller-page "sotp031201" %}}

This controller has one handle with variable notches, a D-Pad and 7 buttons (Select, Start, A, B, C, D, ATS). The A button can distinguish between "soft" and "hard" presses. In addition, the controller has four lamps.

Internally, it is a HID device with a vendor-specific class. The reported data depends on the notch cartridge inserted. 

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | *None*                                    |
| **Manufacturer**            | *None*                                    |
| **Vendor ID**               | 0x0AE4<br>0x1C06 (P5/B5)                  |
| **Product ID**              | 0x0101<br>0x77A7 (P5/B5)<br>0x0004 (P5/B8) |
| **Serial number**           | *None*                                    |
| **USB standard descriptor** | [P4/B7](/controllers/usb/descriptors/sotp031201-P4B7_standard-descriptor.txt)<br>[P4/B7 (without B1)](/controllers/usb/descriptors/sotp031201-P4B1B7_standard-descriptor.txt)<br>[P5/B5](/controllers/usb/descriptors/sotp031201-P5B5_standard-descriptor.txt)<br>[P5/B7](/controllers/usb/descriptors/sotp031201-P5B7_standard-descriptor.txt)<br>[P5/B8](/controllers/usb/descriptors/sotp031201-P5B8_standard-descriptor.txt)<br>[P13/B7](/controllers/usb/descriptors/sotp031201-P13B7_standard-descriptor.txt) |
| **HID report descriptor**   | [P4/B7, P4/B2-B7, P5/B7, P13/B7](/controllers/usb/descriptors/sotp031201_hid-report-descriptor.txt) (recreated, not provided by actual device) |

### P5/B5 cartridge

When this cartridge is inserted, the controller emulates the [Train Mascon](/controllers/usb/cotm02001). The buttons are mapped 1:1 except the **D** button, which is mapped to the **Close** (**閉**) button.

The lamps are used as follows, from top to bottom: doors, ATS, 45 and 15.

### P5/B8 cartridge

When this cartridge is inserted, the controller emulates the [Two handle controller "Type 2"](/controllers/usb/tcpp20009). The buttons are mapped 1:1 and **ATS** is mapped to **START**. The reverser is mapped to the D-pad **UP** and **DOWN** buttons.

Only the top lamp is used, for the doors.

### P4/B7, P4/B2-B7, P5/B7, P13/B7 cartridges

When any of these cartridges is inserted, the controller functions similarly to the P5/B5 mode and data changes depending on the amount of notches. The specific cartridge in use can be detected by looking at the *bcdDevice* value from the standard USB descriptor:

| P4/B7  | P4/B2-B7 | P5/B7  |P13/B7  |
|:------:|:--------:|:------:|:------:|
| 0x0300 | 0x0400   | 0x0800 | 0x0A00 |

#### Input

The controller sends reports to the host (PS2) formed by 4 bytes:

| Byte 1 | Byte 2          | Byte 3    | Byte 4    |
|:------:|:---------------:|:---------:|:---------:|
| 0x01   | Reverser+handle | Buttons 1 | Buttons 2 |

The reverser+handle byte combines two values representing the state of the reverser and the power/brake handle. The handle notch is represented sequentially starting from **0x1** (Emergency), brake notches from highest to lowest, *N* and power notches from lowest to highest.

| Forward | Neutral | Backwards |
|:-------:|:-------:|:---------:|
| 0x8X    | 0x0X    | 0x4X      |

**Note:** the P5/B7 and P13/B7 cartridges do not make use of the reverser and use both nibbles for the handle notch.

The first button byte uses six bits to represent the state of the physical buttons. **0** means that the button is released and **1** that it is pressed. A bitmask can be used to retrieve the buttons.

| Button 1 | Button 2 | Button 3 | Button 4 | Button 5 | Button 6 |
|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| ATS      | D        | A (soft) | A (hard) | B        | C        |

The second button byte also uses six bits to represent the state of the physical buttons.

| Button 1 | Button 2 | Button 3 | Button 4 | Button 5 | Button 6 |
|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| START    | SELECT   | UP       | DOWN     | LEFT     | RIGHT    |

#### Output

No details are known regarding internal functioning. 
