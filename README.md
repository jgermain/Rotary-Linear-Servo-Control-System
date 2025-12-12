# Rotary–Linear Servo Control System  
### MATLAB/Simulink Control System Design | Precision Timing Experiment

## Project Description
A MATLAB/Simulink control system that synchronizes a motor-driven linear cart with a rotating four-slit wheel. The system models servo motor dynamics, derives the rotary-to-linear kinematic mapping, and uses a PID + feedforward controller to achieve sub-percent timing accuracy.

---

## Project Summary
This project designs and simulates a servo-driven linear actuator system that must pass a mounted pin through a slit in a rapidly rotating, four-slit wheel. The system combines motor modeling, kinematic conversions, and PID control to achieve **0.16% timing error** between cart arrival and wheel slit alignment.

The cart is driven by a DC servo motor, and the wheel is powered independently at constant angular velocity. The goal is to have the cart reach **0.50 m** at the exact moment a wheel slit aligns.

---

## Objectives
- Model DC servo motor electromechanical dynamics  
- Convert wheel angular velocity to linear cart displacement  
- Derive the rotary-to-linear kinematic ratio (10.61)  
- Build a Simulink model integrating motor, belt, and cart  
- Design and tune PID/PD controllers  
- Validate timing accuracy via simulation  
- Compare controlled vs uncontrolled behavior  

---
## System Modeling

### **Motor Modeling**
The servo motor is modeled using standard electromechanical equations:

- Armature circuit equation  
- Back-EMF model  
- Motor torque constant  
- Rotor inertia and viscous friction  
- Load reflected through the belt drive  

This yields a second-order transfer function mapping applied voltage → angular speed → linear cart motion.

---

### **Kinematic Relationship**
Wheel angle \( \theta \) maps to cart displacement \( x \) using the derived geometric ratio:

\[
x = 10.61\theta
\]

This relationship determines the timing required for the cart to reach the slit radius at **0.50 m**.

---

## Control Design

### **PID / PD Controller**
A PID controller governs cart position with:

- Proportional control for tracking  
- Integral action for zero steady-state error  
- Derivative action for velocity damping  
- Feedforward term for improved timing  

### **With PID Control**
- Smooth, non-overshooting trajectory  
- Zero steady-state error  
- Accurate alignment with slit timing  

### **Without PID**
- Large overshoot  
- No settling  
- Cart crashes into end-stop  
- Impossible to meet timing requirements  

---

## Key Simulation Results

### **Wheel Angular Velocity**
- Reaches steady state at ~0.2 s  
- Conversion to degrees shown for interpretability  

### **Cart Position (Controlled)**
- Reaches **0.50 m** at **t = 2.52 s**  
- Overshoot ≈ 0  
- Settling time ≈ **1.68 s**  

### **Timing Alignment**
- Wheel slit passes 90° at **t = 2.53 s**  
- Cart reaches target at **t = 2.52 s**  
- Timing error = **0.16%** (≈ 10 ms)  

### **Uncontrolled Behavior**
- Heavy overshoot  
- No convergence  
- Unsafe operation

---

## Error Analysis
Primary sources of timing error:

- Belt elasticity and backlash  
- Linear guide friction  
- Motor driver nonlinearities  
- Sensor quantization  
- Mechanical misalignment  

These effects would cause variation in real-world implementation compared to simulation.

---

## Possible Improvements
- Add wheel-speed encoder feedback  
- Implement trajectory shaping (S-curve)  
- Stiffer belts / improved linear guide  
- Higher-resolution encoder on cart  
- Explore LQR or state feedback control  

---

## References
[1] Teknic Inc, “ClearPath: Teknic's Integrated Brushless Servo Motor, Drive and Encoder, YouTube, May 10, 2018. [Online]. Available: https://www.youtube.com/watch?v=_SYhCRwacDs

[2] ABB (Baldor-Reliance), HDS High-Performance AC PM Servo Motor Data Sheet, version 02/21, 44-page PDF. [Online]. Available: https://www.baldor.com/mvc/DownloadCenter/Files/9AKK107304

[3] Wolfram Research, Inc., “Moment of Inertia of a Cylinder,” Wolfram Formula Repository. [Online]. Available: https://resources.wolframcloud.com/FormulaRepository/resources/Moment-of-Inertia-of-a-Cylinder 

[4] SDP/SI, “Timing Belt Pulleys,” SDP/SI Products. [Online]. Available: https://sdp-si.com/products/Timing-Belt-Pulleys/index.php

[5] OpenBuilds, “V-Slot NEMA 17 Linear Actuator Bundle (Belt-Driven),” OpenBuilds. [Online]. Available: https://us.openbuilds.com/v-slot-nema-17-linear-actuator-bundle-belt-driven/

[6] CJ’s Machine & Fab, “Custom Brackets and Mounts,” CJ’s Machine & Fab. [Online]. Available: https://www.cjsmachineandfab.com/custom-brackets

---

## Images
All simulation plots (cart position, wheel angle, zoomed views, and alignment graphs) are stored in the `/images` folder.

---
