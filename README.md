# Practical Output Regulation of Robotic Manipulators: a Comparison Study

## Abstract

The nonlinear dynamics and uncertainties of robotic manipulators necessitate advanced control strategies to ensure precise output regulation under challenging conditions. This paper compares three control methodologies: Computed Torque Control (CTC), Sliding Mode Control (SMC), and an Internal Model-Based Approach (IMB) with Differential-Algebraic Representation. Experimental validation on the KUKA LWR IV+ robotic manipulator highlights differences in their performance across scenarios involving varying payloads and modeling inaccuracies. The analysis emphasizes the trade-offs among control effort, error convergence, and robustness, offering insights into the suitability of each approach depending on the application's requirements.

## Dynamical system

The KUKA LWR IV+ robot is a seven DOF manipulator, whose link dynamics is governed by

$$
\begin{cases}    
M\left(x_{\theta},w_c\right) \dot{x}\_{\omega}+v\left(x_{\theta}, x_{\omega},w_c\right)+g_{v}\left(x_{\theta},w_c\right) & =& u \\ 
\dot{x}\_{\theta} & =& x_{\omega}
\end{cases}
$$


The equivalent 2R planar robot, moving on a vertical plabe, is characterized by the following matrices

$$ 
M\left(x_{\theta},w_c\right)  =
\begin{bmatrix}
a_{2}+a_{3} & a_{2} \\
a_{2} & a_{2}
\end{bmatrix} +\cos \left(x_{\theta 2}\right)
\begin{bmatrix}
2 a_{1} & a_{1} \\
a_{1} & 0
\end{bmatrix}$$

$$v\left(x_{\theta}, x_{\omega}, w_c\right) =a_{1} \sin \left(x_{\theta 2}\right)
\begin{bmatrix}
-x_{\omega 2}^{2}-2 x_{\omega 1} x_{\omega 2} \\
x_{\omega 1}^{2}
\end{bmatrix}$$

$$g_{v}\left(x_{\theta}, w_c\right) =\cos \left(x_{\theta 1}+x_{\theta 2}\right)
\begin{bmatrix}
m_{2} g \ell_{2} \\
m_{2} g \ell_{2}
\end{bmatrix}
+\cos \left(x_{\theta 1}\right)
\begin{bmatrix}
\left(m_{1}+m_{2}\right) \ell_{1} \mathrm{~g} \\
0
\end{bmatrix}$$

## Exogenous system

The periodic trajectory is given by the following exogenous system

$$
\begin{cases}
\omega_{\theta 1} & = 0.4 \cos (t)  \\ 
\omega_{\theta 2} & =-0.4 \cos (t)
\end{cases}
$$

## Experimental scenarios

The efficacy and the robustness of the method have been validated in three distinct scenarios:

- $i)$ *Nominal case*: No extra mass is attached to the tip of the end-effector,    
- $ii)$ *Extra payload*: An extra mass of $2 \mathrm{~kg}$ is attached to the tip of the end-effector,
- $iii)$ *Incorrect model*: The controller is designed based on one fourth of the actual mass for each links of the $2 \mathrm{R}$ equivalent robot,


## Physical paramters

| Parameter        | Joint(1)       | Joint(2)       |
|------------------|----------------|----------------|
| $\ell$           | $0.5 \mathrm{~m}$ | $0.5 \mathrm{~m}$ |
| $\mathrm{m}$     | $2.6 \mathrm{~kg}$ | $2.6 \mathrm{~kg}$ |
| $\tilde{m}$      | $0.65 \mathrm{~kg}$ | $0.65 \mathrm{~kg}$ |
| $x_{\theta}(0)   | $0.4 \mathrm{~rad}$ | $-0.4 \mathrm{~rad}$ |
| $\tilde{x}_{\theta}(0)   | $0.4 \mathrm{~rad}$ | $-0.6 \mathrm{~rad}$ |

## Experimental data

The project includes experimental data stored in the folder *LAB_DATA*. This folder is organized into three subfolders, each corresponding to a specific control technique:
- **CTC**: Data related to Computed Torque Control.
- **SMC**: Data related to Sliding Mode Control.
- **IMB**: Data related to Internal Model Based Control.

Each subfolder contains *.txt* files with data for position, tracking error and control signals. The filenames follow this pattern:

    (un)matched_setupi_signal_controller.txt

Explaination of the Pattern
- `(un)matched`: Indicates whether the scenario is matched or unmatched.
- `setupi`: Describes the experimental scenario, with $i={1,2,3}$.
- `signal`: Specifies the data type:
    - `error`: tracking error signal.
    - `position`: joint position signal.
    - `control`: control signal.
- `controller`: The control technique used, i.e., CTC, SMC and IMB.


## Output regulation

The project includes the MATLAB code for computing both the polynomial approximation and the IMB gains, defined respectively in equations (A.5) and (A.8) in the manuscript.


Internal model matrices

$$\Phi =
\begin{bmatrix}
    0 & I & 0 & 0 & 0 \\
    0 & 0 & I & 0 & 0 \\
    0 & 0 & 0 & I & 0 \\
    0 & 0 & 0 & 0 & I \\
    0 & -4f^5I & 0 & -5f^3I & 0
\end{bmatrix}
\quad
\Gamma =
\begin{bmatrix}
    0 \\ 0 \\ 0 \\ 0 \\ I
\end{bmatrix}$$

The polynomial approximation

$$\rho = 
\begin{bmatrix}
26.3200 & 3.7930 & 2.2120 & 2.5940 & -13.1400 & -8.0090 & -0.4480 & -0.0290 & -0.8191 & -3.4000 & 1.7500 & 2.8240 \\
12.7600 & 0.0000 & -2.7040 & -8.8020 & -13.4700 & -7.3400 & 0.0000 & 0.0000 & 0.0000 & 0.3085 & 1.8080 & 2.9150 \\
30.6900 & 3.5940 & 2.2450 & 45.8600 & 13.1200 & 7.4070 & 0.5146 & 0.0162 & 0.5729 & 5.2840 & 1.7820 & 2.7200 \\
16.9400 & 0.0000 & -2.7040 & -8.8020 & -13.4700 & -7.9120 & 0.0000 & 0.0000 & 0.0000 & 0.3085 & 1.8080 & 2.9150
\end{bmatrix}
$$

Gain synthesized by the **IMB** technique (A.8)

$$\mathbf{K}=
\begin{bmatrix}
    -501.1559 & -51.6762 & -61.0883 & -13.9976 & -969.4690 & -58.9046 & -1045.9322 & 1.2262 & -3376.5894 & -224.8351 & -674.4890 & -3.7868 & -1028.4645 & 75.5330 \\
    60.5655 & -192.7508 & -12.5232 & -26.7909 & 194.7745 & -364.1018 & 374.1509 & -376.6959 & 624.2392 & -1274.0779 & 228.6800 & -244.2496 & 171.1357 & -390.1254
\end{bmatrix}
$$




