---
title: Block Diagram & Communication Sequence Diagram
---

The block diagram below details how the subsystems within Project Firesight interact with each other. The power subsystem takes in power from the battery and output 3.3 volts to all other subsytems for both the weather station and control panel. The internal temperature sensor, and the external environment sensor communicate with the microcontroller chip through I2C. The environmental sensor data (temperature, pressure, and relative humidity) is relayed to the control panel's microcontroller through the ESP-NOW communication protocol. The second weather station block (shown on the top right) relays it's environmental information to the control panel through the first weather station block using ESP-NOW. The control panel receives this data, compares it to the threshold values, and lights up LEDs correspondingly. 

*Figure 1: Project Firesight Block Diagram*

<img width="746" height="743" alt="image" src="https://github.com/user-attachments/assets/44370ea3-8682-4d24-b353-8e5e6c17f484" />

## Decision Making Process & Product Requirements

The decision making process for structuring the block diagram above revolved around simplicity and the examples given in class. The block diagram meets our product requirements as it measures three different types of environmental data from multiple stations, relays that data back to the control panel via ESP-NOW wireless communication, and the control panel actuates corresponding LEDs based on the data received. By doing so, the stakeholders receive real-time environmental data and information on areas that could produce a wildfire, which allows for proactiveness in wildfire suppression. All boards receive stable power, which is critical in allowing the project to function. Lastly, our block diagram showcases four subsystems working together (power, control panel LED actuators, wireless communication, microcontroller), which satisfies the product requirement of four subsystems working together. 