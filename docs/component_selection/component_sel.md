---
title: Component Selection 
---

## Subsystem 1: Power

*Table 1: Power Component Selection*

### Bucking Voltage Regulator

1. LM2575M-3.3 Bucking Voltage Regulator

    ![](power_1.png)

    * $0.94/each
    * [Product Link](https://www.digikey.com/en/products/detail/rochester-electronics-llc/LM2575M-3-3/12118456)

    | Pros                                      | Cons                                                             |
    | ----------------------------------------- | ---------------------------------------------------------------- |
    | Relatively solder friendly                | Generates switching noise ripple                                 |
    | No heat sink required in some designs     | Limited to 1A output                                             |
    |                                           | Efficiency drops under light loads

2. LM7805MPX/NOPB Bucking Voltage Regulator

    ![](power_2.png)

    * $1.43/each
    * [Product Link](https://www.digikey.com/en/products/detail/texas-instruments/LM7805MPX-NOPB/6110583)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Very low noise output                                             | Poor efficiency at high voltages     |
    | Doesn't require many external components                          | Limited to 1A output                 |
    | Widely available and inexpensive                                  |

3. LM2596S-(5.0/3.3V)/NOPB Bucking Voltage Regulator

    ![](power_3.png)

    * $6.97/each
    * [Product Link](https://www.digikey.com/en/products/detail/texas-instruments/LM2596S-5-0-NOPB/334842)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | High efficiency at moderate to high current                       | Generates switching noise            |
    | Has a shutdown feature                                            | Feedback trace must be isolated      |
    | Widely used, readily available reference designs                  | May be difficult to solder           |

**Choice:** LM2596S-(5.0/3.3V)/NOPB Bucking Voltage Regulator

**Rationale:** The best choice is the LM2596S/NOPB for 5V output and 3.3V as it has a high efficiency at a much higher current load (3A), incorporates a shutdown feature, and is widely used with available reference designs. The high current load is better suited for our project as we will be using a small DC motor to close the underground PCB box in the event of extreme weather conditions. Furthermore, the shutdown feature can be used to turn off all critical components in the event that the underground PCB box must close.

## Subsystem 2: Sensors 

*Table 2: Sensor Component Selection*

### Atmospheric Sensors

1. BME 280 - Humidity, Temperature, and Pressure Sensor

    ![](sensor_1.png)

    * $4.03/each
    * [Product Link](https://www.digikey.com/en/products/detail/bosch-sensortec/BME280/6136306)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Low power consumption                                             | Sensitive to harsh weather           |
    | Senses 3 data types                                               | More complex coding                  |
    | API library available for use on github                           |                     

2. AMG8833-Temperature IR Sensor

    ![](sensor_2.png)

    * $1.43/each
    * [Product Link](https://www.digikey.com/en/products/detail/texas-instruments/LM7805MPX-NOPB/6110583)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Very low noise output                                             | Poor efficiency at high voltages     |
    | Doesn't require many external components                          | Limited to 1A output                 |
    | Widely available and inexpensive                                  |

3. SHT31-DIS-B2.5KS - Humidity & Temperature Sensor

    ![](sensor_3.png)

    * $4.01/each
    * [Product Link](https://www.digikey.com/en/products/detail/sensirion-ag/SHT31-DIS-B2-5KS/5872252?)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Two distinctive, user selectable I2C addresses                    | Generates switching noise            |
    | Wide input voltage range                                          | Feedback trace must be isolated      |
    | NIST traceable measurements (industry standard)                   | May be difficult to solder           |

**Choice:** BME 280 - Humidity, Temperature, and Pressure Sensor

**Rationale:** The best choice for this subsystem is the BME 280 as it senses multiple variables within one package, which prevents I2C bus problems. The code is intensive, but an API library is available on github and the datasheet offers code examples to follow.  

## Subsystem 3: Control Panel 

*Table 3: Red LED Component Selection*

### Wildfire Susceptibilite Indicating LED

1. HLMP-Q150-F0011 Red LED

    ![](led_1.png)

    * $2.01/each
    * [Product Link](https://www.digikey.com/en/products/detail/broadcom-limited/HLMP-Q150-F0011/1235258)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Easiest to solder                                                 | Expensive                            |
    | High visibility                                                   | Takes up space                       |
    | Heat resistant                                                    |                     

2. SML-D12U1WT86 LED

    ![](led_2.png)

    * $0.12/each
    * [Product Link](https://www.digikey.com/en/products/detail/rohm-semiconductor/SML-D12U1WT86/5843853)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Inexpensive                                                       | Vulnerable to thermal cycling        |
    | Compact                                                           | Difficult to solder                  |
    | Very bright for its size                                          |

3. APT2012SURCK LED

    ![](led_3.png)

    * $0.20/each
    * [Product Link](https://www.digikey.com/en/products/detail/kingbright/APT2012SURCK/1747532)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Low power consumption                                             | Difficult to solder                  |
    | Small footprint                                                   | Fragile                              |
    | Vibrant red, suitable for status indication                       |            

**Choice:** HLMP-Q150-F0011 Red LED

**Rationale:** Option 1 is the best choice for our design because it’s the least fragile and easiest to manually solder of the 3. Furthermore, having the highest visibility possible is important for warning the user of wildfire susceptibility.

*Table 4: Sensor LED Component Selection*

###  Sensor Threshold LEDs

1. XL-1606UBC LED

    ![](led_4.png)

    * $0.01042/each
    * [Product Link](https://www.digikey.com/en/products/detail/xinglight/XL-1606UBC/25673224?s=N4IgjCBcoMwOxVAYygMwIYBsDOBTANCAPZQDaIMATAAwAstEAuoQA4AuUIAymwE4CWAOwDmIAL6EAbAE5EIFJAw4CIAG6CofAK4qSkcrWrSYxkMxDtOPASPGEYYWdHloseQnvJhKAVkoxJM1YOSG4%2BIVEJEABaQOcFbV0yCjMo6Mo5BN4dD2SfVKj85xYoMFYSyF8ouNB%2BABNOeBBgq3DbQjYATxZcTjrsFDExIA)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Inexpensive                                                       | Difficult to solder by hand          |
    | Compact footprint                                                 | Lower visibility                     |
    | Low power consumption                                             |                     

2. ALMD-CB1E-VW002 LED

    ![](led_5.png)

    * $1.20/each
    * [Product Link](https://www.digikey.com/en/products/detail/broadcom-limited/ALMD-CB1E-VW002/7325047)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Low power consumption                                             | Takes up space                       |
    | Fast switching speed                                              | Limited viewing angle                |
    | High brightness                                                   |

3. 150141RB73100 RGB LED

    ![](led_6.png)

    * $0.34/each
    * [Product Link](https://www.digikey.com/en/products/detail/w%C3%BCrth-elektronik/150141RB73100/4489963)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | RGB LED                                                           | Thermal management complications     |
    | Compact                                                           | Requires multiple control channels   |
    | Vibrant red, suitable for status indication                       |            

**Choice:** ALMD-CB1E-VW002 Blue LED

**Rationale:** Option 2 is the best choice for sensor threshold indication (humidity, temperature, wind direction) because of its low power consumption and high visibility. Furthermore, the RGB function of option 3 would go unused, making the further subsystem design complications unnecessary.

