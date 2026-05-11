# Vehicle-tracking-NodeMCU
IoT-based Vehicle Tracking System using NodeMCU

## Objective
The objective of this project is to design an IoT-based vehicle tracking system using NodeMCU and GPS module to enable real-time monitoring.

## Overview 
This project is an IoT based monitoring system which will track the location of vehicles in real-time using NodeMCU and GPS technology.

## Technologies used 
1. NodeMCU
2. GPS module
3. LCD Display 
4. Micro USB cable
5. Arduino IDE

## Hardware components 
1. NodeMCU ESP8266
2. LCD display I2C module
3. GPS module NEO-6M
4. Jumper wires
5. Breadboard
6. Power supply

## Block diagram
<img width="638" height="572" alt="Block diagram" src="https://github.com/user-attachments/assets/1f129ba3-efda-439b-89c5-6a8334fced7d" />

## Hardware setup 
<img width="903" height="630" alt="Vehicle tracking" src="https://github.com/user-attachments/assets/bf0d3807-955d-45dc-a89f-05e29e4eebf4" />

## Working principle 
- When all modules are connected to NodeMCU, it reads location coordinates.
- GPS collects the coordinates latitude and longitude values along with date and time.
- NodeMCU enables the data communication via serial monitor.
- The coordinates are displayed on the LCD display.
- The data is collected and transmitted through Wi-Fi for monitoring.

## Sample code 
The source code is available at [https://github.com/Ramyashruti06/Vehicle-tracking-NodeMCU/blob/main/Vehicle_tracking.ino]

## Result
<img width="972" height="515" alt="Result" src="https://github.com/user-attachments/assets/913a84e6-2642-4518-83c7-efd068816fea" />

## Applications 
- GPS wildlife tracking.
- Oil and gas industry.
- Ambulance tracking and emergency medical services fleet.
- Logistics monitoring.

## Limitations 
- GPS signals might get jammed.
- Environmental conditions can cause interference in tracking.
- GPS accuracy might vary with signal strengths.
- Currently unavailable to test the hardware setup.

## Future Scope 
- Cloud integration for real-time tracking of vehicles.
- Mobile application support for multiple vehicle monitoring.
- SMS alert and notification system.
- Improved GPS accuracy for advanced modules.

## Learning Outcomes 
- Usage of software Arduino IDE.
- Implementation of IoT concepts.
- Wi-Fi based Transmission.
- Understanding real-time data transmission concepts. 

## Project status 
Worked on this in my academics as a mini project during my B.Tech.

## Author
KOTIKALAPUDI RAMYA SHRUTI
