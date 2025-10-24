> [!caution] This page contained a drawing which was not converted.   

![Exported image](Exported%20image%2020240415112837-0.png)

Første ledd i løsningen er transienten og andre lettet er steady-state.  
Transienten er det vi har lært tidligere, step- og natural-response.  
Ser ikke på transient-signalet i dette kurset, men fokuserer på Steady State.

![Exported image](Exported%20image%2020240415112837-1.png) ![Exported image](Exported%20image%2020240415112837-2.png) ![Exported image](Exported%20image%2020240415112837-3.png)

Positive fase-avvik (i grader) ligger foran referansepunktet

Bruker cosinus som referanse, og legger heller inn -90grader.

## Spole

![Exported image](Exported%20image%2020240415112837-4.png)

Spenning kommer med en gang, strømmen kommer etter.

![Exported image](Exported%20image%2020240415112837-5.png)     

## RMS

Med DC-signal regner man enkelt med OHMs lov.￼Det er vanskelig å regne effekt av vekselspenning, men med RMS-verdien er det enklere.

![Exported image](Exported%20image%2020240415112837-6.png) ![Exported image](Exported%20image%2020240415112837-7.png)

Dette er formel for å regne arbeid rett ut fra vekselspenning.
 
Kan forenkle:

![Exported image](Exported%20image%2020240415112837-8.png)

Root (kvadratrotet), mean (integralet delt på tid, altså gj.s.), squared (V opphøyd i to).

![Exported image](Exported%20image%2020240415112837-9.png) ![Exported image](Exported%20image%2020240415112837-10.png)  

RMS er altså kun spenning delt på rot av to.  
Med RMS kan man regne med Ohms lov direkte.
 
## Kondensator

![Exported image](Exported%20image%2020240415112837-11.png)  
![Exported image](Exported%20image%2020240415112837-12.png)

# Sinussignal og faseavvik

![Exported image](Exported%20image%2020240415112837-13.png) ![C: Det ligger en spenning v(t) = 50 • COS (l over en motstand på 300Q. Hvilken effekt mottas i motstanden (1 desimal nøyaktighet) ? ](Exported%20image%2020240415112837-14.png)                                                                                                                       

# Visere

Det er vinkel-forskjellen som er viktig.  
Visere er en forenkling av sinusfunksjoner satt inn i eulers med imaginære tall (j).  
Det gjør at man kan regne amplituder og vinkler som vektorer.  
Det er forskjellen mellom strøm- og spenningsvinkel som er viktig.
   
![Exported image](Exported%20image%2020240415112837-15.png) ![Exported image](Exported%20image%2020240415112837-16.png)  
![Exported image](Exported%20image%2020240415112837-17.png)

Frekvensen er viktig for å regne impedansen, men ikke visere - det er kun vinkelen mellom.

![Exported image](Exported%20image%2020240415112837-18.png)   
Viser er startposisjonen (t=0)
      

# Impedanse

![Exported image](Exported%20image%2020240415112837-19.png)

Når man er i impedanse og visere kan man også utføre ohms lov
 
Tidsplanet (det du kan måle med oscilloskop)  
Frekvensplanet (visere og frekvenser)

![Exported image](Exported%20image%2020240415112837-20.png)  

Impedansen til en spole.
 ![Exported image](Exported%20image%2020240415112837-21.png)

Impedansen til en kondensator
   
![Exported image](Exported%20image%2020240415112837-22.png)

![Exported image](Exported%20image%2020240415112837-23.png)

![Exported image](Exported%20image%2020240415112837-24.png)

![B: To spenningskilder på VI (t) +40)1'" og v2 (t) COSO 00;Tt +120)V er koblet sammen i serie. Hva er total spenningsviser over dem VT = VI + V2 (1 desimal nøyaktighet)? ](Exported%20image%2020240415112837-25.png)                                                                                                                                                                                                                                                                                                                          

# Repetisjon

![Exported image](Exported%20image%2020240415112837-26.png) ![Exported image](Exported%20image%2020240415112837-27.png) ![Exported image](Exported%20image%2020240415112837-28.png) ![Exported image](Exported%20image%2020240415112837-29.png) ![Exported image](Exported%20image%2020240415112837-30.png) ![Exported image](Exported%20image%2020240415112837-31.png) ![Exported image](Exported%20image%2020240415112837-32.png) ![Exported image](Exported%20image%2020240415112837-33.png)

![Exported image](Exported%20image%2020240415112837-34.png)

![Exported image](Exported%20image%2020240415112837-35.png) ![Exported image](Exported%20image%2020240415112837-36.png) ![Exported image](Exported%20image%2020240415112837-37.png) ![Exported image](Exported%20image%2020240415112837-38.png) ![Exported image](Exported%20image%2020240415112837-39.png) ![Exported image](Exported%20image%2020240415112837-40.png) ![Exported image](Exported%20image%2020240415112837-41.png) ![Exported image](Exported%20image%2020240415112837-42.png)                                                                                                                                                                                                                                        ![Exported image](Exported%20image%2020240415112837-43.png)                                                                                                                                                                                

fredag 26. januar 2024  
14:27

![Exported image](Exported%20image%2020240415112837-44.png)

clc  
I=1;  
Z1=2*cos(30*pi/180)+2*sin(30*pi/180)*i;  
Z2=4*cos(-25*pi/180)+4*sin(-25*pi/180)*i;  
I2=Z1*I/(Z1+Z2);  
AbsI2=abs(I2)  
FaseI2=phase(I2)*180/pi
 
AbsI2 = 0.3703
 
FaseI2 = 37.3441

![Exported image](Exported%20image%2020240415112837-45.png)                                                                                                                                                                                                                                                                                       

29jan-T1-2  
fredag 26. januar 2024  
14:08

![Exported image](Exported%20image%2020240415112837-46.png)                                                                                                                                                                                                                                             

![Exported image](Exported%20image%2020240415112837-47.png)     

![Exported image](Exported%20image%2020240415112837-48.png) ![Exported image](Exported%20image%2020240415112837-49.octet-stream) ![Exported image](Exported%20image%2020240415112837-50.octet-stream) ![Exported image](Exported%20image%2020240415112837-51.octet-stream) ![Exported image](Exported%20image%2020240415112837-52.octet-stream) ![Exported image](Exported%20image%2020240415112837-53.octet-stream) ![Exported image](Exported%20image%2020240415112837-54.octet-stream) ![Exported image](Exported%20image%2020240415112837-55.octet-stream) ![Exported image](Exported%20image%2020240415112837-56.octet-stream) ![Exported image](Exported%20image%2020240415112837-57.octet-stream) ![Exported image](Exported%20image%2020240415112837-58.octet-stream)

# Viserdiagram

![Exported image](Exported%20image%2020240415112837-59.octet-stream)     

![Exported image](Exported%20image%2020240415112837-60.octet-stream) ![Exported image](Exported%20image%2020240415112837-61.octet-stream) ![Using the steady-state component of Eq. 9.7, we identify four import. ant characteristics of the steady-state solution: 1. The steady-state solution is a cosine function, just like the circuit's source. 2. The frequency of the solution is identical to the frequency of the source. This condition is always true in a linear circuit when the circuit parameters, R, L, and C, are constant. (If frequencies in the solution are not present in the source, there is a nonlinear element in the circuit.) 3. The maximum amplitude of the steady-state response, in general, differs from the maximum amplitude of the source. For the circuit in Fig. 9.5, the maximum amplitude of the current is V,n// R2 + 02L2, while the maximum amplitude of the source is Vm. 4. The phase angle of the steady-state response, in general, differs from the phase angle of the source. For the circuit being discussed, the phase angle ofthe current is — 0, and that of the voltage source is d). These characteristics motivate the phasor method, which we introduce in Section 9.3. Note that finding only the steady-state response means find- ing only its maximum amplitude and phase angle. The waveform and fre- quency of the steady-state response are already known because they are the same as the circuit's source. ](Exported%20image%2020240415112837-62.jpeg) ![Another important characteristic of the sinusoidal voltage (or cur- rent) is its rms value. The rms value of a periodic function is defined the square root of the mean value of the squared function. Hence, if V cos(wt + 4), the rms value of is as Ill rms 1 V % cos2(ot + 4) dt. to (9.4) Note from Eq. 9.4 that we obtain the mean value of the squared voltage by integrating 02 over one period (that is, from to to to + T) and then di- viding by the range of integration, T. Note further that the starting point for the integration to is arbitrary. The quantity under the square root sign in Eq. 9.4 reduces to V %/2. (See Problem 9.8.) Hence, the rms value of v is RMS VALUE OF A SINUSOIDAL VOLTAGE SOURCE (9.5) rms ](Exported%20image%2020240415112837-63.jpeg) ![v = VDT cos(ot + (9.1) To aid discussion of the parameters in Eq, 9.1, we show the voltage ver. sus time plot in Fig. 9.1. The coefficient gives the maximum amplitude of the sinusoidal voltage. Because ± 1 bounds the cosine function, ± V bounds the amplitude, as seen in Fig, 9.1. You can also see that the sinusoi- dal function repeats at regular intervals; therefore, it is a periodic function. A periodic function is characterized by the time required for the function to pass through all its possible values, This time is the period of the function, T. and is measured in seconds, The reciprocal of T gives the number of cycles per second, or the frequency, of the periodic function, and is denoted f, so 1 (9.2) A cycle per second is called a hertz, abbreviated Hz. (The term cycles per second rarely is used in contemporary technical literature.) Now look at the coefficient of t in Eq. 9.1. Omega (o) represents the angular frequency of the sinusoidal function and is related to both T and f. = 27rf = 27/ T (radians/second). (9.3) ](Exported%20image%2020240415112837-64.jpeg) ![RELATIONSHIP BETWEEN PHASOR VOLTAGE AND PHASOR CURRENT FOR AN INDUCTOR V jOL1. (9.11) Equation 9.11 states that the phasor voltage at the terminals of ap inductor equals joL times the phasor current. Figure 9.10 shows the frequency-domain equivalent circuit for the inductor. Note that the rela tionship between phasor voltage and phasor current for an inductor also applies for the mutual inductance in one coil due to current flowing i another mutually coupled coil. That is, the phasor voltage at the terminals of one coil in a mutually coupled pair of coils equals joM times the phasoi current in the other coil. We can rewrite Eq. 9.11 as V = (OL 900)1mL o LIm/(0i + 90)0, ](Exported%20image%2020240415112837-65.jpeg) ![fince is the phasor representation ot the sinus al voltage, we can xpress the current phasor in terms of the voltage phasor as 1 = jocv. slow express the voltage phasor in terms of the current phasor, to con. torm to the phasor equations for resistors and inductors: RELATIONSHIP BETWEEN PHASOR VOLTAGE AND PHASOR CURRENT FOR A CAPACITOR 1 1. joc (9.12) Equation _9.12 demonstrates that the equivalent circuit for the capacitor in he phasor domain is as shown in Fig. 9.12. The voltage across the terminals of a capacitor lags behind the current y 900. We can show this by rewriting Eq. 9.12 as 1 90)0. Thus, we can also say that the current leads the voltage by 900. Figure 9•13 hows the phase relationship between the current and voltage at the termi- nals of a capacitor. ](Exported%20image%2020240415112837-66.jpeg) ![Vab Zll + Z21 + (Zl + 7.42 + + zn)l. The equivalent impedance between terminals a,b is COMBINING IMPEDANCES IN SERIES ab zab 1 (9.16) Remember from Chapter 3 that we can use voltage division to find the voltage across a single component from a collection of series-connected components whose total voltage is known (Eq. 3.9). We derived the volt- age division equation using the equation for the equivalent resistance of series-connected resistors. Using the same process, we can derive the voltage division equation for frequency-domain circuits, where Vs is the voltage applied to a collection of series-connected impedances, V] is the voltage across the impedance Zj, and Zeq is the equivalent impedance of the series-connected impedances: VOLTAGE DIVISION IN THE FREQUENCY DOMAIN zj zeq (9.17) ](Exported%20image%2020240415112837-67.jpeg) ![TABLE 9.2 Circuit Element Resistor Inductor Capacitor Admittance and Susceptance Values Admittance (Y) Susceptance G (conductance) j(-1/oL) joc -I/OL zab = Zl + We can also express Eq. 9.18 in terms of admittance, defined as the rocal of impedance and denoted Y. Thus 1 G + jB (siemens). z Admittance is a complex number whose real part, G, is called conductance and whose imaginary part, B, is called susceptance. Like admittance, con. ductance and susceptance are measured in siemens (S). Replacing imped. ances with admittances in Eq. 9.18, we get Yab = Yl + Y2 + The admittance of each of the ideal passive circuit elements also is worth noting and is summarized in Table 9.2. Finally, remember from Chapter 3 that we can use current division to find the current in a single branch from a collection of parallel-connected branches whose total current is known (Eq. 3.10). We derived the cur. rent division equation using the equation for the equivalent resistance of parallel-connected resistors. Using the same process, we can derive the current division equation for frequency-domain circuits, where Is is the current supplied to a collection of parallel-connected impedances, Ij is the current in the branch containing impedance Zj, and Zeq is the equivalent impedance of the parallel-connected impedances: CURRENT DIVISION IN THE FREQUENCY DOMAIN ) zeq 1] zj (9.20) ](Exported%20image%2020240415112837-68.jpeg)