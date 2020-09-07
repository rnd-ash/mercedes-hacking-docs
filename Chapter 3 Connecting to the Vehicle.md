# Chapter 3: Connecting to the Vehicle

This chapter is possibly the most important of all chapters. You need to be in the car and communicating with the car in order to play around. As introduced in Chapter 1, finding the OBD-II port is the first step along with plugging in the cable and software to interface with the various CAN bus networks. 

## Hardware Needed

## Software Needed

## Wake Up Command

Many modules require constant power in order to keep configurations stored and accessible, but for the best part, most modules will go into a sleep mode when the car is turned off. In order to query these components, a unique wake-up packet is required.

Depending on your model, you should have already performed reconnaisance on what networks are present. For example:

- powertrain/chassis M-CAN (ISO CAN C high speed)
- interior (body) I-CAN (ISO CAN B low speed)
- diagnosis D-CAN (high speed proprietary MB protocol)
- Digital Media Bus for radio/navigation system (MOST).

The reconnaisance stage is really important as this sets the scene for everything else you do. Thankfully there exists a huge amount of documentation for Mercedes-Benz that shows exactly where the components are, what the wiring is and what networks are present. 

![](images/canbuslocation1.jpg)

![](images/canbuslocation2.jpg)

![](images/canbuslocation3.jpg)

Some newer vehicles do a better job of isolating the diagnostic port. It works for diagnostics but since it doesn’t have a steady stream of data, due to it only responding with data as requested, it makes it much harder to "sniff" the bus. 

### K-line ISO 9141

This protocol, also known as Keyword Protocol 2000 or KWP. One underlying physical layer used for KWP2000 is identical to [ISO 9141](https://en.wikipedia.org/wiki/ISO_9141), with bidirectional [serial communication](https://en.wikipedia.org/wiki/Serial_communication) on a single line called the K-line. In addition, there is an optional L-line for wakeup. The data rate is between 1.2 and 10.4 [kilobaud](https://en.wikipedia.org/wiki/Baud), and a message may contain up to 255 bytes in the data field. 

When implemented on a K-line physical layer KWP2000 requires special *wakeup* sequences: *5-baud wakeup* and *fast-initialisation*. Both of these wakeup methods require timing critical manipulation of the K-line signal. (thanks Wikipedia!)

The initialization consists of either a 25ms low followed by a 25ms high and 10.4kbps communication OR the 5 baud init which begins with a 200ms low, a 400ms high, a 400ms low, a 400ms high, a 400ms low and ends with a 200ms high.