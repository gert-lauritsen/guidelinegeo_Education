# Transient Electromagnetic (TEM) – Engineering Documentation



This repository contains a set of technical presentations that describe **Transient Electromagnetic (TEM) systems from an engineering and electronics perspective**, with particular emphasis on transmitter design, receiver challenges, and embedded firmware implementation.



The material is written by and for engineers. It deliberately treats TEM not primarily as a geophysical method, but as a **high-dynamic-range, time-domain electromagnetic measurement system** whose success depends on disciplined electronics, timing, and system architecture.



---



## Contents Overview



### 1. *TEM from an Engineer’s View*  

📄 **File:** `TEM from an engineers view.pptx`



This presentation establishes a **mental model for TEM that is grounded in electrical engineering** rather than geophysics.



#### Core ideas:

- TEM is fundamentally a **stored-energy decay experiment**:

 - Charge a large inductance (TX loop)

 - Force a fast current turn-off

 - Observe how a coupled, distributed RL network (the ground) dissipates energy

- Soil resistivity, depth, and geology are **interpretations layered on top of the electronics**, not the starting point.



#### Key technical topics:

- System decomposition into:

 - Transmitter (high-current, fast turn-off power electronics)

 - Medium (earth as a distributed lossy conductor)

 - Receiver (high dynamic range, dB/dt or induced voltage measurement)

- Receiver front-end challenges:

 - Offset drift

 - Thermal coupling

 - Dielectric memory effects

 - Microphonics

- Cable and dielectric behavior:

 - Why PTFE performs well

 - Comparison with problematic dielectrics

- Integrator-based receiver architecture:

 - Timing, gain, and reset behavior

 - Charge injection and reset constraints

- Practical TX design issues:

 - Avalanche energy

 - Clamp networks

 - Damping resistors

 - Hi/low moment behavior

- DIY calculation examples:

 - Coil current

 - Stored energy

 - LC resonance

 - Critical damping



**Purpose:**  

To give engineers an intuition for *why TEM behaves the way it does* and which parts of the system actually dominate measurement quality.



---



### 2. *Transient Electromagnetic (TEM) Systems – An Electronics-Centered Perspective*  

📄 **File:** `Transient Electromagnetic (TEM) Systems.pptx` 


This presentation explains **why TEM instruments are exceptionally difficult to build**, focusing on electronics constraints rather than theory.



#### Core ideas:

- TEM systems must handle **6–7 decades of dynamic range**

- The transmitter is a **worst-case electrical load**

- Early-time accuracy is brutally sensitive to timing and waveform fidelity



#### Key technical topics:

- Dynamic range limitations of linear ADC chains

- Necessity of:

 - Gain staging

 - Log gating

 - Stacking

- Transmitter turn-off physics:

 - kV-level voltages

 - Energy redirection at turn-off

 - Clamp topology effects on waveform validity

- Early-time measurement sensitivity:

 - ~100 ns timing accuracy requirement

 - Direct coupling between turn-off distortion and false geology

- Receiver reality:

 - Measures dB/dt, not B(t)

 - DC offsets are irrelevant, saturation is fatal

- Stacking as **time-domain lock-in amplification**

- Power-line interference cancellation via timing, not filtering

- Why conductive coupling **cannot be fixed in post-processing**

- Airborne TEM:

 - Motion-induced EMF

 - Geometry uncertainty

 - Calibration as an electronics problem



**Purpose:**  

To explain *why TEM success or failure is decided in hardware and timing*, long before inversion or interpretation.



---



### 3. *TX08 Firmware*  

📄 **File:** `TX08 Firmware.pptx`



This presentation documents the **embedded firmware architecture of the TX08 transmitter**, implemented on an 8051-class microcontroller.



#### Core ideas:

- Even a slow MCU can deliver precision timing if the architecture is correct

- Hardware peripherals, not software loops, define determinism



#### Key technical topics:

- System responsibilities:

 - Pulse sequencing

 - Sampling coordination

 - Communication

 - Parameter storage

- Firmware module breakdown:

 - `TxProc.c` – pulse sequencing and state machine

 - `AnalogSample.c` – ADC setup and scaling

 - `Kommunikation.c` – UART protocol and command handling

 - `config.c` – parameter validation and defaults

 - `F000_FlashPrimitives.c` – flash persistence

 - `Global.c` – shared state

- PCA (Programmable Counter Array) as the **real-time executive**

 - TX edge detection

 - ADC scheduling

 - Sign/polarity sequencing

 - Self-test triggering

- Interrupt-driven measurement sequencing:

 - On-time current and voltage sampling

 - Off-time scheduling

 - Deterministic association of samples with TX state

- Communication interface:

 - Start/stop TX

 - Parameter control

 - Data readout

 - Flash access

- Development environment:

 - Keil PK-51

 - Silicon Labs 8051 toolchain



**Purpose:**  

To document how **deterministic timing, sampling, and state control** are achieved in the transmitter firmware.



