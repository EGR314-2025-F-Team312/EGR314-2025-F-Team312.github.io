---
title: ESP32 Pinout Table
---

## Control Panel Board 

| GPIO Pin # | Function                                       | Connects To What Board Component                                    |
|------------|------------------------------------------------|---------------------------------------------------------------------|
| 0          | MCU Boot Pin                                   | Snap Programmer Boot Male Header Pin, Boot Male Header Pin          |
| 1          | UART RX                                        | UART RX Male Header Pin                                             |
| 2          | UART TX                                        | UART TX Male Header Pin                                             |
| 4          | Weather Station 1 Temperature LED Signal       | Weather Station 1 Temperature 220 Ohm Resistor                      |
| 5          | Weather Station 1 Relative Humidity LED Signal | Weather Station 1 Relative Humidity 220 Ohm Resistor                |
| 6          | Weather Station 1 Pressure LED Signal          | Weather Station 1 Pressure 220 Ohm Resistor                         |
| 7          | Weather Station 1 Wildfire LED Signal          | Weather Station 1 Wildfire 220 Ohm Resistor                         |
| 9          | Weather Station 2 Temperature LED Signal       | Weather Station 2 Temperature 220 Ohm Resistor                      |
| 10         | Weather Station 2 Relative Humidity LED Signal | Weather Station 2 Relative Humidity 220 Ohm Resistor                |
| 11         | Weather Station 2 Pressure LED Signal          | Weather Station 2 Pressure 220 Ohm Resistor                         |
| 12         | Weather Station 2 Wildfire LED Signal          | Weather Station 2 Wildfire 220 Ohm Resistor                         |
| 13         | VBUS Sense                                     | Between 100kOhm and 150 kOhm Resistors                              |
| 19         | Data Minus Pin                                 | Micro USB-B Data Minus Pin                                          |
| 20         | Data Plus Pin                                  | Micro USB-B Data Plus Pin                                           |
| 43         | TXD0 MCU Programming                           | Snap Programmer TXD0 Male Header Pin                                |
| 44         | RXD0 MCU Programming                           | Snap Programmer RXD0 Male Header Pin                                |
| EN         | MCU Enable Pin                                 | EN Push Button, 0.1uF Capacitor, Snap Programmer EN Male Header Pin |

## Weather Station Board

| GPIO Pin # | Function                     | Connects To What Board Component                                    |
|------------|------------------------------|---------------------------------------------------------------------|
| 0          | MCU Boot Pin                 | Snap Programmer Boot Male Header Pin, Boot Male Header Pin          |
| 1          | UART RX                      | UART RX Male Header Pin                                             |
| 2          | UART TX                      | UART TX Male Header Pin                                             |
| 4          | Motor Driver Sleep Logic Pin | Motor Driver Sleep Pin                                              |
| 5          | VBUS Sense                   | Between 100kOhm and 150 kOhm Resistors                              |
| 6          | Motor Driver PH Logic Pin    | Motor Driver PH Pin                                                 |
| 7          | Motor Driver EN Logic Pin    | Motor Driver EN Pin                                                 |
| 8          | Serial Data Line (SDA)       | SDA Screw Terminal, 4.7 kOhm Resistor, Sensor SDA Pins              |
| 9          | Serial Clock Line (SCL)      | SCL Screw Terminal, 4.7 kOhm Resistor, Sensor SCL Pins              |
| 19         | Data Minus Pin               | Micro USB-B Data Minus Pin                                          |
| 20         | Data Plus Pin                | Micro USB-B Data Plus Pin                                           |
| 43         | TXD0 MCU Programming         | Snap Programmer TXD0 Male Header Pin                                |
| 44         | RXD0 MCU Programming         | Snap Programmer RXD0 Male Header Pin                                |
| EN         | MCU Enable Pin               | EN Push Button, 0.1uF Capacitor, Snap Programmer EN Male Header Pin |
