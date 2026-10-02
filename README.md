Rain Rain Go Away - Smart Rain Detection & Wiper Control System

Project Overview:

This project aims to design an automated wiper control system that detects rain using a resistive rain sensor and adjusts the speed of a DC motor accordingly. The system works on four discrete speed levels based on rainfall intensity and uses analog signal processing combined with Arduino for control.

The core functionality includes a comparator network that converts the sensor’s analog signal into a 4-bit digital output. This output is passed through a DAC (Digital-to-Analog Converter) built using a summing amplifier to produce four different analog voltages. These voltages are compared with a triangle wave to generate PWM signals, which control the speed of the wiper motor.

To ensure proper wiper movement, limit switches are used to reverse the direction at 0° and 180°. A servo motor is also used to visually indicate the current wiper speed level, mapped directly to the binary output.

The system is built using components like Arduino UNO, op-amps, motor driver, rain sensor, LEDs, resistors, and capacitors. Simulations were carried out using LTSpice, and the full working prototype has been practically implemented.

Circuit Diagram:
![WhatsApp Image 2025-07-01 at 16 22 26_0677fb17](https://github.com/user-attachments/assets/8760eb40-9bab-4832-aa25-a495b1ad5378)

Results:
![WhatsApp Image 2025-07-01 at 16 22 26_f317a29a](https://github.com/user-attachments/assets/b769af58-85e8-4db2-bd39-48546ef5034f)

![WhatsApp Image 2025-07-01 at 16 22 26_b3e0b00a](https://github.com/user-attachments/assets/02b39c14-a0e3-44e4-9f69-da08d5ae8b96)


For a video demonstration of the working system, check out the Google Drive link here:(https://drive.google.com/drive/folders/1tUdHJNRUtfXS56_pBJ250gK1kQLBFwH8)
