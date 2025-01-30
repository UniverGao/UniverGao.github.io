# Chapture 1. Introduction to control systems

## 1.1 introduction

![fig1.1 Open-loop control system (without feedback).](fig/chapter1/fig_1_1_openloop.svg)

*fig 1.1 Open-loop control system*

An open-loop control system uses a controller and an actuator to obtain the desired response, a component, or process, to be controlled can be represented graphically, as shown in fig 1.1

**An open-loop control system utilizes an actuating device to control the process directly without using feedback.**

![fig1.2 Closed-loop control system (with feedback).](fig/chapter1/fig_1_2_closeloop.svg)

*fig 1.2 Closed-loop control system*

A feedback control system often uses a function of a prescribed relationship between the output and reference input to control the process. 

In general, the difference between the desired output and the actual output is equal to the error, which is then adjusted by the controller.

Figure 1.3 is a negative feedback control system, because the output is subtracted from the input and the difference is used as the input signal to the controller. 

**A closed-loop control system uses a measurement of the output and feedback of this signal to compare it with the desired output (reference or command).**

![fig1.3 Multi-loop control system.](fig/chapter1/fig_1_3_doubleloop.svg)

*fig 1.2 Multiloop feedback system with an inner loop and an outer loop*

## 1.2 Control System Design

The performance specifications will describe how the closed-loop system should perform and will include 
(1) good regulation against disturbances
(2) desirable responses to commands
(3) realistic actuator signals
(4) low sensitivities
(5) robustness.

