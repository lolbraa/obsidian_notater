> [!caution] This page contained a drawing which was not converted.   

# 1-1 Digital and Analog Quantities

_Digital, derive from "counting digits"_  
Digital: Involves quantities of discrete values  
Analog: Involves quantities with continuous value
 
Example: Natural phenomenon's which can be measured **quantitatively** occur in analog form

- The change of temperature is gradual, continous.
- Measurement **sampled** every hour are discrete values and may be digitized.
- They are not the same, but holds information about the other.
 
# 1-2 Binary Digits, Logic Levels, and Digital Waveforms

## Binary Digit

**Positive Logic:** Digital circuits/systems involves only two possible states, represented by two different voltage levels: HIGH / 1 and LOW / 0.

- The opposite system is called **negative logic.**

**Binary:** The two-state number system  
**Bit:** A BInary digiT
 
## Logic Levels

**Logic Levels - Voltage Level**: In analog circuitry a HIGH (or LOW) is defined between a specified minimum and maximum value. In between the accepted voltage levels there is voltages are unacceptable.

- **Digital Waveforms**: A continuous series of changing voltage levels.
 
## Digital waveforms

**Pulse**: A positive pulse is the change from LOW to HIGH. Negative pulse is opposite change.

- **Rising/leading edge**: Occurs when the pulse changes to HIGH.
- **Falling/trailing edge**: Occurs when the pulse changes to LOW.
- **Ideal pulse**: Transition between pulses are "never" ideal, however it's often assumed.
- **Nonideal pulse**: The real deal.
    
    - Overshoot and ringing sometimes produced by stray inductive/capacitive effects.
    - Droop can be caused by stray capacitive and circuit resistance, forming an RC circuit with a ow time constant.
    - Rise/fall time: Commonly measured between 10% and 90% of the pulse amplitude.
    - Pulse width: Measure of the duration of the pulse; often the interval between 50%-point on the rise and fall of a pulse.
 _Waveform Characteristics_

**Pulse Trains:** Digital systems often consists of a series of pulses

- **Periodic:** Repeats at fixed intervals, period (T) [s]. Duty Cycle is an important characteristic: Ratio of the pulse width (tw) to the period (T), expressed as an percentage = (tw/T) *100%
    
## A Digital Waveform Carries binary information

**Bit time:** The defined time interval each bit in a sequence occupies.

- **The Clock:** A periodic waveform in which the interval between pulses is the bit time.
   

![Exported image](Exported%20image%2020240415112117-0.jpeg) ![Exported image](Exported%20image%2020240415112117-1.png) ![Exported image](Exported%20image%2020240415112117-2.jpeg) ![Exported image](Exported%20image%2020240415112117-3.png)

Ulike måter å transmitere informasjon avhengig av situasjon

- Kortdistanse kabel: Gjerne differanse mellom to kabler. 2 spennings- eller strømnivå
- Langdistanse kabel og radio: Amplitude, frekvens, fase-modulasjon eller fase-kombinasjon
- Optisk: Blinking og modulasjon
 
Representasjon av bits I lagring