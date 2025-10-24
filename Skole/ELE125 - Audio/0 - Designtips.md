# Poler og nullpunkt
![[0 - Designtips-2025.05.13 08.55.59.png|550]]





# Designtips
![[0 - Designtips.jpg.jpg]]


![[image.jpg]]


# Valg av komponenter
TH = through hole
SM = surface mount

Se [[Skole/ELE125 - Audio/Oblig 1|Oblig 1]]

## Kondensator
Elektrolytt har gjerne større strøm (lekkstrøm) gjennom seg enn ikke-elektrolytt

ESR is a measure of how much the component deviates from a mathematically pure capacitance. The series resistance is partly due to the physical resistance of leads and foils and partly due to losses in the dielectric. It can also be expressed as tan-δ (tan-delta). Tan-delta is the tangent of the phase angle between the voltage across and the current fowing through the capacitor. 


Toleranse:
- Elektrolytt har gjerne ca +- 20%
- ikke-elektrolytt har gjerne +- 10%

### Discharging
Use a 10 Ω WW resistor across the terminals rather than a screwdriver unless you’re not too worried about the screwdriver, the capacitor, or your eyesight.
### Dielectric absorption
Dielectric absorption is a well-known phenomenon: take a large electrolytic, charge it up, and then make sure it is fully discharged. Wait a few minutes, and the charge will partially reappear, as if from nowhere. This ‘memory effect’ also occurs in non-electrolytics to a lesser degree; it is a property of the dielectric and is minimised by using polystyrene, polypropylene, NPO ceramic, or PTFE dielectrics. Dielectric absorption is invariably simulated by a linear model composed of extra resistors and capacitances; nevertheless dielectric absorption and distortion correlate across the different dielectrics. 

### Capacitor non-linearity
Capacitor non-linearity is undoubtedly the least known of these shortcomings. A typical RC lowpass flter can be made with a series resistor and a shunt capacitor, and if you examine the output with a distortion analyser, you may fnd to your consternation that the circuit is not linear. If the capacitor is a non-electrolytic type with a dielectric such as polyester, then the distortion is relatively pure third harmonic, showing that the effect is symmetrical. For a 10 Vrms input, the THD level may be 0.001% or more. This may not sound like much, but it is substantially greater than the mid-band distortion of a good opamp. Capacitor non-linearity is dealt with at greater length later. 


