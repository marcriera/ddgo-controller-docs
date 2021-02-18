## USB controllers

The information in this section applies to the following controllers:

- DGC-255: one-handle controller (Microsoft Windows)
- DGOC-44U: two-handle controller (Microsoft Windows)
- DRC-184/DYC-288: Ryojōhen controller (Microsoft Windows)
- TCPP-20009: two-handle controller "Type 2" (Sony PlayStation 2)
- TCPP-20011: Shinkansen controller (Sony PlayStation 2)
- TCPP-20012: two-handle controller "Type 2", purple skeleton (Sony PlayStation 2)
- TCPP-20014: Ryojōhen controller (Sony PlayStation 2)

### DGC-255

This controller shares most of its behaviour with DGOC-44U, but internal details need to be confirmed.

### DGOC-44U

This controller is a HID-compliant joystick with two axes and six buttons. You can find its HID descriptor [here](descriptor_dgoc44u.txt).

|                   |                             |
|-------------------|-----------------------------|
| **Product name**  | `電車でGO! コントローラ USB版` |
| **Manufacturer**  | `TAITO`                     |
| **Vendor ID**     | `0x0AE4`                    |
| **Product ID**    | `0x0003`                    |
| **Serial number** | `TCPP20009`                 |

The controller sends reports to the host (PC) formed by 6 bytes:

| Byte 1 | Byte 2 | Byte 3 | Byte 4  | Byte 5 | Byte 6 |
|:------:|:------:|:------:|:-------:|:------:|:------:|
| Brake  | Power  | Null   | Buttons | Null   | Null   |

The values for the brake notch byte are the following. There are 5 unmarked positions between **B8** and **Emergency**, but unlike classic controllers, they are all report the value for **Emergency**.

| Released | B1   | B2   | B3   | B4   | B5   | B6   | B7   | B8   | Emergency | Transition |
|:--------:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:---------:|:----------:|
| 0x79     | 0x8A | 0x94 | 0x9A | 0xA2 | 0xA8 | 0xAF | 0xB2 | 0xB5 | 0xB9      | 0xFF       |

The values for the power notch byte are listed below.

| N    | B1   | B2   | B3   | B4   | B5   | Transition |
|:----:|:----:|:----:|:----:|:----:|:----:|:----------:|
| 0x81 | 0x6D | 0x54 | 0x3F | 0x21 | 0x00 | 0xFF       |

The button byte uses six bits to represent the state of the physical buttons. **0** means that the button is released and **1** that it is pressed.

| Button 1 | Button 2 | Button 3 | Button 4 | Button 5 | Button 6 |
|:--------:|:--------:|:--------:|:--------:|:--------:|:--------:|
| B        | A        | C        | D        | SELECT   | START    |

### DRC-184/DYC-288

No details are available regarding internal functioning.

### TCPP-20009/TCPP-20012

No details are available regarding internal functioning.

### TCPP-20011

No details are available regarding internal functioning.

### TCPP-20014

No details are available regarding internal functioning.

## Acknowledgements

Big thanks to [GMMan](https://github.com/GMMan), who has provided the internal details of the DGOC-44U.
