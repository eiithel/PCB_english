

#**General**
This card is the first linux embedded solution for the robot Moti. She is doing transition between the first arduino based solution of the robot and the new hardware architecture based on a linux kernel that will allow to do much more things.
_(web API, video analyse, real time)_
The software used for the card conception is `Eagle`.
She has been realised at Usine IO, a physical playground for hardware engineers & designers.

##**Functional requirements**

This card has been developped with the idea of writing code very fast. It isn't the final version of Moti but it will rather be usefull for developpers to realize their tests and to validate this type of architecture.
The card allows to connect `actuators` that permit the robot to live and to move and there are also `sensors` that permit the robot to be aware of its environment and to react in consequence.

* Actuators
  * Motor control
  * RGB LEDs control
*  Datas/Sensoring
  *  Accelerometer/gyroscope
  *  Microphone

_the video is not supported in this version._

##**Components choice**

###Control part

* **Teensy 3.1**  
  
  
![](https://github.com/eiithel/pcb/blob/master/Images/teensy.png)

The control card is equipped by a Teensy ARM Cortex 32 bits.
This module is suitable for `C/C++` programming and is compatible with code written for Arduino.
It is also featured by a large number of IO pinouts (_total of 34_). The Teensy is dedicated for three tasks :

*  Communicate to the **Arietta** informations concerning the differents modules/sensors and to manage the different request 
* To deploy 12 GPIO and one serial port.
* To Manage enslavement motor calculations  

>The code written on this card hasn't to be modify. It involves to put in it the simpliest code possible.
.

   * **Arietta**  
![](http://www.acmesystems.it/products/ARIETTA-G25.jpg)  

**Arietta** is a little embedded linux system based on a ARM9 very swift. _(400MHZ)_ it is equipped by a wifi card, several GPIOs and a serial port connected to the **Teensy**.  This is the main part of the intelligence of the robot and is dedicated to several tasks :

  * To receive and to send informations and requests to the Teensy
  * To manage all Moti's intelligence.(_This part can be developped on a computer before to be embedded on the card_).
  * Web server in order to developps applications permitting to a certain number of clients to use its services (Smartphones and tablets).

>An  Arietta's i2C bus is available on the card to add eventually a sensor.


###Motors

Motors are controlled by the control card but need a dedicated integrated circuit to supply them enough power in order to run correctly.
This is what permit the POLULU module based on a **TB6612FNG**.


<img src="http://www.robotshop.com/media/catalog/product/cache/1/image/800x800/9df78eab33525d08d6e5fb8d27136e95/p/o/pololu-dual-dc-motor-driver-1a-4-5v-3-5v-tb6612fng-4_1.jpg" width="300" height="300"/>

PWMs and logic (AIN, BIN) are provided by the **Teensy**.

### **RGB LEDs**

In order to pilot 6 RGB LEDs, we need 6*3 = 18 channels.
It is out of the question to use all the PWM __Teensy__ outputs for that.
The trick is to use a led's driver that will allow us to increase our number of avalaible PWM outputs. This driver is controlled by the i2C Bus and provids 16 PWM channels.
The 2 missing channels will be provided by the __Teensy__.
The used component is the **TLC5940** (Texas Instrument).

<img src="http://www.ti.com/graphics/folders/partimages/TLC5940.jpg" width="250" height="150"/>
 

##**Supplies**

The control part of the architecture needs to be supplied by 5V.
Motor part needs 6V.
The solution was to use DC/DC adjustable regulators in order to provide the good tensions scales.

**PTN78000WAH** _(Texas Instrument)_

![](http://uk.farnell.com/productimages/standard/en_GB/1564908-40.jpg)

This component can supply a max output current of 3A which is enough to run motors.
It works for an 7 to 36V wide input tension.
It permits to obtain a 2.5 to 22V wide output regulate tension.
The output voltage is set using a single external resistor.

* 21 kohm for `5V`
* 13 kohm for `6V`
 
>All the passive components of the circuit are _SMD_ in order to save space on the board.

###**A little display of the card**

![image](https://github.com/eiithel/PCB_english/blob/master/Images/PCB_bottom.jpg)
> <center>_Bottom face_</center>

![image2](https://github.com/eiithel/PCB_english/blob/master/Images/pcb_top.jpg)
><center>_Top face_</center>


###__Bloc diagram__

To resume, here is the electronical architecture of the prototype:

![](https://github.com/eiithel/PCB_english/blob/master/Images/english.png)

> Written by Eiithel.



