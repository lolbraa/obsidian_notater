[GitHub - artisticat1/obsidian-latex-suite: Make typesetting LaTeX as fast as handwriting through snippets, text expansion, and editor enhancements](https://github.com/artisticat1/obsidian-latex-suite?tab=readme-ov-file#cheatsheet)

I de fleste tilfeller (utenom høyt trykk/temp) bruker man RTD (Resistance Thermo Detector)
- Pt100 (mest brukt), Pt1000
	- Pt er platinum - tynn tråd. Edelt metall, stabilt med **liten variasjon mellom produksjoner og over tid**.
	- ≈100 Ω ved 0 °C
	- ≈138 Ω ved 100 °C
	- 1 ohm tilsvarer ca. halvannen grad
- Thermistor - Thermal Sensitive resistor. Laget av halvledermateriale, ikke metall
	- NTC thermistor - Negative Termperature Coefficient
	- Veldig sensitiv, stor forskjell i ohm per grad

Man har også termoelement (themocouple) - måling av spenning som varierer med temperatur.

## Pt100
![[Måleteknikk 1 - Temperatur og resistans-2025.08.21 13.21.40.webp|550]]

## NTC
![[Måleteknikk 1 - Temperatur og resistans-2025.08.21 13.52.20.webp|550]]![[Måleteknikk 1 - Temperatur og resistans-2025.08.21 13.52.30.webp|550]]


# Måling av resistans for å kunne måle temperatur
Må ha lav effekt for å ikke forstyrre målingene; gjerne 1 mW.

## Målebro
Kan måle små forskjeller - lettere å måle forskjell på 0.1 ohm enn 1mV.
![[Måleteknikk 1 - Temperatur og resistans-2025.08.21 14.19.33.webp|550]]
![[Måleteknikk 1 - Temperatur og resistans-2025.08.21 14.20.01.webp|550]]


## Ta hensyn til resistans til ledningsnettet
![[Måleteknikk 1 - Temperatur og resistans-2025.08.21 14.41.34.webp|550]]



![[Måleteknikk 1 - Temperatur og resistans-2025.08.21 14.41.59.webp|550]]
Ikke nøyaktig nok for oljeindustrien (NORSOK)

![[Måleteknikk 1 - Temperatur og resistans-2025.08.21 14.42.12.webp|550]]
![[Måleteknikk 1 - Temperatur og resistans-2025.08.21 14.47.52.webp]]


![[Måleteknikk 1 - Temperatur og resistans-2025.08.21 14.42.44.webp|550]]


# Respons på temperatuforandring
Hvor rask er endring i måling ved temperaturforandring?
![[Måleteknikk 1 - Temperatur og resistans-2025.08.28 12.30.01.webp|550]]

Karakteristisk tid, tidskonstant: $$t_{c} = \frac{\rho Vc_{p}}{hA_{s}}$$
$$
T(t) = T_{a} + (T_{o}-T_{a})e^{-t/t_{c}}
$$

