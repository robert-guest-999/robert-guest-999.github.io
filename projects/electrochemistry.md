---
title: "Electrochemistry"
description: "Building a low-cost impedance spectrometer from scratch"
---

<script>
window.MathJax = {
  tex: { inlineMath: [['$', '$'], ['\\(', '\\)']] },
  svg: { fontCache: 'global' }
};
</script>
<script id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js">
</script>

The general aim of this project is to build some different commonly used pieces of electrochemical characterisation equipment from scratch. The ultimate aim is to make an electrochemical impedance spectrometer and algorithmically implement the Distribution of Relaxation Times (DRT) analysis method from scratch.

# Background Theory
Electrochemical systems can be analysed in many different ways, but almost all of them boil down to applying either a voltage or current profile and observing the results. The most simple example is Linear Sweep Voltammetry, which involves applying a linearly increasing potential between the working and counter electrode, and observing the current passed. Cyclic Voltammetry is an extention of this method which adds a negatively sloped potential ramp once the maximum value is reached. This provides additional information about the reversibility of the system.

# EIS
Electrochemical Impedance Spectrometry (EIS) involves measuring the system impedance at a range of different signal frequencies. A sinusoidal potential is applied to the system, and the effect of the oscillation frequency is observed. A baseline DC potential is also applied.

## Impedance Theory
In the most simple case (a purely resistive circuit), the relationship between voltage and current is linear, time-invariant, and can be described using Ohm's law.

$$
R = \frac{V}{I}
$$

An extension of this concept is to consider the impact of a periodically oscillating voltage:

$$V = V_{0}sin(\omega t)$$

Ohm's law tells us that for a purely resistive circuit, the current will oscillate in phase with the voltage:

$$I = I_{0}sin(\omega t)$$
Hence,
$$
R = \frac{V}{I} = \frac{V_{0}sin(\omega t)}{I_{0}sin(\omega t)} = \frac{V_{0}}{I_{0}}
$$

Where $V_{0}, I_{0}$ are the maximum voltage and current amplitude respectively and $\omega = 2 \pi f$ is the angular frequency






# The Plan
In theory, all that's needed to perform EIS is a variable frequency AC voltage source and a way to record the current flow. In the interest of keeping things affordable, we can use a specially selected microcontroller for both of these tasks. Our shopping list is as follows: The board must contain a Digital to Analog COnverter (DAC) for creating the driving potential, and an Analog to Digital Converter (ADC) to measure the induced current flow (with the help of an opamp chip acting as a transimpedance amplifier). Given these two components, a programme can be written to perform a frequency scan while measuring the current. From this information, the system's impedance can be determined at each of the frequencies sampled. Given that the frequecy range spans from milliHertz all the way up to MegaHz, a logarithmic scale with a set number of points per decade is the sensible way of distributing the measurements.
