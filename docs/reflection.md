---
title: Reflection
---

## Lessons Learned 

1. Research as much as possible 

Researching as much as possible will decrease the build and integration time significantly. By ensuring all circuits are accurate and all components are rated to work together, there will be less debugging errors that pop up, thereby allowing the project to be completed quicker. 

2. Verify the right components were soldered 

Sometimes the simplest mistake is the one that is usually made. If two different voltage regulators are in the project components, ensure that the right voltage regulator is used for it's respective circuit components. This was the reason why the voltage regulator system was not working on the control panel board during the first test. 

3. Get large surface mount components 

The college you are in will not always have the best or precise lab equipment. Furthermore, small surface mount components are extremely hard to hand solder if you have no prior experience. Make life easier for yourself and use large surface mount components, as the risk of shorting any pins is very low. 

4. Don't just check the datasheet, verify the datasheet

Often times, the datasheet does not include all important information pertaining to your component. Look for additional advice on the internet from other people, whether it be forums or YouTube tutorials. The ESP32-S3-WROOM-1 datasheet did not specify that the boot pin needs a pullup resistor. The state of the boot pin is CRITICAL in executing logic. This likely prevented two of our microcontroller boards from working. 

5. Be cautious and think ahead

Always have a back up plan for critical systems. The datasheet did not say that the built in USB compiler within the ESP32-S3 chip ONLY works if there is code in the ESP32-S3 chip. But a freshly bought chip has no code in it, so it was impossible to first program the chips with the USB connector, as initially planned. Having the snap programmer as a back up plan to program the board was critical in this project's success. 

6. Focus on minimum viable product first 

With engineers, there is a tendency to dream up grand projects with complex functions. Start with the bare minimum first, as it will satisfy your stakeholders but also save yourself from a headache. Once the bare minimum has been accomplished, then build upon it. 

7. Integrate each code section one at a time 

When integrating multiple components' logic together, start with one component at a time. That way, if multiple components have issues in them, you'll spot their errors one at a time, which can be less overwhelming than seeing multiple errors all at once. 

8. Don't hand solder SMD components on an empty stomach

An empty stomach produces shaky hands and a less intelligent brain. Soldering SMD components is much easier if your hands are steady. 

9. Connect all of your MCU's GPIOs to male/female header pins 

When hand soldering your MCU, it is possible that you can short two important pins together. Sometimes, it is impossible to figure out how they shorted. By connectiong all of your MCU's GPIOs to pins that jumper wires can connect to, it gives your project flexibility. 

10. Buy plenty of microcontroller chips 

Microcontroller chips can be finicky, especially the ESP32 ones. Buying plenty of microcontroller chips ensures you are covered if some of them don't work. This is partially the reason why Project Firesight only had one weather station board working, as the rest of the ESP32 chips would not execute their program. 

## Top 5 Recommendations for Future Students

1. Research your circuits and your components as much as possible. This reduces the amount of errors that pop up later in the project. 

2. Practice surface mount soldering. Everything becomes better with practice, and it is important to solder your components correctly to ensure your project functions as intended. 

3. Get large surface mount components. The project can satisfy grade requirements while also being easier to solder. 

4. Practice desoldering components. It is likely that mistakes will be made when hand soldering, so another important skill is knowing how to desolder. It will also save you time and frustration if you can quickly fix a short. 

5. Pay attention to detail when soldering your boards. The components can look very similar to each other, and mistakes can happen. Soldering your circuits correctly will decrease debugging time. 

## Version 2.0 

### Communication Architecture 

The communication architecture could be improved by adding an acknowledgement from the control panel that it successfully received the wireless data. This could be done by creating a helper function in the control panel code, which would send a string back to the weather station. The weather station would have a helper function to decode the received acknowledgement, which would light up an extra LED when it receives an acknowledgement. This would give a visual indicator when the weather stations are successfully connected to the control panel. 

The communication architecture could also be improved by using ESP-MESH. This wireless communication protocol is specifically designed to work with a network of devices. While ESP-NOW can accomplish this, it requires more lines of code than ESP-MESH. 
