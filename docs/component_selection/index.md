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

## Subsystem 4: Mechanical Casing & Inner Casing Temperature 

*Table 5: Mechanical Casing Selection*

### Mechanical Casing

1. High-grade ABS material

    ![](casing_1.png)

    * $21.99/each
    * [Product Link](https://www.amazon.com/Gratury-Waterproof-Enclosure-Electrical-370%C3%97270%C3%97150mm/dp/B08281V2RL/ref=asc_df_B0BFPXDN8M?tag=bingshoppinga-20&linkCode=df0&hvadid=80333201323789&hvnetw=o&hvqmt=e&hvbmt=be&hvdev=c&hvlocint=&hvlocphy=77827&hvtargid=pla-4583932719993871&th=1)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Weatherproof & waterproof                                         | Not fireproof                        |
    | Mounting panel included for easy PCB installation                 | Not lightning proof                  |
    | Lightweight                                                       |                     

2. Diecast Aluminum

    ![](casing_2.png)

    * $43.29/each
    * [Product Link](https://www.solutionsdirectonline.com/1550wgbk-9x6x2-diecast-aluminum-enclosure-hammond-manufacturing?msclkid=d75319495d7a1ac47a2a71958aeaedcd&utm_source=bing&utm_medium=cpc&utm_campaign=**LP%20Shop%20-%20Catch%20All%20-%20Brand%20%3E%20Hammond&utm_term=4583726566566583&utm_content=Catch%20All%20-%20Hammond)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | IP66 Rated                                                        | Heavy                                |
    | IP66 Gasket included                                              | Hard to modify/drill into            |
    | Powder Coated Black                                               | Not fireproof                        |

3. Fireproof Box

    ![](casing_3.png)

    * $42.50/each
    * [Product Link](https://www.amazon.com/SentrySafe-H0100-Fireproof-Waterproof-Cubic/dp/B00GE586CY?source=ps-sl-shoppingads-lpcontext&ref_=bing_fplfs&tag=txtadnwplace1-20&th=1)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Fireproof                                                         | Expensive                            |
    | Waterproof                                                        | Heavy                                |
    | Durable                                                           | Thick walls                          |

**Choice:** High-grade ABS 

**Rationale:** The high-grade ABS will be the best material and composition as it is waterproof to help with groundwater. Furthermore, it already has a PCB mounting method and it is easy to drill into to add our external sensors. Some people would argue that this is not the best option because it is not fireproof. This problem is solved by burying the box at least 1 foot underground. This will keep our electronics safe in the event of a wildfire. It is also the cheapest option.

*Table 6: Inner Casing Temperature Sensor Selection*

### Inner Casing Temperature Sensor

1. TC74A4-3.3VCTTR Temperature Sensor

    ![](casingsens_1.png)

    * $1.15/each
    * [Product Link](https://www.digikey.com/en/products/detail/microchip-technology/TC74A4-3-3VCTTR/443268)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Cheap                                                             | Fragile                              |
    | Fairly accurate                                                   | error margin up to 3 degrees         |
    | Fairly simple to solder                                           |                     

2. SLTM20W87F Temperature Sensor

    ![](casingsens_2.png)

    * $0.76/each
    * [Product Link](https://estore.st.com/en/stlm20w87f-cpn.html?)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Cheap                                                             | Fragile                              |
    | Measures up to 130 degrees Celsius                                | Older I2C timing                     |
    | Easy to solder                                                    | Slow temperature updates             |

3. AS6218-AWLT-L Temperature Sensor

    ![](casingsens_3.png)

    * $1.09/each
    * [Product Link](https://www.mouser.com/ProductDetail/ams-OSRAM/AS6218-AWLT-L?qs=xZ%2FP%252Ba9zWqY9z325DmyZ1Q%3D%3D&mgh=1&utm_source=chatgpt.com)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Measures up to 125 degrees Celsius                                | Fragile                              |
    | Accurate up to 0.8 degrees Celsius                                | Could be hard to solder              |
    | Can mount straight to PCB                                         |              

**Choice:** TC74A4-3.3VCTTR Temperature Sensor 

**Rationale:** The component we are going with is the TC74 because we have stock of this sensor and will not cost us to use. It will meet all the requirements needed for this sensor. If we did not have this sensor in stock the best option would be the SLTM20 due to it being the most resistant to high temperatures, has a better accuracy than the TC74, and is the cheapest unit.

### Inner Casing Motor Driver

*Table 7: Inner Casing Motor Driver Selecction*

1. TI DRV8835 Motor Driver

    ![](driver_1.png)

    * $1.95/each
    * [Product Link](https://www.digikey.com/en/products/detail/texas-instruments/DRV8835DSSR/3088201)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Cheap                                                             | Lower top motor voltage              |
    | Low Voltage Operation (VM input: 0-11V)                           | Lots of pins to solder               |
    | 1.5A continuous current                                           |                    

2. TI DRV8833 Motor Driver

    ![](driver_2.png)

    * $2.18/each
    * [Product Link](https://www.digikey.com/en/products/detail/texas-instruments/DRV8833CPWPR/4972147)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Built in current regulation                                       | Will shutdown at consistent high load|
    | Over temperature protection features                              | Uses more MCU pins than others       |
    | Compatible with 3.3V logic                                        |             

3. TI DRV8838 Motor Driver

    ![](driver_3.png)

    * $1.03/each
    * [Product Link](https://www.digikey.com/en/products/detail/texas-instruments/DRV8838DSGR/4767638?s=N4IgTCBcDaICICUBqAOFBmFcDKBxBIAugL5A)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Does not take up a lot of MCU I/O                                 | Solder using heat plate              |
    | Up to 1.8A continuous current                                     | No stall handling built in           |
    | Built in protections                                              | Needs good copper traces             |

**Choice:** TI DRV8838 Motor Driver 

**Rationale:** The best choice is the TI DRV8838 Motor Driver as it satisfies our basic project needs while having manageable cons compared to other choices. Even though it will require a heat plate to solder and needs good copper traces, these can be easily learned and implemented. In contrast, a motor driver that will shutdown at a consistent high load or use more MCU pins could lead to substantial issues. Furthermore, this motor driver has slightly more headroom on continuous current. 

## Subsystem 5: Wireless Communication 

*Table 8: Wireless Communication Selection*

### Wireless Communication

1. ESP-NOW

    ![](comm_1.png)

    * N/A cost
    * [Product Link](https://www.espressif.com/en/solutions/low-power-solutions/esp-now)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Low latency                                                       | Only pairs up to 20 devices          |
    | Simple API (no low level programming)                             | Only works with Espressif devices    |
    | Easily integrates with ESP32                                      |                     

2. ESP-MESH

    ![](comm_2.png)

    * N/A cost
    * [Product Link](https://www.espressif.com/en/products/sdks/esp-wifi-mesh/overview)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Up to 10Mbps of data transfer                                     | Greater power consumption            |
    | Mesh automatically forms                                          | More complex API                     |
    | Mesh self heals                                                   |                         
 
3. Bluetooth (ESP-IDF)

    ![](comm_3.png)

    * N/A cost
    * [Product Link](https://www.espressif.com/en/products/sdks/esp-idf)

    | Pros                                                              | Cons                                 |
    | ----------------------------------------------------------------- | -------------------------------------|
    | Lots of documentation and examples                                | Higher latency                       |
    | VS Code extension available                                       | Most complex API                     |
    | Security measures                                                 |                          

**Choice:** ESP-NOW 

**Rationale:** The best choice for wireless communication is ESP-NOW. Although it can only pair with up to 20 Espressif devices, our network topology only requires a single device to pair with four other ESP32s. Furthermore, the setup code is simpler compared to other communication protocols and has a lower latency, which is important for real-time wildfire prediction and detection.
