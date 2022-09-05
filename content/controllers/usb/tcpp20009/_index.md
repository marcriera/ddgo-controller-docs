---
title: 'Two handle controller "Type 2" (Sony PlayStation 2)'
---

{{% controller-page "tcpp20009" %}}

This controller has two handles (5 power notches and 8+emergency brake notches), a D-Pad and 6 buttons (Select, Start, A, B, C, D). In addition, it provides a door lamp and a 3.5 mm jack connector to plug a horn pedal. There are two rumble motors, one in each handle.

Internally, it is a HID device with a vendor-specific class.

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | TAITO_DENSYA_CON_T01                      |
| **Manufacturer**            | TAITO                                     |
| **Vendor ID**               | 0x0AE4                                    |
| **Product ID**              | 0x0004                                    |
| **Serial number**           | TCPP20010                                 |
| **USB standard descriptor** | [Link](/controllers/usb/descriptors/tcpp20009_standard-descriptor.txt) |
| **HID report descriptor**   | Unavailable                               |

### Input

The controller sends reports to the host (PS2) formed by 6 bytes:

| Byte 1 | Byte 2 | Byte 3 | Byte 4 | Byte 5 | Byte 6  |
|:------:|:------:|:------:|:------:|:------:|:-------:|
| 0x01   | Brake  | Power  | Pedal  | D-Pad  | Buttons |

The values for the brake notch byte are the following.

| Released | B1   | B2   | B3   | B4   | B5   | B6   | B7   | B8   | Emergency | Transition |
|:--------:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:---------:|:----------:|
| 0x79     | 0x8A | 0x94 | 0x9A | 0xA2 | 0xA8 | 0xAF | 0xB2 | 0xB5 | 0xB9      | 0xFF       |

The values for the power notch byte are listed below.

| N    | P1   | P2   | P3   | P4   | P5   | Transition |
|:----:|:----:|:----:|:----:|:----:|:----:|:----------:|
| 0x81 | 0x6D | 0x54 | 0x3F | 0x21 | 0x00 | 0xFF       |

The pedal byte has two possible values depending on the state of the pedal.

| Released | Pressed |
|:--------:|:-------:|
| 0xFF     | 0x00    |

The D-pad byte represents the state of the arrow buttons. If two opposite directions are pressed simultaneously, the result is **Center** unless a third button is pressed.

| N    | NE   | E    | SE   | S    | SW   | W    | NW   | None/Center |
|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:-----------:|
| 0x00 | 0x01 | 0x02 | 0x03 | 0x04 | 0x05 | 0x06 | 0x07 | 0x08        |

The button byte uses six bits to represent the state of the physical buttons. **0** means that the button is released and **1** that it is pressed. A bitmask can be used to retrieve the buttons.

| Button 1 | Button 2 | Button 3 | Button 4 | Button 5 | Button 6 |
|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| B        | A        | C        | D        | SELECT   | START    |

### Output

The controller supports receiving data via a control transfer to turn on/off the door lamp and provide rumble. The setup packet is as follows:

| bmRequestType | bRequest | wValue | wIndex | wLength |
|:-------------:|:--------:|:------:|:------:|:-------:|
| 0x40          | 0x09     | 0x0301 | 0x0000 | 0x0002  |

The data sent to the controller follows the structure below.

| Byte 1 | Byte 2   |
|:------:|:--------:|
| Status | Function |

* **Status:** defines whether the function specified in byte 2 is **Off** (**0x00**) or **On** (**0x01**).
* **Function:** **0x01** is **Left rumble**, **0x02** is **Right rumble**, **0x03** is **Door lamp**.
