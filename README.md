# FPGA-Based-Hardware-Game-Design-Snake-Verilog-HDL-
A snake game on DE10-Lite, integrating keypad scanning and display drivers
# FPGA Snake Game (Verilog HDL)

## Authors

* 范啟彥 (Fan, Qi-Yan)

## Project Overview

This project is a hardware-level implementation of the classic **Snake Game** developed for the **Terasic DE10-Lite (MAX10 FPGA)** platform. The system is built entirely using **Verilog HDL**, demonstrating hardware-software co-design principles, digital logic optimization, and real-time peripheral interfacing.

The goal of this project is to demonstrate how a responsive game system can be implemented using low-level digital logic, focusing on **resource optimization** and **efficient memory management** without the use of a microprocessor or high-level software.

This project is intended for:

* Developers interested in Verilog HDL and FPGA development.
* Students studying digital logic design, FSMs, and hardware resource optimization.

---

## Gameplay Features

### Dynamic Difficulty

* **Speed Leveling**: The game clock frequency automatically increases as the player's score rises, providing a smooth difficulty curve.
* **Real-time Feedback**: Current speed level is displayed via the onboard LEDs.

### Win/Loss Conditions

* **Game Over**: Triggered if the snake collides with the screen boundaries or its own body.
* **Score Tracking**: Points are awarded for each food item consumed, displayed on the seven-segment displays.

### Core Mechanics

* **Pointer-based Movement**: Uses a circular buffer to update coordinates efficiently.
* **Pseudo-random Spawning**: Food locations are generated using a hardware LFSR.
* **FSM-controlled Logic**: Dedicated states for Idle, Play, Pause, and Death.

---

## Controls

### Matrix Keypad (4x4)

| Action | Key Direction |
| --- | --- |
| Move Up | 2 |
| Move Down | 8 |
| Move Left | 4 |
| Move Right | 6 |

### Onboard Switches (SW)

| Function | Switch |
| --- | --- |
| Reset Game | SW[0] |
| Pause Game | SW[1] |

---

## System Architecture

### Hardware Logic Design

* **Clock Divider**: Generates three sub-clocks from the 50MHz source: a scan clock for displays, a game logic clock, and a 1Hz clock for the timer.
* **Keypad Scanner**: Implements matrix scanning to translate physical key presses into directional signals.
* **LFSR (Linear Feedback Shift Register)**: A 16-bit pseudo-random number generator used for randomized food spawning.

### Display Drivers

* **16x8 Dot Matrix**: Utilizes high-frequency row scanning and persistence of vision to render the snake and food.
* **Seven-Segment Controller**: Converts score and time data into BCD (Binary Coded Decimal) for real-time display.

---

## Core Engine Design

### Efficient Snake Management

* **Circular Buffer**: Instead of shifting an entire array, the engine updates only the `head_ptr` and `tail_ptr`.
* **Complexity**: Reduces update complexity from $O(N)$ to $O(1)$, significantly lowering FPGA logic gate utilization.

### Collision Detection

* **Boundary Check**: Monitors X/Y coordinates against map limits.
* **Self-collision**: Checks if the new head position is already marked as "occupied" in the game map grid.

---

## Code Structure

```
Snake_Game/
│
├── Snake_Game_Top.v      // Top-level module & signal routing
├── Clock_Divider.v       // Clock generation & Dynamic Frequency Scaling
├── Keypad_Scanner.v      // Matrix keypad scanning logic
├── Game_Engine.v         // FSM, Snake logic, LFSR, and collision
├── Dot_Matrix_Driver.v   // Visual rendering for 16x8 matrix
└── Seven_Seg_Controller.v // BCD conversion for Score and Time

```

---

## Summary

This project demonstrates a **complete hardware system** built with **Verilog HDL**, including:

* Optimized memory management through pointers.
* Real-time hardware peripheral interfacing.
* Pseudo-random number generation in logic.
* Dynamic Difficulty Scaling (DDS) through clock manipulation.

It serves as a comprehensive reference for low-level digital system integration on MAX10 FPGAs.

Would you like me to generate a **Pin Mapping table** specifically for the DE10-Lite to help with your project documentation?
