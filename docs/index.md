---
title: Welcome!
tags:
- tag1
- tag2
---

<center>
<font size= "8">Project Firesight</font><br>

<font size= "6"> Team Embermen</font><br>

<font size= "5"> Hannah Nair, Luke Willet, Musye Gaim, Joshua Petrone</font><br>

<font size= "5"> Fall 2025</font><br>

<font size= "5"> ASU, Class 2026, Professor Suo</font><br>

**Preparation Date: December, 7th, 2025**
</center>

## Project Summary

Project Firesight is a wireless weather station network that sends real-time environmental data to a central control panel. The weather stations utilize the BME280 sensor, which measures the environment's temperature, relative humidity, and pressure. The central control panel has rows of indicator LEDs for each environmental variable measured, where each row represents one weather station. On the end of each row is a red indicator LED, which lights when that weather station's area is deemed susceptible to wilfires, i.e. when two out of three of the envionmental indicator LEDs light up. Project Firesight allows the user to detect wildfire susceptible areas BEFORE a potential wildfire starts, creating a proactive approach to fighting wildfires which increases the efficiency by which wildfires are suppressed. 

*Figure 1: Project Firesight - Weather Station*
![Weather Station](weatherstation_struct.JPEG)

*Figure 2: Project Firesight - Control Panel*
![Control Panel PCB](controlpanel_pcb.jpg)

*Figure 3: Project Firesight - Weather Station PCB*
![Weather Station PCB](weatherstation_pcb.JPEG)

**_Note_**: The weather station PCB is the green PCB. During integration, the microcontroller on the weather station PCB fried, so the blue PCB's microcontroller was used. 

## Summary Table of Major Components 

| Part Name/Description                                                  | Unit Quantity | Unit Cost | Manufacturer      | Manufacturer Part #         | Vendor       |  Total Cost  | Order Total |
|------------------------------------------------------------------------|---------------|-----------|-------------------|-----------------------------|--------------|--------------|-------------|
| IC REG BUCK 3V 3A TO263                                                | 4             | $3.32     | Texas Instruments | LM2596S-(3.3V)/NOPB         | Digikey      |  $13.28      |  $168.73    |
| 9V 12 W AC/DC External Wall Mount (Class II) Adapter Fixed Blade Input | 1             | $6.23     | GlobTek, Inc.     | 1939-WR9HD1333CCP-F(R6B)-ND | Digikey      |  $6.23       |             |
| BME 280 Breakout Board                                                 | 2             | $8.99     | HiLetgo           | GY-BME280-3.3               | Amazon       |  $17.98      |             |
| LED RED DIFFUSED GULL WING SMD                                         | 5             | $2.01     | Broadcom Limited  | HLMP-Q150-F0011             | Digikey      |  $10.05      |             |
| LED BLUE ROUND 4SMD                                                    | 25            | $1.20     | Broadcom Limited  | ALMD-CB1E-VW002             | Digikey      |  $30.00      |             |
| Junction box enclosure.  5.9"D x 10.6"W x 14.6"H                       | 1             | $49.99    | Gratury           | G                           | Amazon       |  $49.99      |             |
| ESP32 Microcontroller                                                  | 5             | $5.06     | Espressif Systems | ESP32-S3-WROOM-1-N4         | Digikey      |  $25.30      |             |
| ESP32 Snap Programmer                                                  | 3             | $5.30     | M5 Stack          | S006                        | Electromaker |  $15.90      |

**_Note_**: The motor driver, DC motor, and internal temperature sensor were not included in the final prototype as the motor driver was unable to be properly soldered with the surface mount equipment provided at Peralta Lab. The OUT+ and OUT- pins that drive the motor would consistently short with the GND pin on the driver due to how small the driver and the pads were. Thus, the motor and related components are left out of the summary table as they were unused.

## Page Links

[Team Organization](./teamorg.md)

[Ideation and Concept Generation](./concept_gen.md)

[Component Selection](./component_selection/index.md)

[Block Diagram](./BlockDiag.md)

[Bill of Materials](./BOM.md)

[Team Schematic](./team-schematic.md)

