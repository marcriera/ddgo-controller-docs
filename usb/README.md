## USB controllers

The information in this section applies to the following controllers:

- DGC-255: one-handle controller (Microsoft Windows)
- DGOC-44U: two-handle controller (Microsoft Windows)
- DRC-184/DYC-288: Ryojōhen controller (Microsoft Windows)
- TCPP-20009: two-handle controller "Type 2" (Sony PlayStation 2)
- TCPP-20011: Shinkansen controller (Sony PlayStation 2)
- TCPP-20012: two-handle controller "Type 2", purple skeleton (Sony PlayStation 2)
- TCPP-20014: Ryojōhen controller (Sony PlayStation 2)
- MTC: Multi Train Controller (Sony PlayStation 2)
- ZKNS-001: one-handle controller (Nintendo Switch)

### DGC-255

This controller has one handle (5 power notches and 8+emergency brake notches), a D-Pad and 6 buttons (Select, Start, A, B, C, D).

Internally, it is a HID-compliant joystick with two axes, 6 buttons and a PoV hat switch (the handle positions are reported via axes).

Besides the PoV hat switch, it reports the same data as a DGOC-44U controller. The games check if the controller has a PoV hat switch to distinguish between a DGC-255 and a DGOC-44U.

### DGOC-44U

This controller has two handles (5 power notches and 8+emergency brake notches) and 6 buttons (Select, Start, A, B, C, D).

Internally, it is a HID-compliant joystick with two axes and 6 buttons (the handle positions are reported via axes).

|                           |                                           |
|---------------------------|-------------------------------------------|
| **Product name**          | 電車でGO! コントローラ USB版                 |
| **Manufacturer**          | TAITO                                     |
| **Vendor ID**             | 0x0AE4                                    |
| **Product ID**            | 0x0003                                    |
| **Serial number**         | TCPP20009                                 |
| **Standard descriptor**   | Unavailable                               |
| **HID report descriptor** | [Link](dgoc44u_hid-report-descriptor.txt) |

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

### DRC-184/DYC-288

No details are available regarding internal functioning.

### TCPP-20009/TCPP-20012

This controller has two handles (5 power notches and 8+emergency brake notches), a D-Pad and 6 buttons (Select, Start, A, B, C, D). In addition, it provides a door lamp and a 3.5 mm jack connector to plug a horn pedal. There are two rumble motors, one in each handle.

Internally, it is a HID device with a vendor-specific class.

|                           |                                           |
|---------------------------|-------------------------------------------|
| **Product name**          | TAITO_DENSYA_CON_T01                      |
| **Manufacturer**          | TAITO                                     |
| **Vendor ID**             | 0x0AE4                                    |
| **Product ID**            | 0x0004                                    |
| **Serial number**         | TCPP20010                                 |
| **Standard descriptor**   | [Link](tcpp20009_standard-descriptor.txt) |
| **HID report descriptor** | Unavailable                               |

#### Input

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

#### Output

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

### TCPP-20011

This controller has two handles (13 power notches and 7+emergency brake notches), a D-Pad and 6 buttons (Select, Start, A, B, C, D). In addition, it provides a simple display, a door lamp and a 3.5 mm jack connector to plug a horn pedal. There are two rumble motors, one in each handle.

Internally, it is a HID device with a vendor-specific class.

|                           |                                           |
|---------------------------|-------------------------------------------|
| **Product name**          | TAITO_DENSYA_CON_T02                      |
| **Manufacturer**          | TAITO                                     |
| **Vendor ID**             | 0x0AE4                                    |
| **Product ID**            | 0x0005                                    |
| **Serial number**         | TCPP20011                                 |
| **Standard descriptor**   | [Link](tcpp20011_standard-descriptor.txt) |
| **HID report descriptor** | Unavailable                               |

#### Input

The controller sends reports to the host (PS2) formed by 6 bytes:

| Byte 1 | Byte 2 | Byte 3 | Byte 4 | Byte 5  | Byte 6 |
|:------:|:------:|:------:|:------:|:-------:|:------:|
| Brake  | Power  | Pedal  | D-Pad  | Buttons | Null   |

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

#### Output

The controller supports receiving data via a control transfer to update the screen, turn on/off the door lamp and provide rumble. The setup packet is as follows:

| bmRequestType | bRequest | wValue | wIndex | wLength |
|:-------------:|:--------:|:------:|:------:|:-------:|
| 0x40          | 0x09     | 0x0301 | 0x0000 | 0x0008  |

The data sent to the controller follows the structure below.

| Byte 1      | Byte 2      | Byte 3                     | Byte 4      | Bytes 5-6   | Bytes 7-8 |
|:-----------:|:-----------:|:--------------------------:|:-----------:|:-----------:|:---------:|
| Left rumble | Right rumble| Door lamp + Limit approach | Speed gauge | Speedometer | ATC limit |

* **Left/right rumble:** **0x00** is **Off**, **0x01** is **On**.
* **Door lamp:** **0x0?** is **Off**, **0x8?** is **On**.
* **Limit approach:** values between **0x?0** and **0x?A** representing the number of LEDs lit above the speedometer. In-game, these mark the 10 km/h right below the speed limit.
* **Speed gauge:** values between **0x00** and **0x16** representing the number of LEDs lit on the speed gauge. LED #23 cannot be lit. In-game, these mark 15 km/h increments in the current speed, with one lit when speed is 1-15 km/h, two when 16-30 km/h, etc.
* **Speedometer:** values between **0x0000** and **0x0999** representing the current speed. Values are encoded with **BCD 8421** (i.e. **120 km/h** should be represented as **0x0120**, NOT **0x0078**).
* **ATC limit:** values between **0x0000** and **0x0999** representing the ATC speed limit. Values are encoded with **BCD 8421** (i.e. **120 km/h** should be represented as **0x0120**, NOT **0x0078**).

Multi-byte values should be stored in **Little Endian**.

### TCPP-20014

This controller has two handles (4 power notches and an analogue brake handle with three areas), a D-Pad and 7 buttons (Select, Start, Horn, Announce, Camera, Left doors, Right doors). In addition, it provides a 3.5 mm jack connector to plug a horn pedal.

Internally, it is a HID device with a vendor-specific class.

|                           |                                           |
|---------------------------|-------------------------------------------|
| **Product name**          | TAITO_DENSYA_CON_T03                      |
| **Manufacturer**          | TAITO                                     |
| **Vendor ID**             | 0x0AE4                                    |
| **Product ID**            | 0x0007                                    |
| **Serial number**         | TCPP20014                                 |
| **Standard descriptor**   | [Link](tcpp20014_standard-descriptor.txt) |
| **HID report descriptor** | Unavailable                               |

#### Input

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

### MTC

No details are available regarding internal functioning.

### ZKNS-001

No details are available regarding internal functioning.

## Acknowledgements

- [GMMan](https://github.com/GMMan), who has provided the internal details of the DGOC-44U.
- [TheYamanote](https://twitter.com/The_Yamanote), who has helped with the TCPP-20009.
