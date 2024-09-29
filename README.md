# dottalk-arduino
DotTalk Arduino Firmware

# Bluetooth Braille Input/Output System

## Overview
This project implements a Bluetooth-based Braille input/output system. The user can input Braille characters using buttons, and the system can also receive characters via Bluetooth and display them in Braille. The system provides tactile feedback through vibration for both input and output operations.

![image](https://user-images.githubusercontent.com/18140805/188360827-5f070fad-446a-4b5d-a96e-76d59f2ebead.png)

## Key Features

### 1. Bluetooth Communication
- **SoftwareSerial** is used to enable Bluetooth communication on pins 10 (Rx) and 11 (Tx).
- Data is sent and received via Bluetooth at a baud rate of 9600, allowing seamless communication between the Braille device and external devices like smartphones.

### 2. Braille Input
- The user inputs Braille characters using **3 buttons** (connected to pins 2, 3, and 4) representing the 6 dots in a Braille cell.
- The state of the buttons is read and stored in the `braille` array, which holds the Braille pattern for the current character.
- The system compares the input pattern with a predefined **alphabet array** to convert the Braille input into a corresponding letter.
- Once the character is recognized, it is transmitted via Bluetooth, and the user receives **vibration feedback** for confirmation.

### 3. Braille Output
- When the system receives a character over Bluetooth, it switches to **output mode**.
- The received character is converted into a Braille pattern using the `braille_output` array and then displayed via **Braille actuators**.
- The actuators control the state of the Braille dots (up or down) using digital pins, representing the received character in tactile form.
- The system uses vibration to inform the user that a character has been displayed.

### 4. Vibration Feedback
- The **vibration motor** is used to provide feedback during both input and output operations.
- The function `setVibrationDuration()` controls the vibration motor, adjusting its duration based on whether the user is inputting or receiving Braille characters.
- For example, short vibrations confirm valid character inputs, while longer vibrations may indicate special conditions like the end of a transmission.

### 5. Input/Output Mode Switching
- The system operates in two modes: **input mode** and **output mode**.
  - **Input Mode**: The user can press buttons to input Braille, which is then converted into a character and sent via Bluetooth.
  - **Output Mode**: When the system receives a character from Bluetooth, it converts the character into a Braille pattern and displays it through the actuators.
- When a new character is received, the system switches automatically from input to output mode, and after displaying the character, it returns to input mode.

## Code Structure

### Setup
- In the `setup()` function, pins are initialized for **input (buttons)** and **output (actuators, vibration motor)**.
- Bluetooth communication is started using `BtSerial.begin(baudrate)`.

### Loop
- The `loop()` function monitors button presses for Braille input and checks for incoming data from Bluetooth.
- Depending on the button or Bluetooth input, the system either processes the input Braille character or outputs the received character as Braille.

### Auxiliary Functions
- **Vibration Control**: `setVibrationDuration()` manages vibration feedback to the user.
- **Character Validation**: `isValidChar()` checks if the input or received character is a valid alphabet letter.
- **Display Function**: `display()` converts a received character into a Braille pattern and controls the actuators to display it.

## Summary
This system allows users to input and output Braille characters using a combination of buttons and Bluetooth communication. The system supports real-time Braille input/output with tactile feedback, making it useful for communication with external devices like smartphones.

## Contact Info
- Doyoung Kim  (felixkim0719@gmail.com)
