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
```
//Including Libraries
#include <TinyGPS++.h>
#include <SoftwareSerial.h>
#include <ESP8266WiFi.h>
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27, 16, 2);
TinyGPSPlus gps;  // The TinyGPS++ object
SoftwareSerial ss(4, 5); // The serial connection to the GPS device(tx,rx)
const char* ssid = "Your_userID";
const char* password = "Your_Password";//WiFi details
float latitude , longitude;
int year , month , date, hour, minute , second; String date_str , time_str , lat_str , lng_str; int pm;
WiFiServer server(80);
void setup() // Setting up the LCD display and WiFi connection
{
Wire.begin(2,0); // initializing the LCD lcd.init();
// Enable or Turn On the backlight lcd.backlight();
lcd.print("Vehicle Tracking"); delay(2000); Serial.begin(9600); ss.begin(9600); Serial.println(); Serial.print("Connecting to..."); lcd.println(WiFi.localIP());
Serial.println(ssid);
WiFi.begin(ssid, password);
while (WiFi.status() != WL_CONNECTED)
{ delay(500); Serial.print("."); lcd.setCursor(0, 0); lcd.print("WiFi connecting...\n");
Serial.print("WiFi connecting\n");
}
Serial.println("");
// Serial.println("WiFi connected");
server.begin();
Serial.println("Server started");
// Print the IP address Serial.println(WiFi.localIP());
lcd.setCursor(0, 0); lcd.print("WiFi connected \n"); delay(2000);
Serial.print("WiFi connected\n"); lcd.setCursor(0, 1); lcd.print(WiFi.localIP()); delay(2000); }
void loop() // for establishing the GPS connection and receiving the coordinates
{
while (ss.available() > 0)
if (gps.encode(ss.read()))
{
if (gps.location.isValid())
{
latitude = gps.location.lat(); lat_str = String(latitude , 6); longitude = gps.location.lng(); lng_str = String(longitude , 6);
}
if (gps.date.isValid())
{
date_str = ""; date = gps.date.day(); month = gps.date.month(); year = gps.date.year();
if (date < 10)
date_str = '0';
date_str += String(date);
date_str += " / ";
if (month < 10)
date_str += '0';
date_str += String(month);
date_str += " / ";
if (year < 10)
date_str += '0';
date_str += String(year); }
if (gps.time.isValid())
{
time_str = ""; hour = gps.time.hour(); minute = gps.time.minute(); second = gps.time.second();
minute = (minute + 30); if (minute > 59) { minute = minute - 60; hour = hour + 1; }
hour = (hour + 5) ; if (hour > 23) hour = hour - 24;
if (hour >= 12)
pm = 1; else
pm = 0;
hour = hour % 12;
if (hour < 10)
time_str = '0';
time_str += String(hour);
time_str += " : ";
if (minute < 10)
time_str += '0';
time_str += String(minute);
time_str += " : ";
if (second < 10)
time_str += '0';
time_str += String(second);
if (pm == 1)
time_str += " PM ";
else time_str += " AM ";
}
}
// Check if a client has connected WiFiClient client = server.available(); if (!client)
{
return;
}
// Prepare the response using the HTTP server
String s = "HTTP/1.1 200 OK\r\nContent-Type: text/html\r\n\r\n <!DOCTYPE html> <html>
<head> <title>GPS Interfacing with NodeMCU</title> <style>"; s += "a:link {background-color: BLUE;text-decoration: none;}";
s += "table, th, td {border: 1px solid black;} </style> </head> <body> <h1  style="; s += "font-size:300%;";
s += " ALIGN=CENTER> GPS Interfacing with NodeMCU</h1>"; s += "<p ALIGN=CENTER style=""font-size:150%;""";
s += "> <b>Location Details</b></p> <table ALIGN=CENTER style="; s += "width:50%";
s += "> <tr> <th>Latitude</th>"; s += "<td ALIGN=CENTER >";
s += lat_str;
s += "</td> </tr> <tr> <th>Longitude</th> <td ALIGN=CENTER >"; s += lng_str;
s += "</td> </tr> <tr>  <th>Date</th> <td ALIGN=CENTER >"; s += date_str;
s += "</td></tr> <tr> <th>Time</th> <td ALIGN=CENTER >"; s += time_str;
s += "</td>  </tr> </table> ";
if (gps.location.isValid())
{ s+="<p align=center><a style=""color:YELLOW;font-size:125%;"" href=""http://maps.google.com/maps?&z=15&mrt=yp&t=k&q=";
s += lat_str; s += "+"; s += lng_str;
s += """ target=""_top"">Click here!</a> To check the location in Google maps.</p>";
}
s += "</body> </html> \n";
client.print(s); delay(100);
}
```
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
