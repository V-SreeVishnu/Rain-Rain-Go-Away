# Rain Rain Go Away: Smart Rain Detection & Wiper Control System

An automatic wiper controller that detects rain with a resistive sensor and sets the wiper speed in four discrete levels based on rainfall intensity. The signal path is almost entirely analog (comparators, op-amps, PWM), with an Arduino UNO driving a servo needle that shows the current speed level. The design was simulated in LTspice and built as a working prototype.

**Demo:** [Prototype videos](https://drive.google.com/drive/folders/1tUdHJNRUtfXS56_pBJ250gK1kQLBFwH8)

## Circuit diagram

![Circuit diagram](https://github.com/user-attachments/assets/8760eb40-9bab-4832-aa25-a495b1ad5378)

## How it works

```
Rain sensor → Comparator network → Summing-amplifier DAC → Comparator (PWM) → Motor driver → Wiper motor
                    │                                             ▲                 ▲
                    ├→ LED dashboard + Arduino servo needle       │                 │
                                                    Triangle-wave generator   Limit switches + D flip-flop
```

1. **Comparator network:** the sensor's analog output (0 to 3.7 V) goes to the inverting inputs of four LT1017 comparators. Each comparator gets a reference from a 1 kΩ resistor-ladder divider spanning 3.7 V to ground. As the sensor output falls (more water), more comparators switch high, giving a 4-bit code (A, B, C, D) that also lights the LED dashboard.
2. **DAC:** the 4-bit code feeds a non-inverting summing amplifier (4 × 620 Ω inputs, Ri = 10 kΩ, Rf = 1 kΩ, gain 1.1) that outputs one of four DC levels.
3. **PWM generation:** an op-amp square-wave oscillator (about 100 Hz) feeds an op-amp integrator to make a triangle wave. A comparator compares it with the DAC level, so the PWM duty cycle rises as the DAC voltage rises. The PWM goes to the motor driver's enable pin.
4. **Wiper sweep:** two limit switches and a D flip-flop toggle the motor driver's `IN1` and `IN2` inputs, reversing the motor at 0° and 180°.
5. **Speed indicator:** an Arduino UNO reads the 4-bit code and moves a servo needle to match the speed level.

| Comparator code | LEDs lit | Speed level | DAC output (approx.) |
|---|---|---|---|
| 0000 | 0 | Off (no water) | ~2 V |
| 1000 | 1 | Level 1 | ~3.5 V |
| 1100 | 2 | Level 2 | ~4.5 V |
| 1110 | 3 | Level 3 | ~5.5 V |
| 1111 | 4 | Level 4 | ~6.5 V |

## Components

Resistive rain sensor, op-amps and comparators (LT1017), resistors, capacitors, motor driver, DC motor, limit switches, Arduino UNO, servo motor, LEDs, power supply, breadboard and jumper wires.

## Results

![Result 1](https://github.com/user-attachments/assets/b769af58-85e8-4db2-bd39-48546ef5034f)

![Result 2](https://github.com/user-attachments/assets/02b39c14-a0e3-44e4-9f69-da08d5ae8b96)

The LTspice simulation of the triangle-wave generator produced the expected triangle wave at the comparator input, and the full prototype ran the wiper at four speeds. See the demo videos above.
