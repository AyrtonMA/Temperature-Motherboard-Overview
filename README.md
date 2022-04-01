# Temperature Motherboard Overview
By: Ayrton Antenucci, Electric Powertrain Design, University of Toronto Formula Racing

Each year, the University of Toronto Formula Racing Team (UTFR) designs and builds a car to compete in international Formula SAE (Formula Student) events. As such, the team must ensure all elements of the vehicle, including the electric powertrain, comply entirely with Formula SAE regulations. This article will discuss the team’s ‘Temperature Motherboard’, including its purpose, functionality, and design. All of UTFR’s boards are fabricated in collaboration with JLCPCB (www.jlcpcb.com/RAT), a leading PCB manufacturer providing high quality, reliable, and cost-effective PCBs at a consistently rapid pace.

## Purpose and Functionality
    
As per Formula SAE (FSAE) regulations, the temperature of at least 20% of the cells within the accumulator must be monitored at all times. In addition, all circuits susceptible to high voltage (Tractive System or TS circuits) must be electrically isolated from low voltage circuits grounded to the chassis (Grounded Low Voltage or GLV circuits). 

UTFR’s battery management system (BMS) is responsible for receiving and monitoring cell temperatures over a CAN bus; however, the team has implemented Energus cell modules which feature built-in analog temperature sensors that are not directly compatible with the BMS. As such, the voltage readings from the sensors must be converted to temperatures and sent over CAN to the BMS. This is achieved in two stages:

<ol> 
  <li> A total of 15 boards (3 per 26-module segment) collect, multiplex, and galvanically isolate >20% of analog temperature readings, sending the output of each multiplexer to the Temperature Motherboard;
  
  <li> The Temperature Motherboard collects and multiplexes all 15 outputs of the previously multiplexed signals to send to an on-board MCU. The MCU controls the select signals for all multiplexers in the temperature monitoring system, converts analog readings to temperatures, and sends the data over a CAN bus to the BMS. 
</ol>

This ensures a sufficient number of cell temperatures are continuously monitored and that the temperature sensors (considered TS circuits) are electrically isolated from the BMS (a GLV circuit) as per FSAE regulations. 

## Schematic and PCB Design

The Temperature Motherboard PCB was designed entirely using Altium Designer. As is shown in the schematic below, the board incorporates 15 B050LS-1WR3 isolated 5V DC/DC converters (PS1-15), which provide isolated power to each of the 15 on-segment boards. A 16-1 multiplexer (U1) handles the 15 analog signals and sends it to an Arduino Micro (U2). The outgoing multiplexer select signals are driven through MOSFETs (Q1-3) and universally sent to the 15 on-segment boards. A modular CAN node (CAN1) is used to send the collected temperatures to the BMS.

![image](https://user-images.githubusercontent.com/88075549/161333206-9dd53325-ef52-4f42-9ae0-d714cc3ede2e.jpeg)

The Temperature Motherboard’s layout separates all GLV and TS circuits, as shown below. The 15 isolated DC/DC converters occupy the left-half of the board, labelled TS (Tractive System), to ensure GLV circuits cannot be exposed to high voltage.

![image](https://user-images.githubusercontent.com/88075549/161333278-38203ba7-dacc-43fc-afa4-3e01cc47f6d2.jpeg)

## Ordering and Fabrication

The Temperature Motherboard was manufactured with exceptional quality by JLCPCB within days of ordering. If desired, JLCPCB also offers professional SMT assembly with just a 24h turnaround time - more information can be found at www.jlcpcb.com/smt-assembly. The ordering process is remarkably simple:

<ol>
  <li> Export Gerber files of PCB project
  <li> Click ‘Order Now’ on www.jlcpcb.com
  <li> Upload Gerber files, confirm generated PCB requirements and preferences (including SMT assembly)
  <li> Once all PCBs are saved to cart, proceed to checkout.
<ol>
