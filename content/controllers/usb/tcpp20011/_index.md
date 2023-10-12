---
title: "Shinkansen controller (Sony PlayStation 2)"
---

{{% controller-page "tcpp20011" %}}

This controller has two handles (13 power notches and 7+emergency brake notches), a D-Pad and 6 buttons (Select, Start, A, B, C, D). In addition, it provides a simple display, a door lamp and a 3.5 mm jack connector to plug a horn pedal. There are two rumble motors, one in each handle.

Internally, it is a HID device with a vendor-specific class.

|                             |                                           |
|-----------------------------|-------------------------------------------|
| **Product name**            | TAITO_DENSYA_CON_T02                      |
| **Manufacturer**            | TAITO                                     |
| **Vendor ID**               | 0x0AE4                                    |
| **Product ID**              | 0x0005                                    |
| **Serial number**           | TCPP20011                                 |
| **USB standard descriptor** | [Link](/controllers/usb/descriptors/tcpp20011_standard-descriptor.txt) |
| **HID report descriptor**   | Not provided                              |

### Input

The controller sends reports to the host (PS2) formed by 6 bytes:

| Byte 1 | Byte 2 | Byte 3 | Byte 4 | Byte 5  | Byte 6   |
|:------:|:------:|:------:|:------:|:-------:|:--------:|
| Brake  | Power  | Pedal  | D-Pad  | Buttons | *Unused* |

The values for the brake notch byte are the following.

| Released | B1   | B2   | B3   | B4   | B5   | B6   | B7   | Emergency | Transition |
|:--------:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:---------:|:----------:|
| 0x1C     | 0x38 | 0x54 | 0x70 | 0x8B | 0xA7 | 0xC3 | 0xDF | 0xFB      | 0xFF       |

The values for the power notch byte are listed below.

| N    | P1   | P2   | P3   | P4   | P5   | P6   | P7   | P8   | P9   | P10  | P11  | P12  | P13  | Transition |
|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----------:|
| 0x12 | 0x24 | 0x36 | 0x48 | 0x5A | 0x6C | 0x7E | 0x90 | 0xA2 | 0xB4 | 0xC6 | 0xD7 | 0xE9 | 0xFB | 0xFF       |

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
| D        | C        | B        | A        | SELECT   | START    |

### Output

The controller supports receiving data via a control transfer to update the screen, turn on/off the door lamp and provide rumble. The setup packet is as follows:

| bmRequestType | bRequest | wValue | wIndex | wLength |
|:-------------:|:--------:|:------:|:------:|:-------:|
| 0x40          | 0x09     | 0x0301 | 0x0000 | 0x0008  |

The data sent to the controller follows the structure below.

| Byte 1      | Byte 2      | Byte 3                     | Byte 4      | Bytes 5-6   | Bytes 7-8 |
|:-----------:|:-----------:|:--------------------------:|:-----------:|:-----------:|:---------:|
| Left rumble | Right rumble| Door lamp + Limit approach | Speed gauge | Speedometer | ATC limit |

* **Left/right rumble:** **0x00** is **Off**, **0x01** is **On**.
* **Door lamp:** **0x0X** is **Off**, **0x8X** is **On**.
* **Limit approach:** values between **0xX0** and **0xXA** representing the number of LEDs lit above the speedometer. In-game, these mark the 10 km/h right below the speed limit.
* **Speed gauge:** values between **0x00** and **0x16** representing the number of LEDs lit on the speed gauge. LED #23 cannot be lit. In-game, these mark 15 km/h increments in the current speed, with one lit when speed is 1-15 km/h, two when 16-30 km/h, etc.
* **Speedometer:** values between **0x0000** and **0x0999** representing the current speed. Values are encoded with **BCD 8421** (i.e. **120 km/h** should be represented as **0x0120**, NOT **0x0078**).
* **ATC limit:** values between **0x0000** and **0x0999** representing the ATC speed limit. Values are encoded with **BCD 8421** (i.e. **120 km/h** should be represented as **0x0120**, NOT **0x0078**).

Multi-byte values should be stored in **Little Endian**.
