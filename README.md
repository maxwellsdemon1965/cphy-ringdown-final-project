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

basically just explain how the notebook works, use slide 10 and the plots




After obtaining the 

Lastly, the ringdown portion of the waveform is reconstructed using the amplitude, phase shift, frequency, and decay time obtained from the final linear regression. , and the fractional root-mean-square error of the reconstructed fit when compared to the original waveform is calculated.

![](resources/.png)

## Reference Documentation

* [1] Giesler, M., Isi, M., Scheel, M. A., and Teukolsky, S. A., “Black Hole Ringdown: The Importance of Overtones”, <i>Physical Review X</i>, vol. 9, no. 4, 2019. doi:10.1103/PhysRevX.9.041060.
* [2] Berti, E., Cardoso, V., and Will, C. M., “Gravitational-wave spectroscopy of massive black holes with the space interferometer LISA”, <i>Physical Review D</i>, vol. 73, no. 6, 2006. doi:10.1103/PhysRevD.73.064030.
