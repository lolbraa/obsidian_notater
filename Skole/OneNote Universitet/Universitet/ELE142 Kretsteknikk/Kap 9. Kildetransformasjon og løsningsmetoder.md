> [!caution] This page contained a drawing which was not converted.   

Jobbe i frekvensdomenet. Gjøre om til viser. Obs, sinus er -90grader

# Kildetransformasjon

![Exported image](Exported%20image%2020240415112841-0.png)                                                                                                            ![Exported image](Exported%20image%2020240415112841-1.png) ![Exported image](Exported%20image%2020240415112841-2.png)  ![Exported image](Exported%20image%2020240415112841-3.png) ![Exported image](Exported%20image%2020240415112841-4.png)

clear all, close all, clc  
syms I I1 I2 Vx  
Eq1=  
Eq2=  
Eq3=  
Eq4=  
svar=solve([Eq1, Eq2, Eq3, Eq4],[I, I1, I2, Vx]);  
I=double(svar.I)  
AbsI=abs(I)  
FaseI=phase(I)*180/pi

![Exported image](Exported%20image%2020240415112841-5.octet-stream) ![Exported image](Exported%20image%2020240415112841-6.octet-stream) ![Exported image](Exported%20image%2020240415112841-7.octet-stream) ![Exported image](Exported%20image%2020240415112841-8.octet-stream) ![Exported image](Exported%20image%2020240415112841-9.octet-stream) ![Exported image](Exported%20image%2020240415112841-10.octet-stream) ![Exported image](Exported%20image%2020240415112841-11.octet-stream)

søndag 11. februar 2024  
16:31

![Exported image](Exported%20image%2020240415112841-12.png) ![Exported image](Exported%20image%2020240415112841-13.png) ![Exported image](Exported%20image%2020240415112841-14.png) ![Exported image](Exported%20image%2020240415112841-15.png) ![Exported image](Exported%20image%2020240415112841-16.png)

%Oppg 9.56  
clear all, close all, clc  
syms V1 V2  
Eq1=…==0;  
Eq2=…==0;  
svar=solve([Eq1, Eq2],[V1, V2]);  
V1=double(svar.V1)  
V2=double(svar.V2)

![Exported image](Exported%20image%2020240415112841-17.png)                                                                                                                                                                                                     ![Exported image](Exported%20image%2020240415112841-18.png) ![Exported image](Exported%20image%2020240415112841-19.octet-stream) ![Exported image](Exported%20image%2020240415112841-20.octet-stream) ![Exported image](Exported%20image%2020240415112841-21.octet-stream) ![Exported image](Exported%20image%2020240415112841-22.octet-stream) ![9.8 The Node-voltage Method In Sections 4.2—4.4, we introduced the node-voltage method of circuit analysis, culminating in Analysis Method 4.3 (p. 130). We can use this analysis method to find the steady-state response for circuits with sinusoi_ dal sources. We need to make a few modifications: If the circuit is in the time domain, it must be transformed to the appropriate frequency domain, To do this, transform known voltages and currents to phasors, replace unknown voltages and currents with phasor symbols, and replace the component values for resistors, in- ductors, mutually coupled coils, and capacitors with their impedance values. • Follow the steps in Analysis Method 4.3 to find the values of the un- known voltage and current phasors of interest. Apply the inverse phasor transform to the voltage and current pha- sors to find the steady-state values of the corresponding voltages and currents in the time domain. Example 9.13 illustrates these steps. Assessment Problem 9.12 and many of the chapter problems give you an opportunity to use the node-voltage method to solve for steady-state sinusoidal responses. ](Exported%20image%2020240415112841-23.jpeg)