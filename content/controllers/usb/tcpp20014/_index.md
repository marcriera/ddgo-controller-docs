---
title: "Ryojōhen controller (Sony PlayStation 2)"
---

{{% controller-page "tcpp20014" %}}

This controller has two handles (4 power notches and an analogue brake handle with three areas), a D-Pad and 7 buttons (Select, Start, Horn, Announce, Camera, Left doors, Right doors). In addition, it provides a 3.5 mm jack connector to plug a horn pedal.

Internally, it is a HID device with a vendor-specific class.

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | TAITO_DENSYA_CON_T03                      |
| **Manufacturer**            | TAITO                                     |
| **Vendor ID**               | 0x0AE4                                    |
| **Product ID**              | 0x0007                                    |
| **Serial number**           | TCPP20014                                 |
| **USB standard descriptor** | [Link](/controllers/usb/descriptors/tcpp20014_standard-descriptor.txt) |
| **HID report descriptor**   | [Link](/controllers/usb/descriptors/tcpp20014_hid-report-descriptor.txt) (recreated, not provided by actual device) |

### Input

The controller sends reports to the host (PS2) formed by 8 bytes:

| Byte 1 | Byte 2 | Byte 3 | Byte 4 | Byte 5  | Bytes 6-8 |
|:------:|:------:|:------:|:------:|:-------:|:---------:|
| Brake  | Power  | Pedal  | D-Pad  | Buttons | Unused    |

Unlike traditional controllers, the brake handle is analogue and the brake byte reflects the position of the handle precisely. There are three areas with the ranges listed below, plus the emergency notch.

| Reduce pressure | Keep pressure | Increase pressure | Emergency |
|:---------------:|:-------------:|:-----------------:|:---------:|
| 0x23-0x64       | 0x65-0x89     | 0x8A-0xD6         | 0xD7      |

When using the controller with **Densha de GO! Professional 2** or **Densha de GO! Final**, the brake handle is interpreted as having 6 brake notches + emergency. The aproximate byte range for each notch is listed below (taken from **Densha de GO! Professional 2**).

| Released  | B1        | B2        | B3        | B4        | B5        | B6        | Emergency |
|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|
| 0x23-0x2A | 0x2B-0x3C | 0x3D-0x4E | 0x4F-0x63 | 0x64-0x8A | 0x8B-0xB0 | 0xB1-0xD6 | 0xD7      |

The values for the power notch byte are listed below.

| N    | P1   | P2   | P3   | P4   | Transition |
|:----:|:----:|:----:|:----:|:----:|:----------:|
| 0x00 | 0x3C | 0x78 | 0xB4 | 0xF0 | 0xFF       |

The pedal byte has two possible values depending on the state of the pedal.

| Released | Pressed |
|:--------:|:-------:|
| 0xFF     | 0x00    |

The D-pad byte represents the state of the arrow buttons. If two opposite directions are pressed simultaneously, the result is **Center** unless a third button is pressed.

| N    | NE   | E    | SE   | S    | SW   | W    | NW   | None/Center |
|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:-----------:|
| 0x00 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08        |

The button byte uses seven bits to represent the state of the physical buttons. **0** means that the button is released and **1** that it is pressed. A bitmask can be used to retrieve the buttons.

| Button 1 | Button 2 | Button 3 | Button 4    | Button 5   | Button 6 | Button 7 |
|:--------:|:--------:|:--------:|:-----------:|:----------:|:--------:|:--------:|
| Horn     | Announce | Camera   | Right doors | Left doors | SELECT   | START    |
