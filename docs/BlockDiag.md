---
title: Block Diagram & Communication Sequence Diagram
---

The block diagram below details how the subsystems within Project Firesight interact with each other. The power subsystem takes in power from the battery and output 3.3 volts to all other subsytems for both the weather station and control panel. The internal temperature sensor, and the external environment sensor communicate with the microcontroller chip through I2C. The environmental sensor data (temperature, pressure, and relative humidity) is relayed to the control panel's microcontroller through the ESP-NOW communication protocol. The second weather station block (shown on the top right) relays it's environmental information to the control panel through the first weather station block using ESP-NOW. The control panel receives this data, compares it to the threshold values, and lights up LEDs correspondingly. 

*Figure 1: Project Firesight Block Diagram*

<img width="746" height="743" alt="image" src="https://github.com/user-attachments/assets/44370ea3-8682-4d24-b353-8e5e6c17f484" />

### Decision Making Process & Product Requirements

The decision making process for structuring the block diagram above revolved around simplicity and the examples given in class. The block diagram meets our product requirements as it measures three different types of environmental data from multiple stations, relays that data back to the control panel via ESP-NOW wireless communication, and the control panel actuates corresponding LEDs based on the data received. By doing so, the stakeholders receive real-time environmental data and information on areas that could produce a wildfire, which allows for proactiveness in wildfire suppression. All boards receive stable power, which is critical in allowing the project to function. Lastly, our block diagram showcases four subsystems working together (power, control panel LED actuators, wireless communication, microcontroller), which satisfies the product requirement of four subsystems working together. 

## Communication Sequence Diagram 

The communication sequence diagram, in the figure below, satisfies user needs and product requirements by initializing ESP-NOW communication between all weather stations and the control panel, continuosly reading environmental data from the BME280 sensors for each weather station, and sending that data back to the control panel. If the control panel receives a data packet that is the length expected, it will decode that data, store it in it's respective environmental data variables, and light up LEDs correspondingly if the environmental data surpasses the threshold value. If the length of the packet does not match what is expected, that data packet is ignored. Initializing ESP-NOW communication allows for wireless communication and reduces disruption to the environment that the weather stations are in, which satisfies the wireless communication product requirement and the user need of minimizing environmental disruptions. Checking the packet length ensures that no data is received that is not from the weather stations, which verifies that accurate data is received by the control panel, allowing for proactive wildfire supression. 

*Figure 2: Communication Sequence Diagram*
![Communication Sequence Diagram](communication_diagram.png)

### Communication Message Structure 

The communication message structure for the environmental data was structured to be as simple as possible. The structure of the message from the weather stations is a float variable for temperature, pressure, and relative humidity, and an unsigned integer for a time stamp that the data was sent, using the millis() function. The weather stations send their environmental data every loop scan, and the control panel processes that environmental data packet every time an ESP-NOW message arrives on radio via the esp_now_register_recv_cb() function and the OnDataRecv() function, which are built in ESP-NOW library functions. Please see the Appendix for the full control panel and weather station code. 

## Top Five Software Changes 

### Micropython To C++ 

The code was initially set to be programmed through micropython. However, due to continuous microcontroller programming issues with VS Code Pymakr extension, and the lack of time available to translate the example ESP-NOW Arduino code given in class (which was in C++) to micropython, the software was written in C++ instead and programmed through Platform IO, as that was proven to work with previous lab assignments. 

### Adding Serial Print Lines for ESP-NOW Debugging

The initial code written had no serial print lines to dictate which part of the code has been executed. This provided the team with no feedback on what part of the code was not working, which makes debugging immensely difficult. Thus, serial print lines were added in sections of the code to communicate which sections of the code processed, and where it was stuck. 

### Time Stamp Data Addition 

When the code first worked, environmental data was measured and successfully sent over to the control panel. However, when trying to trigger all LEDs for demonstration purposes, it was difficult determining if the environmental data was stagnating (and therefore, not reaching the threshold values to trigger the LEDs), or if the ESP-NOW connection was lost. A time stamp variable was added to the data payload to fix this, as it would ALWAYS change each time the environmental data was received. 

### PWM Breathing Code Library

Initially, the PWM breathing code for the LEDs was written by utilizing the analogWrite() function within Arduino. However, further research found that ESP32 has a built in PWM controller library for LEDs. To increase simplicity and code readability, this library was utilized. 

### PWM Breathing Delay

The initial delay that determined how intense the LEDs would breathe was accomplished by the delay() function. However, since multiple LEDs may be breathing at the same time, the delay() function could not be utilized as it stops the microcontroller frome executing any code at all. To fix this, the millis() function was utilized and compared to a time stamp constant. 
