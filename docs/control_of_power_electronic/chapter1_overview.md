# 1-Overview of Advanced Control of Power Electronic Systems 

## 1.1 Linear controller implementation and analysis

In conclusion, many advanced control methods can be applied in power electronic systems with different objectives, which can be generally divided into two categories: linear controller and nonlinear controller. The overview of these advanced control methods can be seen in Fig. 1.1

![fig1.1](fig/chapter1/1_1_control_methods.svg)

*Fig. 1.1 Overview of advanced control methods in power electronic systems.*

###  1.1.1 Implement PI controller

The PI regulator is a linear controller. 
The transfer function of conventional PI controller in the continuous domain can be expressed as:

$$
G_{pi}(s) = k_p + \frac{k_i}{s} \tag{1.1}
$$

where kp and ki are the proportional and integral gains, respectively.

### 1.1.2 Implement PR controller

The transfer function of PR controller can be obtained by shifting the integrator part of the conventional PI controller to both positive and negative fundamental frequency:

$$
G_{PR_ideal}(s) = k_p + \frac{K_i}{s-j\omega} + \frac{k_i}{s+j\omega} = k_p + \frac{2k_is}{s^2 + \omega^2} \tag{1.2}
$$

However, it should be pointed out that the PR controller expression in Eq. (1.2) is an ideal one, which is quite sensitive to the grid frequency variation. Thus, the practical PR controller is adopted by the following equation:

$$
G_{PR}(s) = k_p + \frac{k_r \omega_c s}{s^2 + \omega_c s + \omega_0^2} \tag{1.3}
$$

### 1.1.3 Implement repetitive controller

The conventional repetitive controller (CRC) in the continuous domain can be expressed as follows:

$$
G_{CRC}(s) = k_{RC}\frac{e^{-sT_0}}{1-e^{-sT_0}} \tag{1.4}
$$

where $k_{RC}$ is the gain parameter of CRC regulator, $T_0$ is the period of thefundamental control frequency.

Moreover, based on the nature of exponential function, the conventionalRC given in Eq. (1.4) can also be written as:

$$
G_{CRC}(s) = -\frac{k_{RC}}{2} + \frac{k_{RC}}{T_0s} + \frac{2k_{RC}}{T_0}\sum_{n=1}^{\infty}\frac{s}{s^2 + (n\omega_0)^2} \tag{1.5} 
$$

From the above expression, it can be concluded that an RC is equivalent to a parallel combination of :
(1) a negative proportional term, 
(2) an integral element,
(3) and an infinite number of resonant controllers
connected in parallel at specific harmonic frequencies. 

This implies that an RC contains lots of resonant frequencies, while a PR controller contains only one.

An ideal RC has an infinite open-loop gain at the resonant frequencies and can make the control system to track the reference signals **without steady-state error**. However, it also results in **poor stability inevitably** and has **poor robustness** against the deviation of resonant frequencies. 

To improve the stability and robustness, a low-pass filter $Q(s)$ or a constant $Q$ less than 1 is added to the internal model. When $Q$ is a constant less than 1, the expression of the RC with a certain bandwidth becomes:

$$
G_{BRC}(s) = \frac{K_{RC}Qe^{-T_0s}}{1 - Qe^{-T_0s}} \tag{1.6}
$$

Based on the nature of exponential function, Eq. (1.6) can be rewritten as follows:

$$
\begin{split}
G_{BRC}(s) = -\frac{k_{RC}}{2} + \frac{k_{RC}}{T_0s + T_0\omega_c} + \frac{2k_{RC}}{T_0}\sum_{n=1}^\infty\frac{s + \omega_c}{s^2 + 2\omega_c s + \omega_c^2+(n\omega_0)^2} \\ 
\approx -\frac{k_{RC}}{2} + \frac{k_{RC}}{T_0s + T_0\omega_c} + \frac{2k_{RC}}{T_0}\sum_{n=1}^\infty \frac{s + \omega_c}{s^2 +2\omega_c s + (n\omega_0)^2} 
\end{split}
\tag{1.7}
$$

When $\omega_c$ is far smaller than $\omega_0$, the symbol of approximate equal holds. $\omega_c$ is the resonant bandwidth and $\omega_c = -\ln Q/T_0$.

From Eq. (1.7), it can be seen that the integral element in Eq. (1.5) becomes an inertial element, and the resonant controllers become quasi-resonant controllers.

### 1.1.4 Pole placement control

Based on the system data considered and the operating condition, the state equation of the system under study is given by:

$$
\dot{X} = AX + BU
$$

Where $U$ is input signal, we set the the feedback that the output is set as input: $U = -KX$, The use of state feedback control modifies the system state equation to $\dot{X} = (A - BK)X$, which is the state variable presentation of the compensated system. The characteristic equation of the compensated system is: $|sI -A + BK| = 0$, Here, the state feedback gain matrix K can be determined using the Ackermann’s formula, which is:

$$
K =
\begin{bmatrix}
0 & 0 & 0 & ... & 1
\end{bmatrix}
\begin{bmatrix}
B & AB & ... & A^{n-1}B
\end{bmatrix}
\phi(A)
\tag{1.8}
$$

where $\phi(A) = A^n + \alpha_1 A^{n-1} + ... + \alpha_{n-1} A + \alpha_n I$, $\alpha_i$ are the coefficients of the desired characteristic polynomial.

However, the pole placement control is based on an accurate model of the system. The control performance will be deteriorated if the system parameters are deviated. Furthermore, the pole placement control is only applicable for a linear plant, which might be a limitation for this method, since most power electronic plants are nonlinear.

### 1.1.5 Linear quadratic regulator

