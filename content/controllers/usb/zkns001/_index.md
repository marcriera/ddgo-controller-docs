---
title: "One handle controller (Nintendo Switch)"
---

{{% controller-page "zkns001" %}}

This controller has one handle (5 power notches and 8+emergency brake notches) and 16 buttons (the same as a Nintendo Switch Pro Controller, except the stick buttons). Internally, it is a HID-compliant joystick mimicking a Nintendo Switch Pro Controller. The stick buttons and the right stick are unused, and only the Y axis of the left stick is used.

|                             |                                                                                                  |
|-----------------------------|--------------------------------------------------------------------------------------------------|
| **Product name**            | One Handle MasCon for Nintendo Switch<br>One Handle MasCon for Nintendo Switch Exclusive Edition |
| **Manufacturer**            | *None*                                                                                           |
| **Vendor ID**               | 0x0F0D<br>0x33DD (Exclusive Edition)                                                             |
| **Product ID**              | 0x00C1<br>0x0002 (Exclusive Edition)                                                             |
| **Serial number**           | *None*                                                                                           |
| **USB standard descriptor** | [Link](/controllers/usb/descriptors/zkns001_standard-descriptor.txt)                             |
| **HID report descriptor**   | [Link](/controllers/usb/descriptors/zkns001_hid-report-descriptor.txt)                           |

### Input

The power/brake handle notches are reported in the Y axis of the left stick. There are no transition values between notches. In addition, when the handle is set to **Emergency**, **ZL** is pressed.

| Emergency | B8   | B7   | B6   | B5   | B4   | B3   | B2   | B1   | N    | P1   | P2   | P3   | P4   | P5   |
|:---------:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
| 0x00      | 0x05 | 0x13 | 0x20 | 0x2E | 0x3C | 0x49 | 0x57 | 0x65 | 0x80 | 0x9F | 0xB7 | 0xCE | 0xE6 | 0xFF |
