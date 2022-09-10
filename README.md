![dietSCSI logo](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/title.svg)

The dietSCSI is a SCSI disk emulator, designed to be low-cost while remaining highly functional.

Features
----------

* SMT-first design, optimized for modern low-cost assembly services
  * Target price of ~$10 each in small quantities from JLCPCB, fully assembled
  * This implies that the retail price for a fully-assembled board could be $20 with a 100% markup
* Can be [hand-assembled](https://youtu.be/Q2M2qIhKqx8) using only parts that are [readily available from DigiKey](https://www.digikey.com/short/dphdzd52) (Except for the STM32 microcontroller, but those aren't readily available anywhere at the moment)
* Integrated DB25 and 50-pin IDC connectors on one board.  A single PCB design covers multiple use cases, ideal for easy switching between multiple computers
  * This also means that you can use the dietSCSI itself as a DB-25 to 50-pin SCSI adapter in a pinch
* On-board termination (jumper-selectable)
* Design files for [3D printed cases](https://github.com/ArrestedLightning/dietSCSI/blob/main/Mechanical/README.md) are available in variants for both portable usage and 3.5" hard disk replacement
* 0.1" headers for external activity LEDs
* Can be powered via SCSI termination power or from an external source
* Designed to run firmware based on the open source [BlueSCSI firmware](https://github.com/erichelgeson/BlueSCSI/)
* [Default firmware](https://github.com/ArrestedLightning/dietSCSI_firmware/) has both [USB image passthrough](https://youtu.be/Y3mzckQU518) and [USB firmware update support](https://youtu.be/odwWRFDpAHM) built in (see the [usage page](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/usage.md) for details).

![dietSCSI PCB image](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/dietSCSI_render.jpg)

Documentation
--------
* [Ordering assembled boards from JLCPCB](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/ordering_boards.md)
* [Hand assembly](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/hand_assembly.md)
* [Finishing](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/finishing.md)
* [Usage](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/usage.md)
* [Test Results](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/testresults.md)

Acknowledgments
--------

* The [ARDSCSuino-stm32](https://github.com/ztto/ArdSCSino-stm32) project for the original implementation of STM32-to-SCSI hardware and firmware
* [This TI document](https://www.ti.com/lit/an/slla035/slla035.pdf) on SCSI termination
* The [BlueSCSI project](https://github.com/erichelgeson/BlueSCSI/) for their work on the firmware


BlueSCSI is a registered trademark.  This project is not affiliated with or endorsed by the BlueSCSI project.  Please do not contact the BlueSCSI people for support; use GitHub discussions or email me directly.
