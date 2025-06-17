# Interactive-Medicine-Box-for-Children
Embedded System Project Building a Interactive Medicine Cabinet for Children using Arduino Uno

<img width="638" alt="Box 1" src="https://github.com/user-attachments/assets/8a43e11e-4e39-4536-a1bd-c2f5992be1cf" />

(Box in closed state)

<img width="659" alt="Box 2" src="https://github.com/user-attachments/assets/b47c8fdc-25c5-4765-9db2-e71b09ddb432" /> 

(Box in opened state)


# Our Team
- Adika Rizky Primantoro (235150301111011) 
- Haniif Zaahid Nashrullah (235150300111007) 
- Muhammad Eka Wardana (235150307111004) 
- Muhammad Syauqi Fadillah (235150307111005) 
- Muhammad Raka Naufal (235150307111007) 

## Project Domain
This project focus on automation of giving children their medicine on time with the help of RTC sensor to track time, servo for the opening and closing mechanism, push button for interactive purposes, and DFPlayer for storing audio files and outputted to the speakers to make sound that interact with the children. With Arduino Uno Microcontroller.

### Problem Statements

- Administering medication to children is often challenging due to the unpleasant taste of the medicine, fear, or boredom, leading to non-compliance with treatment.
- That can potentially worsen their health condition if the medication is late or not taken at all.
- The children may forget when to take their medicine.

### Goals
- Automate the time when to take the medicine using the help from RTC sensor.
- Provide an interactive experience for children to take their medicine.

### Solution Statements
- Offers an innovative solution by combining safe medicine storage with interactive features.
- Interactive features such as schedule reminders, cheerful music tones, and rewards for children to enhance their motivation.
- Equipped with aRTC Sensor, this product simplifies the process for parents to remind themselves of medication schedules while making the medication-taking process more enjoyable and effective for children.
- With this kind of approach, it is hoped that medication adherence will improve, parental stress will decrease, and the accuracy of medication administration times will be better maintained.


## Prerequisites
### Components Lists
- Arduino Uno : Microcontroller for data processing and system control.
- RTC DS3231 : Keeps track of time and to set the medicine schedule.
- Servo Motor MG996R : To open and close the medicine box lid.
- Push Button : A manual input to open the box.
- DFPlayer Mini MP3 Player Module : To store MP3 file of an reminder audio.
- Mini Speaker 8 Ohm : To output the sound from the MP3 Player.
- Buzzer Piezo : Provide a simple audible alarm as notification.
- 9V Battery : Provide additional power for the servo.
- LED : Indicates that the system is on. When it is time to take medication, the LED will flash and a simple alarm will sound as a notification.

### Datasheet Arduino Uno
![Pinout-UNOrev3_latest](https://github.com/user-attachments/assets/0096fd56-95db-492e-95bb-b8bdb62bdd61)

### DatasheetRTC DS3231 
![DS3231-RTC-Pinout](https://github.com/user-attachments/assets/e774f48a-862f-4d61-a4a1-cf88817a01ff)

### Schematic Cirkit Designer 
(This one using a ESP32 Microcontroller instead of Arduino Uno, but it remains the same function)
<img width="566" alt="skematik" src="https://github.com/user-attachments/assets/4a11720d-8997-417c-86b4-6d9c834d829f" />

## Demo and Evaluation
- Setup: Connect all components as per the schematic and upload the code to Arduino Uno via USB cable.
- Demo: Demonstrate the system in action on how the RTC tracks time, how the servo opens the medicine container, how cheerful music or reminders play through the DFPlayer, and how children interact using the button.
- Evaluation: Test the system from two perpective, an adult and children. Provide usability feedback from both of the perspective.

[Demo Video] (https://drive.google.com/file/d/1kYSsPfOctSTLLGh2M94BbAzYQHsvbD6L/view)


## Conclusion
This project demonstrates a practical solution for improving children's medication adherence through automation and interaction. By using the combination of an RTC module, servo motor, DFPlayer, and Arduino Uno, the system ensures timely reminders and adds engaging audio features to motivate children. The approach reduces parental stress, encourages routine, and makes the medication process more enjoyable. With further refinement, this system has the potential to support better health habits in a fun and accessible way.
