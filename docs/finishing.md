DB-25
==========

There are two main types of DB-25 connectors out there.  Some of them have the metal outer shell crimped on; it will stay in place without any screws or standoffs installed.  If this is the type you have on your board, congratulations, you're done with this step!  The other type of connector uses the threaded standoffs on either side of the connector pins to hold the metal shell in place.  This type is generally what you'll get if you have JLCPCB assemble your boards.  Unfortunately, those threaded standoffs have to go if you want to be able to plug your dietSCSI directly into the back of your computer.  If you are absolutely sure you won't need the DB-25 connector (e.g. you plan to permanently install your dietSCSI inside a computer), you technically don't have to do anything here.  However, I would suggest doing it now, while you're thinking about it, regardless.  That way it'll be ready to go in the future should you need an external SCSI device in a pinch.
The standoffs can be removed by loosening them with a pliers and carefully unscrewing them.  Be careful not to bend the pins on the connector while the shell is off.  The standoffs will then need to be replaced with some low-profile screws.  On most DB-25 connectors, the screw threads are SAE #4-40; 1/4" (6.35mm) length is more than sufficient to hold the shell in place.  If you don't have some of these on hand, you should be able to get them from most online or physical hardware stores.  Here is an option [from McMaster-Carr](https://www.mcmaster.com/92949A106/); I have also previously purchased them [from Amazon](https://smile.amazon.com/gp/product/B07TM4Y5CB/), but they appear to be out of stock as of this writing.

![dietSCSI DB25 screws comparison](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/db25_screws.jpg)

Testing
=========

Whether you assembled your dietSCSI board yourself or got it professionally assembled, it's a good idea to give it a quick visual inspection for assembly errors and solder bridges.  Once you are satisfied that there are no hardware issues, it's not a bad idea to try and power the board up in a controlled manner to check for electrical problems.  The best option is a bench power supply with a current limit function, if you have it.  Set it to 5V, 0.5A, and inject power into pins 1 and 2 of the Berg connector.  After powering the board up, verify that the power LED comes on and stays on, and there is no smoke.  The board should be drawing less than 200mA.  If everything looks good, you can move on to programming.  Otherwise, look over the board again, paying careful attention to component orientation, and checking for cracks and solder bridges.

Programming
==========

Now that your board is assembled, you need to get firmware onto it.

JTAG
----------

The most reliable way to get firmware on to your board is using JTAG.  You can get cheap ST-LINK V2 sticks off of Amazon/eBay/Aliexpress for a few dollars; they're virtually all the same.  J10 is the JTAG connector on the dietSCSI board.  Only the first four pins are necessary for programming.  They are in the same order as the corresponding pins on the ST-LINK.  If you'd like, you can solder a 0.1" header into the dietSCSI board.  This would let you use a ribbon cable or female-female dupont wire to connect the ST-LINK to the board.  However, I've found that using male-female dupont wire that's taped into a bundle of 4 is sufficient to make good contact as long as it's inserted and held in at an angle.

![dietSCSI JTAG connector soldered in](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/jtag_soldered.jpg)

![dietSCSI JTAG connector pressed in](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/jtag_press.jpg)

The first time you program the board, no additional steps should be necessary.  On subsequent programmings, you will need to put the chip into bootloader mode by shorting out the BOOT0 pins.  This can be done by jamming a tweezers or a piece of stiff wire in J7.  If you prefer, you can solder a 2-pin 0.1" header into J7 and install a jumper.

### From Source

1. Download and install [Visual Studio Code](https://code.visualstudio.com/).
2. Install [PlatformIO IDE](https://platformio.org/install/ide?install=vscode).
3. Download a copy of the firmware source code or check one out with git.
4. Open Visual Studio Code, then open the firmware source code folder using PlatformIO's "Open Project" command.
5. Connect the dietSCSI board to the computer using the ST-LINK adapter.
6. Click on the "PlatformIO: Upload" button in the lower left corner of the window.
7. Compiling and uploading the firmware should take a few seconds.  It will start running once the upload completes.  An error at this point is normal as the firmware disables the debug pins as soon as is starts.


### Using ST GUI

1. Download and install STM32CubeProg from https://www.st.com/en/development-tools/stm32cubeprog.html.
2. Download a copy of the firmware image in .bin or .hex format.
3. Open the STM32CubeProgrammer application and switch to the Erasing & Programming page using the controls on the left side of the window.
4. Click on File Path > Browse and select the firmware image.  It's not a bad idea to make sure the "Verify programming" option is selected.
5. Connect the ST-Link adapter to the dietSCSI board.  In the top right corner of the STM32CubeProgrammer window, make sure ST-LINK is selected and click connect.
6. Click on the "Start Programming" button and wait for the process to finish.

### Using Command Line

1. Download and install a copy of the stlink command line tools from https://github.com/stlink-org/stlink.  If you're on Linux, they are likely already available in your package manager (Under Ubuntu, try the `stlink-tools` package).
2. Download a copy of the firmware image in .bin or .hex format.
3. Connect the ST-Link adapter to the dietSCSI board.
4. Run the command `st-flash --flash=128k write '/path/to/firmware.bin' 0x8000000`.  Depending on the exact model of microcontroller you have, you may or may not need to omit the `--flash=128k` argument.  If you are using a hex format image, add the argument `--format=ihex` before `write`.

Serial
----------

It is also possible to program the board using a USB-TTL serial adapter.  This has been tested on both an original STM32 as well as the HK32 and GD32 clones, but it may not be supported on all clones.  A 3.3V TTL adapter is recommended, but a 5V adapter may also work.  The programming UART pins are available on the 50-pin SCSI connector, they are labeled G, R, and T for Ground, Receive, and Transmit, respectively.  They are labeled from the point of view of the dietSCSI board; unfortunately, not all serial adapters label their pins consistently.  If it doesn't work, try swapping the RX and TX pins.  If your serial adapter also has a 5V output pin, you can use this to power the board (attach to the middle pin in the bottom row), otherwise, use a USB cable to supply power.  The Boot0 jumper _must_ be shorted when connecting power in order to put the board into serial programming mode.  I have also found that this process works much more reliably with the termination jumpers removed.

![dietSCSI UART programming pins](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/uart_prog_pins.jpg)

### Using ST GUI

1. Download and install STM32CubeProg from https://www.st.com/en/development-tools/stm32cubeprog.html.
2. Download a copy of the firmware image in .bin or .hex format.
3. Open the STM32CubeProgrammer application and switch to the Erasing & Programming page using the controls on the left side of the window.
4. Click on File Path > Browse and select the firmware image.  It's not a bad idea to make sure the "Verify programming" option is selected.
5. Connect the TTL serial adapter to the dietSCSI board.  Apply power to the board while shorting the Boot0 jumper.  In the top right corner of the STM32CubeProgrammer window, make sure UART is selected.  Choose the port corresponding to your adapter and click connect.  I have found that this will occasionally fail the first time you try to connect.  If it fails, try just clicking connect again.  Otherwise, you may have RX and TX backwards; try swapping them.
6. Click on the "Start Programming" button and wait for the process to finish.


Cases
==========

Several cases are available for 3D printing, depending on how you intend to use your dietSCSI device.  Check out the [README in the mechanical directory](https://github.com/ArrestedLightning/dietSCSI/blob/main/mechanical/README.md) for more information.