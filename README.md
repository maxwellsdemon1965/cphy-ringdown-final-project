# Performing quasinormal fits to ringdown portion of gravitational waveforms

Final project for Computational Physics (PHY 381C Fall 2022)
Author: Hector Iglesias

##  Introduction


gravitational waves: inspiral, merger, ringdown


In the ringdown regime, the resulting black hole is a single perturbed black hole characterized by two parameters: the final remnant mass $M$ and dimensionless spin $j$. This perturbed black hole radiates gravitational waves at a specific set of frequencies and timescales described by black hole perturbation theory. The set of frequencies and decay times are known as quasinormal modes (QNMs). These modes are modeled as exponentially damped sinusoids [1].

write model of modes (slide 5)
include real and imaginary frequencies (slide 5)

$$
\Psi_{4_{(\ell',m')}} = \sum_{\ell m} \sum_{n=0} C_{\ell m n} e^{-t/\tau_{\ell m n}} e^{i (\omega_{\ell m n} t + \phi_{\ell m n})}
$$

$\omega_{\ell m n} = Re(\omega)$, $\tau_{\ell m n} = Im (\omega)^{-1}$



Quasinormal mode fits (berti paper) (slide 6, 7)

$$
F_{\ell m n} = M \omega_{\ell m n} = f_1 + f_2 (1-j)^{f_3}
$$

$$
Q_{\ell m n} = \pi f_{\ell m n} \tau_{\ell m n} = q_1 + q_2 (1-j)^{q_3}
$$

$$
\Psi_{4_{(2,2)}} = A_{220} e^{i \theta_{220}} \approx C_{220} e^{-t/\tau_{220}} e^{i (\omega_{220} t + \phi_{220})}
$$

$$
\text{ln} A_{220} = \text{ln} C_{220} - \frac{1}{\tau_{220}} t
$$

$$
\theta_{220} = \omega_{220} t + \phi_{220}
$$

[2]


## Setup
At this point in time, 


## Notebook
This notebook searches for the best starting time of the quasinormal mode of interest by performing linear fits on the log amplitude and phase of the gravitational waveform. After obtaining the best starting time—corresponding to the highest $R^2$ score—a linear fit is performed one last time to obtain the quasinormal mode frequency and decay time. Using this information, the estimated final mass and dimensionless spin of the remnant black hole is calculated and compared to the values obtained from the black hole's apparent horizon at the end of the simulation.

To start with, the notebook needs to work with gravitational wave data from a BBH simulation. The Center of Gravitational Physics at UT Austin has simulated gravitational wave data from a variety of simulations in the form of .h5 files. These .h5 files can be downloaded from the Waveforms page on the main website: https://sites.cns.utexas.edu/cgp/waveform. After specifying the simulation to be analyzed as well as the mode of interest, the notebook will produce plots of the entire waveform and the merger+ringdown portion of the waveform.

![](resources/D11_q1_a1_0_0_0_a2_0_0_-0.6_m240-plot.png)
![](resources/D11_q1_a1_0_0_0_a2_0_0_-0.6_m240-merger+ringdown-plot.png)

Quasinormal modes are not expected to all start at the same time, and they are not expected to turn on at the time of merger, so an optimal start time needs to be chosen. This optimal start time of the QNM is determined by performing linear fits of the log amplitude and the phase [....], and 

While ringdown is assumed to start after merger, there is no reason that QNMs are excluded from appearing before merger, so the range of start times has been written with this in mind. In the notebook, the start times range from [-25, 25], where the values are the start times are the time after merger (the time array has its values shifted so that $t_{\text{merger}}$ is at 0), but this range can be changed. 

For each start time, the data is truncated to a width of 50 $M$, where $M$ is the total mass and serves as the units for time in the simulation. The truncated data is split into training data (50%), validation data (25%), and test data (25%). A linear regression model is trained on the training data, and using this model, a prediction is made using time values from the validation dataset. From this prediction, an $R^2$ score is computed on the validation dataset. This $R^2$ is then appended to a dictionary with the start time as its key. At the end of the loop, the start time corresponding to the largest $R^2$ score is picked out, and this is the optimal start time for the QNM.


One last time:
After obtaining the 


![](resources/comparison_test_predicted_log_amp.png)
![](resources/comparison_test_predicted_phase.png)


Using Emanuele Berti's fitting functions [2], the estimated final mass and dimensionless spin of the simulation's remnant black hole is calculated. Since the .h5 file also contains information about the apparent horizons of the initial pair of black holes and the remnant black hole, the mayawaves library can be used to calculate the mass and dimensionless spin of the remnant black hole using its apparent horizon. The values obtained from the apparent horizon and the fitting functions are compared to each other.

Lastly, the ringdown portion of the waveform is reconstructed using the amplitude, phase shift, frequency, and decay time obtained from the final linear regression. The fractional root-mean-square error of the reconstructed fit when compared to the original waveform is also calculated.

![](resources/reconstructed_qnm_fit.png)

## Reference Documentation

* [1] Giesler, M., Isi, M., Scheel, M. A., and Teukolsky, S. A., “Black Hole Ringdown: The Importance of Overtones”, <i>Physical Review X</i>, vol. 9, no. 4, 2019. doi:10.1103/PhysRevX.9.041060.
* [2] Berti, E., Cardoso, V., and Will, C. M., “Gravitational-wave spectroscopy of massive black holes with the space interferometer LISA”, <i>Physical Review D</i>, vol. 73, no. 6, 2006. doi:10.1103/PhysRevD.73.064030.
