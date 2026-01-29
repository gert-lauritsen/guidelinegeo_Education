\# Transient Electromagnetic (TEM) – Engineering Documentation



This repository contains a set of technical presentations that describe \*\*Transient Electromagnetic (TEM) systems from an engineering and electronics perspective\*\*, with particular emphasis on transmitter design, receiver challenges, and embedded firmware implementation.



The material is written by and for engineers. It deliberately treats TEM not primarily as a geophysical method, but as a \*\*high-dynamic-range, time-domain electromagnetic measurement system\*\* whose success depends on disciplined electronics, timing, and system architecture.



---



\## Contents Overview



\### 1. \*TEM from an Engineer’s View\*  

📄 \*\*File:\*\* `TEM from an engineers view.pptx` :contentReference\[oaicite:0]{index=0}



This presentation establishes a \*\*mental model for TEM that is grounded in electrical engineering\*\* rather than geophysics.



\#### Core ideas:

\- TEM is fundamentally a \*\*stored-energy decay experiment\*\*:

&nbsp; - Charge a large inductance (TX loop)

&nbsp; - Force a fast current turn-off

&nbsp; - Observe how a coupled, distributed RL network (the ground) dissipates energy

\- Soil resistivity, depth, and geology are \*\*interpretations layered on top of the electronics\*\*, not the starting point.



\#### Key technical topics:

\- System decomposition into:

&nbsp; - Transmitter (high-current, fast turn-off power electronics)

&nbsp; - Medium (earth as a distributed lossy conductor)

&nbsp; - Receiver (high dynamic range, dB/dt or induced voltage measurement)

\- Receiver front-end challenges:

&nbsp; - Offset drift

&nbsp; - Thermal coupling

&nbsp; - Dielectric memory effects

&nbsp; - Microphonics

\- Cable and dielectric behavior:

&nbsp; - Why PTFE performs well

&nbsp; - Comparison with problematic dielectrics

\- Integrator-based receiver architecture:

&nbsp; - Timing, gain, and reset behavior

&nbsp; - Charge injection and reset constraints

\- Practical TX design issues:

&nbsp; - Avalanche energy

&nbsp; - Clamp networks

&nbsp; - Damping resistors

&nbsp; - Hi/low moment behavior

\- DIY calculation examples:

&nbsp; - Coil current

&nbsp; - Stored energy

&nbsp; - LC resonance

&nbsp; - Critical damping



\*\*Purpose:\*\*  

To give engineers an intuition for \*why TEM behaves the way it does\* and which parts of the system actually dominate measurement quality.



---



\### 2. \*Transient Electromagnetic (TEM) Systems – An Electronics-Centered Perspective\*  

📄 \*\*File:\*\* `Transient Electromagnetic (TEM) Systems.pptx` :contentReference\[oaicite:1]{index=1}



This presentation explains \*\*why TEM instruments are exceptionally difficult to build\*\*, focusing on electronics constraints rather than theory.



\#### Core ideas:

\- TEM systems must handle \*\*6–7 decades of dynamic range\*\*

\- The transmitter is a \*\*worst-case electrical load\*\*

\- Early-time accuracy is brutally sensitive to timing and waveform fidelity



\#### Key technical topics:

\- Dynamic range limitations of linear ADC chains

\- Necessity of:

&nbsp; - Gain staging

&nbsp; - Log gating

&nbsp; - Stacking

\- Transmitter turn-off physics:

&nbsp; - kV-level voltages

&nbsp; - Energy redirection at turn-off

&nbsp; - Clamp topology effects on waveform validity

\- Early-time measurement sensitivity:

&nbsp; - ~100 ns timing accuracy requirement

&nbsp; - Direct coupling between turn-off distortion and false geology

\- Receiver reality:

&nbsp; - Measures dB/dt, not B(t)

&nbsp; - DC offsets are irrelevant, saturation is fatal

\- Stacking as \*\*time-domain lock-in amplification\*\*

\- Power-line interference cancellation via timing, not filtering

\- Why conductive coupling \*\*cannot be fixed in post-processing\*\*

\- Airborne TEM:

&nbsp; - Motion-induced EMF

&nbsp; - Geometry uncertainty

&nbsp; - Calibration as an electronics problem



\*\*Purpose:\*\*  

To explain \*why TEM success or failure is decided in hardware and timing\*, long before inversion or interpretation.



---



\### 3. \*TX08 Firmware\*  

📄 \*\*File:\*\* `TX08 Firmware.pptx` :contentReference\[oaicite:2]{index=2}



This presentation documents the \*\*embedded firmware architecture of the TX08 transmitter\*\*, implemented on an 8051-class microcontroller.



\#### Core ideas:

\- Even a slow MCU can deliver precision timing if the architecture is correct

\- Hardware peripherals, not software loops, define determinism



\#### Key technical topics:

\- System responsibilities:

&nbsp; - Pulse sequencing

&nbsp; - Sampling coordination

&nbsp; - Communication

&nbsp; - Parameter storage

\- Firmware module breakdown:

&nbsp; - `TxProc.c` – pulse sequencing and state machine

&nbsp; - `AnalogSample.c` – ADC setup and scaling

&nbsp; - `Kommunikation.c` – UART protocol and command handling

&nbsp; - `config.c` – parameter validation and defaults

&nbsp; - `F000\_FlashPrimitives.c` – flash persistence

&nbsp; - `Global.c` – shared state

\- PCA (Programmable Counter Array) as the \*\*real-time executive\*\*

&nbsp; - TX edge detection

&nbsp; - ADC scheduling

&nbsp; - Sign/polarity sequencing

&nbsp; - Self-test triggering

\- Interrupt-driven measurement sequencing:

&nbsp; - On-time current and voltage sampling

&nbsp; - Off-time scheduling

&nbsp; - Deterministic association of samples with TX state

\- Communication interface:

&nbsp; - Start/stop TX

&nbsp; - Parameter control

&nbsp; - Data readout

&nbsp; - Flash access

\- Development environment:

&nbsp; - Keil PK-51

&nbsp; - Silicon Labs 8051 toolchain



\*\*Purpose:\*\*  

To document how \*\*deterministic timing, sampling, and state control\*\* are achieved in the transmitter firmware.



