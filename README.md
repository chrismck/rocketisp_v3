# All Versions
There have been two other versions of this programmer:

| VER | Description |
|-----|-------------|
| 1.0 | First iteration  of the programmer which was through hole - not documented here |
| 1.1 | Second iteration using small (smaller then 2.0) smd components - no case |
| 2.0 | Third iteration of programmer, was quickly dropped due to IRQ pin trace missing - my bad |
| 2.1 | Fourth iteration, was designed to fit case available via Digikey or 3D printer - fixed 2.0 trace |
| 3.0 | revision to move away from USB thumb drive connector to B style, added switch for power, PDI resistors, etc |

Versions 2.1 and 3.0 are documented here.  I've included the Gerbers, Schematics in PDF form and 3D printer case
files for version 2.1.

## Older Revisions (1 and 2.1)
![OldRevisions](/Images/oldversions.png)
To be honest the small USB programmer is not revision 2.1, as I simply bridged the 2 pins that were missing the connection.

# rocketisp_v2

Small USB TPI/SPI/PDI programmer based on USBasp w/3D printed case

This project was, like the multitude of programmers out there, based on the USBasp programmer.  The original project by Thomas Fischl can be found here: https://www.fischl.de/usbasp/  His project originally supported only a SPI interface, but in later revisions of the firmware supported TPI.

This programmer was oringally supposed to support SPI, TPI, and PDI with no additional components but the design was made without 2 small resistors for the PDI shared send/receive line.  These were simply added with a custom cable for PDI use with my xC3mini xMega development board.

A 3D printed case was created, but the design (as large as it is, with lots of wasted real estate) was created to fit a specific case.

![ROCKETasp_V2](/Images/ROCKETasp_Front_v2_1.png)

The case can be purchased through Digikey # HM1472-ND (Red) or via other distributors using Model # 1551USB3 (Hammond)
for around $5 CAD. The case needs to be modified in the rear to allow the pin header to protrude out, or you can print the modified case
using the supplied STL files for the Top and Bottom.  Use fine settings.

I've stopped using the v2.1 programmer as I found it a pain to have to include a custom cable that includes 2x 220Ohm resistors for
use with my xC3mini board using PDI.  Instead I now use the v3 programmer, which sadly I haven't designed a case for yet.

# rocketisp_v3
Version 3 of the SPI/TPI/PDI programmer, this with switchable 5V/3V3 power, and the missing 220R PDI resistors.  Ya! No more custom ribbon wire or adapters. See <Insert Adapter link here>.

![ROCKETasp_V3](/Images/ROCKETasp_Front_v3.png)

## Firmware Notes

 Software derived from latest USBasp firmware supporting
 SPI (Serial Peripheral Interface) and TPI (Tiny Programming Interface)
 by Thomas Fischl from https://www.fischl.de/usbasp/ & PDI (Program and Debug Interface) 
 additions by "szu" from http://szulat.blogspot.com/ the majority of this work is theirs.
 
### Firmware Version 1.0V3
 
 3rd revision hardware can be 3V3 (for PDI) and 5V powered by using switch,
 the microcontroller is powered using 3V3 when selected 
 
 I've made the minor changes for porting to the ATMEGA328PB, the microcontroller I had
 around when I designed it.
 
 Original License remains GNU GPL v2
 
 Target RocketISP v3, USB programmer, using
 Microchip ATMEGA328PB using external 12MHz Crystal,
 ~6Kb Program Memory (19%), 200b Data Memory (10%)
 
  PIN Usage details:	
  | PIN | PURPOSE | NOTES |
  |-----|---------|-------|
  | PD7 | SPI Activity | 1st Red LED |					
  | PC2 | SLOW SCK (8khz) | DO NOT USE i.e.:set to OFF, when programming PDI targets |		   			
  | PC3 | Powered | Green LED - need to change to indicate USB connection status |					
  | PC4 | TPI Activity | 2nd Red LED |
  | PC5 | PDI Activity | Blue LED |
  | PB0 | RESCUE CLOCK | 5V Only Feature* TBD |
  | PB1 | DEBUG OPTION | TDB - Use for custom firmware |
  | PB2 | TARGET RESET | Control Target Reset Line |					

 	FORCE SLOW CLOCK and DEBUG OPTION both use Internal Pull Ups and are considered ON when grounded.

 ### Programming Firmware

 When reflashing the firmware, or flashing custom firmware:
 
 	FUSES: TARGET = atmega328pb, HFUSE=0xD1, LFUSE=0xFF, EFUSE=0xF7
  
 Board can be programmed using any SPI ISP programmer such as Atmel JTAGICE3, Atmel ICE or even another ROCKETasp or USBasp.
 I would recommend programming at 5V, with the dip switches, and power selection in the following positions:
 
 DIP switch settings:        
 | DIPSWITCH| POS | NOTES |
 | --------- | --- | ----- |
 | DEBUG OPT | OFF | TBD |
 | VTARGET | ON | ROCKETasp needs external power if using a JTAGICE3 or ICE as they don't power targets
 | SLOW CLOCK | OFF | only on SPI targets |
 | FIRMWARE | ON | allow firmware upgrade
                    
 Power Select:      5V
 
 Use the SPI/TPI connector (one closest to the microcontroller's crystal) - Need to update better Silk so it's easier to identify the
 correct connector to use, power switch which direction is 3V3, which is 5V, and the DIP switches.  I forgot to add the information and
 was simply and oversight.  I've made too many of these programmer boards, lol.  I'm hesitant to respin the PCB AGAIN with the updated silk.
 
 Burn as you would any target ATMEGA328PB board, ensuring the correct fuses above.
 
 ## Board Layout
  ![Version3_Layout](/Additional_Files/board_overlay_v3.png)
 
