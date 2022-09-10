In a world where professional assembly of well-optimized boards costs basically nothing, you shouldn't have to assemble these boards by hand - no one should.  This is the main reason why this project exists.  Nevertheless, should you wish to hand-assemble this board for some reason, you certainly have that option.

Ordering Boards
=============

Zipped Gerber files are available in the project folder for each released revision of the board.  They should be ready to upload to your favorite PCB manufacturer such as JLCPCB, PCBWay, OSH Park, etc.  The boards should be ordered in 1.6mm (0.062") thickness, which should be the standard thickness just about everywhere.  White solder mask is suggested, but obviously not functionally required.  The surface finish is also up to you; HASL seems to work fine for these boards.


Ordering Parts
=============

The BOM for the board is provided as a CSV file in the project folder for each released revision of the board.  It contains part numbers for both LCSC and DigiKey.  I'm not opposed to adding other distributors' part numbers if there is interest in that as well.  A shared DigiKey cart containing the parts you need is available [here](https://www.digikey.com/short/dphdzd52).  Unfortunately, given the current state of the global electronic component market (as of mid-2022), parts are likely to go in and out of stock all the time, and the STM32 microcontroller is straight up unobtainable via authorized distributors.  A list of some substitutes for parts that are likely to go out of stock is included below.  If there are other parts you are unsure about substitutes for, feel free to open an issue or post about it on the discussions page.

|Reference|Description|Alternates|
|---------|-----------|----------|
|J11|DB25 right angle male connector|DB25-PL-24, A-DS 25 A/KG-T4S|
|D4, D5, D6|Schottky Diode, 40V/1A, SOD-123|MBRX120LF-TP, SBA130AS\_R1\_00001, B5819W-TP|
|J2|USB 2.0 Type-C connector|12402012E212A, USB4105-GF-A|
|U1|3.3V linear regulator, SOT223, 1117 pinout|LM1117MPX-33NOPB, AZ1117IH-3.3TRG1, LDL1117S33R, NCP1117ST33T3G|


Assembling The Board
=============
This board is designed with primarily surface-mount components.  In order to assemble this board, some familiarity with surface-mount soldering is required.  A soldering iron with a fine point, some 0.3mm solder, and a magnifier or microscope are also helpful.  There are a number of videos on how to solder surface-mount components; here are a few that look reasonable:

https://www.youtube.com/watch?v=b9FC9fAlfQE

https://www.youtube.com/watch?v=hoLf8gvvXXU

https://www.youtube.com/watch?v=f9fbqks3BS8

https://www.youtube.com/watch?v=EW9Y8rDm4kE

[This](https://youtu.be/Q2M2qIhKqx8) is a time-lapse of the actual assembly of two copies of this board.  This is by no means the only order in which components can be installed, but I think it's a pretty reasonable one.  If nothing else, I would definitely suggest installing the fine-pitch parts (the microcontroller, USB connector, and SD card slot) first, and the large through-hole connectors last.

An interactive HTML BOM is also provided in the file ibom.html.  This provides a mapping between component values and their location on the board, which I have found to be very helpful when hand-assembling boards.

Once you've finished assembling the board, proceed to the [finishing page](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/finishing.md).
