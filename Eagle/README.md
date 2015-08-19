#Instructions

In the `lb` repertory you can find all the libraries used for the pcb design.

*   robot_insa_V1.lbr for __AriettaG25__
*   Teensy3.0.lbr for __Teensy__
*   TI-Eagle_library.lbr for __PTN78000WAH__
*   TLC5940.lbr for the __TLC__


Eagle files are located in the `Eagle` reportory.

* `leka.sch` is the schematic, this file represents the circuit diagram.
Parts are placed on many sheets and are connected together through ports.


* `leka.brd` represents the "_physical_" PCB. In this file, traces are connected 
besides the connections defined in the schematic.   
The auto-route function didn't 
have been used because the optimisation is worst with this method.  
Take the time to realize your own routes. Mountage will be easier!

![](https://github.com/eiithel/PCB_english/blob/master/Images/board.png)

> A little display of .brd file

>If you order this PCB from a PCB manufacturer, **DON'T** ask for serigraphy.
Indeed, there is a lot of "stop mask" issues during DRC checking and this problem can be simply resolved by deleting this layer. 
The explanation is that Serigraphy layer prints onto top or bottom copper and that isn't correct.
