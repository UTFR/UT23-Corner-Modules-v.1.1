# UT23 Corner Modules v.1.1

By: Benjamin Liang, Controller Design Lead, University of Toronto Formula Racing Team

In this article, I will present the Corner Modules v.1.1 for UT23, our car for next year’s competition season. Each year, we, the University of Toronto Formula Racing Team (UTFR) design and build a new formula-style car from scratch to compete in international Formula SAE events. At its heart, formula-style cars are designed for the sole purpose of racing and achieving maximum performance. To effectively design a fast and reliable car, proper data acquisition must be implemented for performance critical systems across the car. The corner modules are the fundamental cornerstone of our data acquisition architecture. This PCB is designed to interface with a wide variety of sensors and communicate the information over CAN bus to be data logged and used by our central controller.

![image](https://user-images.githubusercontent.com/82067858/209455231-ff090e01-a791-487d-92c4-7efc9febb2a0.png)
 
The corner modules include different components such as an Arduino Micro, a CAN controller and transceiver, a 5V linear regulator and a series of op amps. In this article, I will go over how some of these components are used for CAN bus communication and strain gauge measurement.

Schematic Design

Specifically, the controller design revolves around an Arduino Micro as the MCU. The Arduino Micro is responsible for reading all the sensor signals and forwarding all that information to the CAN controller over SPI communication. On top of the required bypass capacitors and CAN bus termination, the rest of the CAN bus circuitry on the corner module includes a crystal oscillator that generates the required controller clock signal, CAN transceiver, interrupt LED indicator, and TX/RX diagnostic LEDs driven by a buffer. The CAN bus termination is controllable via a dip switch such that it can be connected and disconnected as required to fit the needs of a variety of systems and applications.

![image](https://user-images.githubusercontent.com/82067858/209455235-4bb8d92e-04a7-4ee1-96eb-6ecf94b761e1.png)
 
The corner module strain gauge measurement circuit uses a Wheatstone bridge and an adjustable gain op amp to accurately measure strain in a variety of ways. The circuit is compatible with off the shelf strain gauge modules that can be powered off 5V, quarter bridge strain gauge measurement and half bridge strain gauge measurement. Wheatstone bridges are used for strain gauge measurement to properly scale the change in voltage due to measured strain. The reference half bridges with nets SG_0_REF to SG_3_REF provide a reference voltage at these nets equal to that of the opposite half bridge equipped with one or two unloaded strain gauges. When measuring voltage across the bridge, this allows for the measurement of positive and negative strain as voltages centered at zero, which can be easily scaled by an op amp. 

![image](https://user-images.githubusercontent.com/82067858/209455239-ee3a882a-9791-45ea-a141-4aaa3a71bc07.png)
 
The op amp part number we use in our strain gauge measurement circuit is INA2332AIPWT, which includes separate reference voltage and gain setting pins. This allows for easy hardware translation and scaling of our strain gauge voltage measurement to maximize our measurement range and accuracy. The other LM2904D op amps are used as buffers to accurately set the reference voltage for the signal transformation op amps (INA2332AIPWT). The transformation op amps also include shutdown functionality which we can configure in hardware via pull-up and pull-down jumpers. The circuit is also compatible with off the shelf strain gauge modules that include their own signal transformation using jumpers connected to our Wheatstone bridge that bypass our signal transformation circuitry.

PCB Layout

The corner module is a four-layer board designed using Altium Designer as shown in the figure below. The four layers include a high-frequency digital signal and power top layer, a power and ground second layer, a grounded third layer, and an analog and low-frequency signal bottom layer. Differential signals were routed near each other, and other high-frequency signals were far from one another while still preserving similar trace lengths. A substantial effort was placed in making a user-friendly silkscreen to ensure the correct and safe operation of the board.

![image](https://user-images.githubusercontent.com/82067858/209455242-69086bae-bf08-4285-8c8a-3f3137a12636.png)
 
JLCPCB

This PCB is the cornerstone of a rapid and thorough design cycle with the goal of informing our design decisions next season. This amazing technical development within our team was only possible thanks to the help of JLCPCB (https://jlcpcb.com/RAT). Founded in 2006, JLCPCB (https://jlcpcb.com/RAT) is a leading global PCB manufacturer with over 16 years of experience providing the best customer experience through the rapid production of highly reliable and cost-effective PCBs.

![image](https://user-images.githubusercontent.com/82067858/209455244-79242853-0865-4af7-a9b1-6a6b0039eee5.png)
 
The corner modules were ordered from JLCPCB (https://jlcpcb.com/RAT) for quick, reliable, and cost-effective manufacturing. Ordering PCBs from JLCPCB (https://jlcpcb.com/RAT) is extremely simple and consists of the following four quick steps:

1.	Export Gerber files from Altium Designer
2.	Click on the instant quote button on the JLCPCB website (https://jlcpcb.com/RAT)
3.	Add your Gerber files and double-check the uploaded PCB in the Gerber viewer
4.	JLCPCB automatically detects all the general PCB specifications and fills out the order form for you. Review and modify these to ensure they match your PCB requirements.
5.	Click save to cart, fill out your address, select your shipping method, and pay

Furthermore, JLCPCB (https://jlcpcb.com/RAT) also provides many other manufacturing services including an SMT service which fulfills the money and time saving needs of customers at only an $8.00 setup fee ($0.0017 per joint). It is a one stop online platform where you can also track the progress of your PCBA manufacturing process, which is completed within a day, in real time. Through the platform you can conveniently source thousands of components from JLCPCB (https://jlcpcb.com/RAT) and its reliable component partners like Digikey and Mouser. The quality and reliability are always superb with professionally trained engineers, X-ray inspection, automated optical inspection, automated component placement, and various soldering techniques. 
