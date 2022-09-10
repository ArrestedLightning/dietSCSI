Ordering Assembled Boards
=============

This board is optimized for assembly at JLCPCB's low-cost PCB assembly service.  The process is pretty simple:

1. Download the following files from Hardware/Main/\<current rev\>/dietSCSI: **AL1030 \<rev\>.zip**, **dietSCSI\_bom\_jlc.csv**, and **dietSCSI\_cpl\_jlc.csv**.
2. Go to https://jlcpcb.com/
3. Create an account or log in if you already have an account.
4. Click on Order Now in the upper right corner of the page.
5. Click on the "Add gerber file" button near the center of the page.
6. Select the zip file you downloaded earlier and upload it.
7. Select your options.  Here you can select the quantity of boards you wish to order.  Most default settings should be OK, but it is suggested to change the PCB color to white.
8. Scroll down to the _PCB Assembly_ section of the page and turn the switch on.  Select _Assemble top side_.  The other default settings should not need to be changed.  Click on Confirm.
9. Click on _Add BOM File_ and upload the _bom_ file you downloaded earlier.
10. Click on _Add CPL File_ and upload the _cpl_ file you downloaded earlier.
11. Under the Usage Description field, select an appropriate description from the list.
12. Click Next.
13. You will be taken to the Select Parts page.  Look for any parts that have "Inventory Shortage" listed in the rightmost column.  Click on the magnifying glass and search for an alternate part (see "Component Substitutions" below).
14. Once you have selected any necessary substitute parts, click next at the bottom of the page.
15. Scroll to the bottom of the page and make sure there are no parts under the "Unselected parts" heading.
16. Click on "Save to Cart".
17. Go through the checkout process.
18. Wait for your boards to arrive!
19. Once your boards arrive, proceed to the [Finishing](https://github.com/ArrestedLightning/dietSCSI/blob/main/docs/finishing.md) page.

Component Substitutions
============
Various components may not be in stock when you are ready to place your order.  Passive components like resistors or capacitors can generally be replaced with any part of the same value and package.  Some substitutes for more complex parts such as connectors are listed on the schematic.  There are several options for the main microcontroller that are more or less compatible with the original part, but for maximum functionality, sticking with the original STM32F103 part is recommended.  For example, the HK32F103 parts are known to have unusable USB hardware, and have difficulty communicating with SD cards at full speed, which reduces maximum throughput.