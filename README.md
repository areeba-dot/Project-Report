# Project-Report
Microvolts level noise detection in thermal cameras
Project Introduction
Thermal cameras rely on infrared detectors to capture temperature variations, converting infrared radiation into electrical signals to create thermal images. For optimal performance, these detectors require stable biasing supplies, as even small amounts of noise—ranging from microvolts to millivolts—can interfere with the weak signals and degrade image quality.
The project's objective was to reduce noise in the biasing supplies, which directly impacts the accuracy and reliability of the thermal camera’s output. Various noise reduction techniques were employed. Low-pass and Butterworth filters were used to eliminate high-frequency noise while maintaining signal integrity due to their smooth roll-off and minimal phase distortion. Additionally, single-ended to differential signal conversion was implemented to cancel common-mode noise and improve the signal-to-noise ratio. Preamplifiers were added to boost signal strength, ensuring that the processed signal could withstand noise at later stages.
An integral part of the project involved studying and using the Picotest noise measurement apparatus, which provided high-precision noise analysis tools such as specialized probes, preamplifiers, and signal analyzers. These tools were essential for accurately measuring the noise in the biasing circuits and evaluating the effectiveness of the noise reduction techniques.
Overall, the project addressed the critical challenge of reducing noise in the biasing supplies for infrared detectors in thermal cameras. By implementing advanced filtering, signal conversion, and amplification techniques, combined with precise noise measurement, the project successfully improved the thermal cameras' ability to detect accurate temperature differences, enhancing their performance in applications like surveillance, industrial inspections, and medical diagnostics.

TIDA-01583 Refrence design

The project started off with study of datasheet of TID-01583 which is a refrence design for ultra low noise power supply by texas instruments. The document presented a comprehensive reference design aimed at generating ultra-low-noise, programmable bias voltages and power supplies specifically for thermal image sensors, with a focus on uncooled microbolometer detectors. These detectors are crucial in thermal imaging cameras, which require precise and stable bias voltages to function effectively. The design addresses the inherent challenges posed by traditional power supplies, which often fail to meet the stringent accuracy and noise requirements necessary for optimal performance in thermal imaging applications.

To achieve this, the reference design utilizes a combination of Texas Instruments' advanced components, including the DAC80508 precision digital-to-analog converter (DAC), the OPA2192 low-noise precision amplifier, and the TPS71750 and TPS71733 high-PSRR low-dropout regulators (LDOs). The DAC80508 features a true 16-bit resolution and buffered rail-to-rail voltage output, allowing for programmable voltage outputs that can be adjusted on-the-fly to cater to different sensor requirements. The OPA2192 amplifier provides low offset voltage and drift, ensuring high DC precision and low noise, while the TPS717 series LDOs deliver excellent power supply rejection and low quiescent current.


The design incorporates a thorough analysis of stability to ensure reliable operation when driving capacitive loads, which can introduce instability in amplifier circuits. The stability analysis focuses on maintaining an adequate phase margin to prevent oscillations and ensure consistent performance. Additionally, noise analysis is conducted to minimize output noise through the implementation of heavy low-pass filtering, which effectively suppresses unwanted noise from the DAC and other components.

From this document i gained the knowledge about significance of utilizing ultra-low-noise components and careful design considerations to achieve precise bias voltages for thermal imaging applications. This information  can be applied in detection of microvolt-level noise by implementing the recommended precision DACs and low-noise amplifiers to ensure that the biasing supplies for detectors in thermal cameras maintain optimal performance with minimal noise interference, thereby enhancing image quality and thermal sensitivity.



Software of choice

After this document study, i further moved onto the simulations. For simulations of analogue electronics the software being commonly used by the engineers these days include LTspice,multisim,simulink and many more. The software I've used is TINA-TI. It is a simulation tool which provides all the conventional DC, transient and frequency domain analysis of SPICE and much more.  TINA is available for both offline and online use, making it suitable for a wider range use.TINA was given preference upon softwares having more advanced features because of several reasons. One being that some previously designed circuits to be used in this project were made in TINA-TI. Along with that TINA also offers user-friendly interface and versatile simulation capabilities, making it accessible for beginners and efficient for experienced users. 
After gaining experience of TINA software and comparing it's features with multisim and simulink, I'm of opinion that Multisim software by National Instruments has much more advanced and a larger number of features as compared to TINA. It could also be of great use in performing efficient simulations of an electronic circuit. 

Noise analysis
In simulations, the first task assigned to me was noise analysis of the biasing supplies.According to detectors' data sheet, it requires 4 biasing supplies. All of these are supplied through a biasing supply card. This card has low pass filters placed on each supply point. The voltages are named to be VSK, GFID, GSK and VBUS. All of these supplies have somewhat same circuitry at the back and hence I've simulated one of these in details i.e. VSK. It's circuit in figure below.


A low-pass filter is used at the biasing supply point to reduce high-frequency noise and ensure a stable voltage. Thermal detectors are sensitive to noise, and fluctuations in the bias supply can degrade their performance. The filter blocks unwanted noise, improving the signal-to-noise ratio and ensuring more accurate detection. This leads to clearer thermal images and prevents spurious signals from affecting the detector's output. 
Along with the DC voltage of few volts such as 2V given as input to the filter, a white noise of few Millivolts was also injected so as to keep the simulations closest to the real life measurements. As while doing the same in hardware, this much amount of noise is induced automatically because of wires and measuring probes.

The optimum noise range is different for various frequency ranges. For 1Hz to 1KHz the value of noise should not exceed 2μV, for 1Hz to 10 KHz 5μV and 100μV for 1Hz to 10MHz. From simulations performed, the average value of noise noted was 12.5nV.


When an AC voltage is given as input to the circuit, the output voltage is of few volts. As it is a low pass filter and hence allows only low frequency signals to pass through. For the same reason, when given a dc input, the output voltage signal is almost same as the input signal. 


Single ended to differential converter
Next, i moved on to the simulation of single ended to differential converter circuit which had been already designed specifically for this application. Single-ended to differential conversion is the process of converting a signal with reference to a single ground into two complementary signals, each referenced to the other .

This is commonly done to improve noise immunity, as differential signals are more resistant to common-mode noise—interference that affects both signal lines equally. In noise-sensitive applications , like the biasing supplies of detector, this conversion helps in minimizing the impact of external noise on the signal by allowing the noise present on both lines to cancel out, improving overall signal integrity and measurement accuracy.Single ended to differential conversion enhances the rejection ratio, signal to noise ratio as well as increases the data rate.

In provided design, THS4551 fully differential amplifier is being used to drive the AD9649 ADC as they complement each other perfectly in terms of performance. The AD9649 requires a differential input for optimal operation, as it reduces noise and distortion, leading to more accurate analog-to-digital conversion. The THS4551, being a fully differential amplifier, converts single-ended signals into differential ones, providing low noise and high linearity, which is critical for feeding clean signals into the ADC. Compared to a standard differential amplifier, the fully differential architecture of the THS4551 offers better common-mode noise rejection, enhanced dynamic range, and improved signal integrity. This ensures that the ADC receives a clean and precise signal, maximizing its performance.
The complete schematic of the circuit is shown in figure 
At the input of the circuit are two same level dc inputs. Both these voltages are kept at same level as in this case, ideally all the common mode signals would be rejected and only Vd will be amplified. Along with that, it also makes the biasing easier. 
The AC voltage is set at 1.5V peak to peak setting the voltage range from 0.2V to 3.0V as the detector output voltage ranges from 1.0V to 4.2V. Next to the input voltage are the biasing resistors followed by a capacitor serving the purpose of filtering and lessening noise.

After capacitor, signal is fed into a fully differential amplifier circuit. The zero ohm resistances mentioned in circuit provide the flexibility while performing the analysis on hardware. The common mode voltage is set as 1.357V which should also be output of amplifier circuit as

    Vocm = output on both points

The amplifier circuit is followed by a butterworth filter of third order followed by a feedback path. Gain is required to be at 1.11 in order for ADC to have an input of 1.7Vpp. The values of resistors and capacitors in butterworth filter are set so that the voltage after filter is atleast 90 percent of the voltage before filter.  

    V_o_u_t &= V_i_n * 90%
            = 1.7*0.9 \\
            &= 1.53V \\
     Gain &= input/output \\
              &=1.7/1.53  \\ 
              &=1.11      \\
FDA gain= \frac{Amplifier gain}{RLC network gain } \\
               &=1.11/ 0.9  \\
               &= 1.233 \\
         
The filter is set at a cut off frequency of 15MHz. Values of inductors and capacitor are set using the formula \\

    f_c &= 1/6.28 sq.rt LC \\



 I also recorded the overall noise in output of this circuit and it was recorded to be 46 \mu\text{V}
 Proposed changes in design
 While analyzing the physical implementation of this design, one of the doubts was about the Butterworth filter's cutoff frequency, which proved to be a little too high. Because of the high cutoff frequency, one of the issues faced was aliasing due to noise beyond the Nyquist frequency. 
Since the filter allowed noise components at frequencies higher than the Nyquist frequency to pass through, these high-frequency noise components folded back into the lower frequency range during digitization. This aliasing distorted the signal by superimposing unwanted high-frequency noise onto the original signal band, making it difficult to distinguish between the actual signal and the aliased noise. Consequently, this resulted in a degraded SNR, negatively impacting the accuracy and performance of the system, especially in precision-sensitive detector applications. To solve this issue i proposed a change in filter's cutoff frequency. In latest design the cutoff frequency which was previously 15MHz is now set to be 5MHz. 
\begin{align*}
f_c &= 1/6.28 sq. rt LC
For \\
L &= 750 nH \\
C &= 150pF \\
f_c= 15 MHz \\
\end{align*}
\begin{figure}[H]
    \centering
    \includegraphics[width=0.55\linewidth]{cutoff 1.png}
    \caption{Cut off frequency measured to be 12.51 MHz}
    \label{fig:enter-label}
\end{figure}
And,
\begin{align*}
 L &= 750 nH \\
C &= 500pF \\
f_c= 8 MHz \\
\end{align*}
\begin{figure}[H]
    \centering
    \includegraphics[width=0.55\linewidth]{cutoff 2.png}
    \caption{Cut off frequency measured to be 5 MHz}
    \label{fig:enter-label}
\end{figure}

The capacitor was changed instead of the inductor because it directly influences the cutoff frequency in low-pass filter designs, allowing for precise adjustment of the filter's frequency response.
\section{Apparatus study}
Lastly,I conducted an extensive study on the datasheets of the measurement equipment referenced in the document, focusing on their specifications and performance characteristics. Below are some of my key observations regarding the capabilities and advantages of each tool in the context of measuring noise of the detector's biasing signal.
\begin{figure}[H]
    \centering
    \includegraphics[width=0.55\linewidth]{1.png}
    \caption{Block diagram for the flow of signal}
    \label{fig:enter-label}
\end{figure}

 The P2104A PDN transmission line probes, J2180A ultra-low noise pre-amplifier, N9020 signal analyzer, 150V 1 MHz ripple probe, and P2106A resistive divider probe were highlighted as essential tools for this task.

Key terms were defined to provide clarity on the concepts involved in the measurements. The noise floor described as the minimum detectable signal level, influenced by both internal and external noise, which affects the system's dynamic range and sensitivity. The Power Supply Rejection Ratio (PSRR) explained as a measure of how well a circuit can filter out power supply noise, with higher values indicating better performance. Phase margin which is discussed in terms of system stability, where a positive margin suggests stability and a higher margin reduces the risk of oscillations.

The study also covered impedance, which is the total opposition to alternating current flow, combining resistance and reactance, and emphasizes the importance of shielding to protect circuits from electromagnetic interference (EMI). The pre-amplifier's role in amplifying weak signals while maintaining integrity and minimizing noise was also noted.

The ripple probe is characterized by its cost-effectiveness and bandwidth capabilities, with specific features such as a maximum voltage of 150V and a frequency cutoff of 1 MHz. The configuration details include a custom high-voltage divider probe, the J2180 pre-amplifier, and a DC bias injector, all designed to enhance measurement accuracy.
\begin{figure}[H]
    \centering
    \includegraphics[width=0.85\linewidth]{ripple probe.png}
    \caption{Configuration of ripple probe}
    \label{fig:enter-label}
\end{figure}

The PDN transmission line probes, particularly the P2104A, are explained as tools for measuring noise and ripple with advantages like integrated series resistors for extended measurement range and bidirectional capabilities. 
\begin{figure}[H]
    \centering
    \includegraphics[width=0.55\linewidth]{PDN probe.png}
    \caption{PDN probe P2104A}
    \label{fig:enter-label}
\end{figure}

The resistive divider probe, P2106A, is specifically designed for high-voltage environments, allowing for safe and accurate power supply noise measurements.
The J2180A is an ultra-low noise pre-amplifier designed for amplifying very weak signals, crucial for maintaining signal integrity in sensitive measurements. It has a bandwidth range of 0.1 Hz to 100 MHz, delivers an output voltage peak-to-peak of 3V, and boasts a noise level of 2.4 nVp er sq.rt Hz. Compatible with the P2106A resistive divider probe, it minimizes noise during amplification, and its high permeability shielding effectively reduces external interference.
\begin{figure}[H]
    \centering
    \includegraphics[width=0.55\linewidth]{J2180.png}
    \caption{Pre-amplifier J2180}
    \label{fig:enter-label}
\end{figure}
The signal analyzer, N9020A, is noted for its superior sensitivity and frequency range, making it more suitable for measuring low-noise signals compared to traditional oscilloscopes. I concluded the study with a summary of the measurement techniques and the importance of using the right tools for observing ripples in the output signal of the detector, emphasizing the overall goal of achieving reliable and precise noise measurements in power supply systems.
From all of my observations and study, I would recommend the use of probe P2106A along with the J2180A pre-amplifier and signal analyzer N9020A for practical measurement of noise, as this combination ensures optimal signal integrity, minimal noise introduction, and high sensitivity across a broad frequency range. The P2106A enables safe and accurate high-voltage measurements, the J2180A amplifies weak signals while maintaining low noise levels, and the N9020A provides superior analytical capabilities, making these tools ideal for precise microvolt-level noise assessments in power supply systems.

 \section{Way forward}
 The next step in the project which is yet to be done is the hardware implementation and measurement of the noise reduction techniques in real-world conditions. This involves physically assembling of the circuit using biasing supply card. After assembling the hardware, the Picotest apparatus will be employed to measure the actual noise levels in the biasing supplies, allowing for a direct comparison with the simulation results. The measurements will verify if the implemented techniques have successfully reduced noise to the desired microvolt range or if further adjustments are needed. This phase will also help identify any unforeseen issues in the practical setup, such as component tolerances or parasitic effects, which can then be addressed through iterative testing and refinements. Once the hardware proves effective in reducing noise, the system's impact on the thermal camera's image quality can be evaluated, ensuring it meets the required performance standards in real-world applications.
