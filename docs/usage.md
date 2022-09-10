Termination
===========
Parallel SCSI devices typically require at least one, but no more than two, device(s) on the bus to have termination enabled.  Best practice is to enable termination on devices at the ends of the SCSI bus.  For an internal device, you will almost always want termination to be enabled.  For an external device, you will also usually want termination enabled, but you may need to disable it if other devices on the bus also provide termination.

SCSI devices are notorious for being sensitive to termination issues; sometimes the only way to resolve issues is trial and error.  If you are having issues with SCSI device reliability, try disabling termination if it is enabled, or enabling it if it is disabled.  On may Macintosh machines, the internal SCSI hard drive is on the same bus as the external SCSI port, and the internal hard drive will typically have termination enabled, so you may already have one terminated device on the bus without realizing it.  Counterintuitively, sometimes adding more SCSI devices to the bus, such as a ZIP drive, may actually improve the stability of the bus.

SCSI Addressing
===========
8-bit SCSI allows for up to 8 devices on the bus (i.e. IDs 0 - 7).  On Macintosh systems, the internal hard disk is typically assigned to SCSI ID 0, and an internal CD-ROM drive is typically assigned to SCSI ID 3.  The computer itself will typically be at SCSI ID 7.  Other internal drives (Zip, Jazz, M-O, etc) will also consume SCSI IDs.  Connecting two devices with the same SCSI ID to the same SCSI ID will typically result in a computer that hangs up on boot.  If you are unsure which SCSI IDs are already in use on your computer, use a tool such as SCSIProbe to enumerate the existing SCSI devices.

Disk Images
===========
The standard firmware for the dietSCSI uses raw disk images to represent hard disks.  The naming of the disk images is used to configure disk and SCSI parameters.

The TL;DR version is this:

Images should be named like HD[ID][LUN]_[SS].hda. [ID] represents the SCSI id. [LUN] represents the SCSI LUN; 0 is the only value supported. [SS] is the sector size.  This will virtually always be 512, but could also be 256 or 1024 in certain circumstances.  Additional text in the file name is ignored and can be used to help identify disk images.  Disk images can be named using the extensions .hda or .img.  File names should be less than 32 characters.

Example disk image names:

HD10_512.hda

HD20_512 Mac OS.img

A nice prebuilt hard disk image with Mac OS and tons of apps and games for compact macs is https://archive.org/details/macpack-20210619.  Rename boot.vhd to something like HD10_512.hda.

You can also easily generate custom blank disk images using [Disk Jockey] (https://bluescsi.onegeekarmy.eu/diskjockey/).

USB Passthrough Mode
===========
On units running USB-enabled firmware, USB passthrough mode is available.  When plugged into a computer's USB port, the same disk images that would be made available over the SCSI port will instead be made available to the computer over USB as separate USB disks.  If both your SCSI-equipped and USB-equipped computers can understand a common file system, this allows you to use the dietSCSI as a simple and convenient way to transfer files.  Note that USB and SCSI operation are mutually exclusive.  Plugging in both the SCSI and USB ports is not recommended, but doing so will result in the USB interface taking precedence over the SCSI interface.

USB passthrough mode adds a delay of around 1 second on startup as the device needs time to detect if it is connected to a USB host.  In my limited testing, I did not find this to cause any compatibility problems, but if it does, USB passthrough mode can be disabled by creating a file named `nousb` in the root directory of the SD card.

Currently on Windows hosts, only a single volume can be passed through over USB.  If additional volumes are present on the SD card, USB passthrough mode will not work at all under Windows.  On Mac OS or Linux hosts, all volumes will be passed through to the host as expected.  This will be fixed in a future firmware release.

A video demonstrating this feature is available here: https://youtu.be/Y3mzckQU518.



USB Firmware Updates
==========
On units running USB-equipped firmware, the device's firmware can be updated using the USB port, without requiring any additional hardware such as an ST-LINK programmer.  This is possible due to the built-in [STM32duino bootloader](https://github.com/ArrestedLightning/STM32duino-bootloader). To update the firmware in the device, bridge the pins labeled "Boot 1" using a tweezers or piece of wire, or solder in a two-pin header and install a jumper.  Then plug in the USB cable.  The red LED (D1) should start to flash.
The firmware is updated using the `dfu-util` command.  The command you will use should look something like `dfu-util -D firmware.bin`.  The `-R` flag can be added to reboot the device automatically after the update completes.  This process has been tested on Linux, but it should also be possible under Mac OS and Windows.  After updating, check the `LOG.txt` file on the SD card to verify that the new firmware version was installed successfully.

A video demonstrating this feature is available here: https://youtu.be/odwWRFDpAHM.