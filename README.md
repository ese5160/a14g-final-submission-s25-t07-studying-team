[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/AlBFWSQg)
# a14g-final-submission

    * Team Number: 07
    * Team Name: Studying Team
    * Team Members: Guanlin Li, Xinmi Wang
    * Github Repository URL: https://github.com/ese5160/a14g-final-submission-s25-t07-studying-team
    * Description of test hardware: 

## 1. Video Presentation

## 2. Project Summary

### Device description

This device is a force-feedback knob that should be able to imitate the feeling of a mechanical knob, including level-devided knob, level-less knob, and limitation of knobs. The user should be able to send the data of the knob to the node-red so that it could control other devices, such as temperature, volume, and all other stuffs that could be adjusted using a knob. 

This project is inspired by an online project that uses a brushless dc motor to provide force-feedback to a knob. Using the motor, the knob could give different force-feedback to the user, making the knob highly adjustable. 

The knob could be used as a central control for in-home smart device control. For example, it could set the desired temperature using the knob, which could give a level-devided feeling to the user when they choose between each level of temperature. In detail, if the user wishes to spin the temperature from 70F to 71F, they will feel the force that tries to move the knob back to 70F before they reached the midpoint between these two temperature, and the force that spins towards 71F when they go pass the midpoint. Also, we can set a boundary where the knob will always tries to move back if the user spins out of bound. For example, if the upper bound is 80F, then the knob will always try to return to 80F if the user spins it beyond 80F. 

The internet is an important part to our project, as the knob needs to send the current readings to different devices in order to control them. Therefore, we need to send the current mode, the button status, and the readings to node-red using MQTT so that the user could use them as they wanted. 

### Device functionality



### Challenges

There are all kinds of challenges that we faced. The first one is the driver for the LCD screen and the motor. Since our project is using C and there's no library for the motor and the LCD screen that writes in C, we have to make our own library. We checked different datasheets and examples and we finally figured out how to initialize and send data/commands the LCD screen. However, we were unable to fully control the motor at the end. We were also not sure where the motor went wrong, since our code matches the workflow of FOC control. Therefore, the spring-like motor will be the only mode we could demonstrate. We will work on this motor during the summer and hopefully we could figure out a way to control it. 

The second challenge is from our hardware manufacturer. When our boards arrived, the 7V4 on all three of the boards are not working. We used the oscilloscope to check the output of the 7V4, and we found that the chip is trying to power up but immediately entered protect mode that reset the chip and output. We then probed voltages across the converter and finally discovered that the voltage at the feedback is not correct - it should be around 1.2V as the reference voltage should be, but it rises all the way to 2.5V. We then probed the resistance of the two resistor that forms the voltage devider of the feedback end, and discovered that the manufacturer accidentally swapped the two resistor, causing abnormal voltage at the feedback pin. The 7V4 functions as expected after we swapped the two resistors back. 

We also found a channel conflict when we are trying to wrap everything up. The WiFi module on the chip uses SERCOM2 to communicate with the MCU. However, the LED and the I2C sensor also requires SERCOM0/SERCOM2. Therefore, we only have 2 channels available while we have 3 devices that needs to use them. This was discovered only several hours before the demo, so we were unable to fix this issue. If more time were given, we could probably find spare pins that uses other SERCOM and connect it to the LED signal jumper, thereby resolve this issue. 

During the integration, we also found that the LCD signal cannot be derived from the MCU. This stops our LCD from displaying the data that we need to show to the user in order to provide any visual feedback. We have no time to address this, although we tried to scrape off the cover of the output line and weld an enameled wire from it to connect to our logic analyzer. We speculate that there might be some connection problem from the MCU to the board, or there might be software problems that redefined the mode of the MOSI line.

### Prototype learnings

We learned alot when assembling our prototype and testing it. For example, we learned that if the power regulator is not working, we should first connect an oscilloscope to it and check the output of it. If we see that the regulator is struggling to power up and put back into protection mode immediately, there could be something to do with the feedback voltage. 

Also, we should test everything on the dev board before making the PCB. The course is kind of rush so we have no time to validate our idea, therefore, we were not able to accomplish our target and there are mistakes discovered later that could be prevented if we validate it beforehand. 

If we can start it over again, we would probably first validate the motor to see if it could work. We spend excessive time on the motor driver but were unable to bring a satisfying driver at the end. Also, we would prevent the use of SERCOM2 for the LED signal pin by changing the pin to other pin that uses SERCOM1 for example. Also, we would move the LCD screen's connector closer to the MCU so that it won't be interfered by other noisy signals. We also connect the wrong pin for the LCD screen (MOSI and SCLK on the wrong pad of SERCOM20). We would also adjust this one if possible. 

### Next steps & Takeaways

A working motor driver is needed to finish this project. Currently, we are not able to fully control the motor. Also, we need to make the LCD screen of the device working. Currently, the LCD screen is not working due to unknown reason, and we wish to find out the reason behind it. 

A main thing we learned in this course is to validate the idea and driver for every part in the project before actually build the PCB board. Personally for me (Guanlin), I think the most interesting part in this course is about the bootloader. I always heard this part during my projects, online resources, and even in 5190, but this is the first time I actually write a bootloader that updates my firmware. I learned alot during the implementation of the bootloader. 

### Project links

Node-Red link: [CLICK HERE](http://172.178.40.121:1880/#flow/9ecac7261ee87947)

Node-Red UI: [CLICK HERE](http://172.178.40.121:1880/ui/#!/0?socketid=yH4iVXIwXRf_c1zhAAAJ)

Altium link: [CLICK HERE](https://upenn-eselabs.365.altium.com/designs/2CB5A97B-359C-4D7A-BC51-302EB17B2030#design)


## 3. Hardware & Software Requirements

## 4. Project Photos & Screenshots

## Codebase

- A link to your final embedded C firmware codebases
- A link to your Node-RED dashboard code
- Links to any other software required for the functionality of your device

