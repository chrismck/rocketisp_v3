# rocketisp_v3
Version 3 of the SPI/TPI/PDI programmer, this with switchable 5V/3V3


## Firmware Notes

 Software derived from latest USBasp firmware supporting
 SPI (Serial Peripheral Interface) and TPI (Tiny Programming Interface)
 by Thomas Fischl from https://www.fischl.de/usbasp/ & PDI (Program and Debug Interface) 
 additions by "szu" from http://szulat.blogspot.com/ the majority of this work is theirs.
 
### Version 1.0V3
 
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
 
 Use the SPI/TPI connector (one closest to the microcontroller's crystal) - Need to update better Silk 
 
 Burn as you would any target ATMEGA328PB board, ensuring the correct fuses above.
 
 
