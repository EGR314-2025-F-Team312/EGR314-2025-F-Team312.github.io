---
title: Final Schematic and PCB
---
The EDA software used for this project was KiCad. The team schematic and PCBs are split into two -- one for the main control panel and one for the weather stations.

The KiCad project file zip can be downloaded by this link: [KiCad Projects File](https://github.com/EGR314-2025-F-Team312/EGR314-2025-F-Team312.github.io/raw/refs/heads/main/project_firesight_EDA.zip)

The Gerber Drill files zip can be downloaded by this link: [KiCad Gerber File](https://github.com/EGR314-2025-F-Team312/EGR314-2025-F-Team312.github.io/raw/refs/heads/main/project_firesight_gerber.zip)

## Schematic

### Main Control Panel Circuit

*Figure 1: Control Panel Schematic*

![Control Panel](team312_controlpanel_v1.svg)

### Weather Station Circuit

*Figure 2: Weather Station Schematic*

![Weather Station](team312_weatherstation_v1.svg)

The schematic satisfies the user needs of the project as the power regulator circuit supplies +3.3V to all required power pins for all components in the weather station & control panel schematic. The product won't function as intended if it doesn't receive any power. The microcontroller for both schematics can be programmed either through the USB D- and D+ lines or through the snap programmer, in case any of the two options fail. This satisfies user needs as it provides the logic for the product, which allows for the transmission of real-time environmental data through wireless communication. For the control panel, the logic will indicate what areas are susceptible to wildfires, which enables proactive wildfire supression. 

### Schematic Design & Decision Making Process

The schematic was designed to be as readable and simple as possible. Net labels were used to clean up schematic connections and improve readability. Subsystems were split into different areas on the schematic for organization, and text was placed where needed to add clarity.  

## PCB Design

### Control Panel PCB

*Figure 3: Front Copper Layer - Control Panel*

![Control Panel PCB Front](controlpanel_pcb_front.png)

*Figure 4: Back Copper Layer - Control Panel* 

![Control Panel PCB Back](controlpanel_pcb_back.png)

### Weather Station PCB 

*Figure 5: Front Copper Layer - Weather Station* 

![Weather Station PCB Front](weatherstation_pcb_front.png)

*Figure 6: Back Copper Layer - Weather Station*

![Weather Station PCB Back](weatherstation_pcb_back) 

### PCB Design & Decision Making Process

The PCB design process aimed for simplicity and to keep subsystems near each other as much as possible. Components were organized onto the board first before connections were made. All boards utilize two layers, a front copper layer as the positive power plane and a back copper layer as the ground power plane. This was done to decrease the amount of connections on the board and increase simplicity. Silkscreen text was added to increase clarity when soldering. 

### Version 2.0

For version 2.0 of the hardware design, more silkscreen comments would be added to further increase the clarity of the board when making connections to other hardware components or during soldering. This is an important change as it would decrease the time it would take for soldering and testing, and also ensures that no wrong connections are made that could harm the components on the board. Version 2.0 of Project Firesight would have a casing for the control panel such that the bare PCB is not exposed. This would increase the longevity of the product and protect critical components. In addition, all GPIO pins on the microcontroller for both boards would be connected to male header pins, which would provide flexibility during project integration if the initially planned pins were shorted during soldering. Lastly, version 2.0 would use surface mount components that have pins extending from the SIDE of the component, not copper pads on the back. This would make hand-soldering much easier and prevent accidental shorts (which is what happened with our motor driver). 





