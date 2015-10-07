#**Introduction**  
There is currently no cure for autism. Special educators often struggle to communicate with children
sometimes immured in their silence. Autistic children can develop their language and facilitate their
interpersonal interactions with the help of early childhood management and special education.   
According to recent studies, the robot is a relevant tool for reducing some autistic symptoms, such as
joint attention deficit disorder. It also promotes generalization of skills.   
I proposed a new hardware and software architecture for Leka's first educational robot, as an extension
to its control system. This new architecture is based on a Linux kernel.   
This expansion provides support for experimentation and verification of embedded Linux applications
for a robotic base.    
**Key words**: robotics, autism, hardware conception, embedded linux

##**Functional requirements**

This card has been developed for the purpose of writing code at rapid speeds. It isn't the final version of Moti but it will be rather useful for developers, helping them to realize their tests and to validate this type of architecture. The card allows connection between `actuators` that permits the robot to live and to move and there are also `sensors` that permit the robot to be aware of its environment and to react consequential to that environment.

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

The control card is equipped with a __Teensy__ ARM Cortex 32 bits, a powerfull 32 bits MCU.   
This module is suitable for `C/C++` programming and is compatible with code written for __Arduino__. It is also featured with a large number of IO pinouts (_total of 34_). The Teensy is dedicated to three tasks :

*  Communicate to the __Arietta__ informations concerning the differents modules/sensors and to manage the different requests.
* To deploy 12 GPIO and one serial port.
* To Manage enslavement motor calculations.

>The code written on this card doesn't have to be modified. It should have just the simpliest code possible.
.

   * **Arietta**  
![](http://www.acmesystems.it/products/ARIETTA-G25.jpg)  

The __Arietta__ is a little embedded linux system based on a very swift ARM9. (_400MHZ_) it is equipped with a WIFI module, several GPIOs and a serial port connected to the __Teensy__. This comprises the central intelligence of the robot and is dedicated to several tasks :

  * To receive and to send information and requests to the __Teensy__.
  * To manage all Moti's intelligence. (_This part can be developped on a computer before being embedded on the card_).
  * Web server in order to develop applications permitting a certain number of clients to use its services (_Smartphones and tablets_).

>An Arietta's i2C bus is available on the card to add eventual sensor.   

A simple example of how to communicate beetween Arietta and Teensy :  
<https://github.com/eiithel/node_Serial>   
I used NodeJS for my tests.


###Motors

Motors are controlled by the control card but they need a dedicated integrated circuit to supply them enough power in order to run correctly. This is what permits the POLULU module based on a __TB6612FNG__ chip.

![toshiba](https://github.com/eiithel/PCB_english/blob/master/Images/toshiba.jpg)

PWMs and logic (AIN, BIN) are provided by the **Teensy**.

You can see a use case here: <https://github.com/eiithel/motors_test>    

>Be carefull. The **Teensy** is provided by 3 Timers.  
Motors PWMs come from **Timer0** but this timer is already used for **GSCLK** and **SIN** signals of the **TLC** due to pin sharing.  
You have to replace this PWMs by Outputs provided by Timer2 which is not used.  
This Timer is located under the **Teensy** (_pins 25 & 32_).

### **RGB LEDs**

In order to pilot 6 RGB LEDs, we need 6*3 = 18 channels. It is out of the question to use all the PWM Teensy outputs for that. The trick is to use a LED's driver that will allow us to increase our number of avalaible PWM outputs. This driver is controlled by the i2C Bus and provids 16 PWM channels. The 2 missing channels will be provided by the Teensy itself. The used component is the __TLC5940__ (Texas Instrument).

<img src="http://www.ti.com/graphics/folders/partimages/TLC5940.jpg" width="250" height="150"/>

You can see a use case here: <https://github.com/eiithel/TLC4950_test>
 

##**Supplies**

The robot is designed with separate voltage regulators for digital and analog supply.   
The control part of the architecture needs to be supplied by 5V. The motor and its components need 6V. The solution was to use DC/DC adjustable regulators in order to provide good tensions scales.

**PTN78000WAH** _(Texas Instrument)_

![](http://uk.farnell.com/productimages/standard/en_GB/1564908-40.jpg)

This component can supply a max output current of 3A which is enough to run motors. It works for a 7 to 36V wide input tension. It permits to obtain a 2.5 to 22V wide output regulate tension. The output voltage is set using a single external resistor.

* 21 kohm for `5V`
* 13 kohm for `6V`
 
>All the passive components of the circuit are _SMD_ in order to save space on the board.

__BE CAREFULL__

This input is not protected against over and reverse voltages.  
When supplying the board take care to not invert anode and cathode. It would cause irreversible damages to the whole board.

###**A little display of the card**

![image](https://github.com/eiithel/PCB_english/blob/master/Images/PCB_bottom.jpg)
> <center>_Bottom face_</center>

![image2](https://github.com/eiithel/PCB_english/blob/master/Images/pcb_top.jpg)
><center>_Top face_</center>


###__Bloc diagram__

To sum up, here is the electronical architecture of the prototype:

![](https://github.com/eiithel/PCB_english/blob/master/Images/english.png)

--
And the final view with some little errors to correct:   

![](https://github.com/eiithel/PCB_english/blob/master/Images/topi.png)

<center>_Final view_</center>


> Written by Eiithel.

<a href="https://fr.linkedin.com/pub/ethel-marquer/84/151/485" style="text-decoration:none;"><span style="font: 80% Arial,sans-serif; color:#0783B6;"><img src="https://static.licdn.com/scds/common/u/img/webpromo/btn_in_20x15.png" width="20" height="15" alt="Voir le profil LinkedIn de Ethel Marquer" style="vertical-align:middle;" border="0">&nbsp;Voir le profil de Ethel Marquer</span></a>


