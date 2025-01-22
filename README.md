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






