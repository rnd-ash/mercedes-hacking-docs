# Chapter 2: Tools and Equipment

This chapter talks about a subject that is often the source of confusion for many who are getting involved in hacking their cars: what tools do I need? 

Whilst we could write an entire book on the subject, we will aim to reference tools that are easily accessible from a cost and usability perspective and offer the best bang for buck. We want as many people as possible to participate in tinkering with their cars so have excluded some good tools that are expensive, such as the official Mercedes-Benz *XENTRY* vehicle diagnosis systems. 

As with all things hacking, you use the tools that work with the targets in question, namely the protocols in use as shown in Chapter 1: Vehicle Bus Protocols and Diagnostics. The tools listed below work with Mercedes-Benz models and whilst not all models use the same protocols, we will show at the start of each recommendation which model this particular tool works best with. 

## Hardware

There has been an immense amount of research and development gone into low-cost tools for us car hackers in recent years. Companies like https://www.macchina.cc/ and http://www.linklayer.com/ have produced two of the best tools, namely the [Macchina M2](https://www.macchina.cc/catalog) and [CANtact Pro](https://www.crowdsupply.com/linklayer-labs/cantact-pro). 

### Macchina M2

![](/Users/daniel/Documents/Code/Carhacking/mercedes-hacking-docs/images/macchinam2.jpg)

The Macchina M2 is based on the Arduino Due and makes use of a SAM3X ARM Cortex-M3 processor processor, which gives it support for the following protocols:

- 2 CAN
- 1 SWCAN
- J1850
- LIN
- IOS9141

The choice of an ARM-Cortex-M3 also gives amazing options to add additional mods to the board, like Wireless/BLE and GSM

![](/Users/daniel/Documents/Code/Carhacking/mercedes-hacking-docs/images/macchinam2board.png)



### CANtact Pro

Eric Evenchick of Linklayer Labs has been a car hacker for a long time and as such, is uniquely positioned to design and develop tools for budding car hackers. The CANtact Pro is a new addition to the tool lineup and incredibly powerful. 

![](/Users/daniel/Documents/Code/Carhacking/mercedes-hacking-docs/images/cantactpro.jpg)

It supports CAN and CAN-FD (Flexible Data) and is found on more modern vehicles. It has software support for Windows, macOS, and Linux 

## Software