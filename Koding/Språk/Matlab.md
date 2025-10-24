---
tags:
  - programmeringsspråk
---
# Hotkeys
CTRL + R: Kommenter
CTRL + T: Fjern kommentar

# Tall
## Forkorte
```MATLAB
double(vpa(svar.Ic,4))) 
```
## Konvertere
### Grader
```
rad2deg(angle(U1))
```

## Potenser
[Exponents and Logarithms](https://se.mathworks.com/help/matlab/exponents-and-logarithms.html?searchHighlight=logarithm&s_tid=srchtitle_support_results_2_logarithm)

|                                                                             |                                                             |
| --------------------------------------------------------------------------- | ----------------------------------------------------------- |
| [`exp`](https://se.mathworks.com/help/matlab/ref/double.exp.html)           | Exponential                                                 |
| [`expm1`](https://se.mathworks.com/help/matlab/ref/double.expm1.html)       | Compute `exp(X)-1` accurately for small `X`                 |
| [`log`](https://se.mathworks.com/help/matlab/ref/double.log.html)           | Natural logarithm                                           |
| [`log10`](https://se.mathworks.com/help/matlab/ref/double.log10.html)       | Common logarithm (base 10)                                  |
| [`log1p`](https://se.mathworks.com/help/matlab/ref/double.log1p.html)       | Compute natural logarithm of `1+X` accurately for small `X` |
| [`log2`](https://se.mathworks.com/help/matlab/ref/double.log2.html)         | Base 2 logarithm and floating-point number dissection       |
| [`nextpow2`](https://se.mathworks.com/help/matlab/ref/double.nextpow2.html) | Exponent of next higher power of 2                          |
| [`nthroot`](https://se.mathworks.com/help/matlab/ref/double.nthroot.html)   | Real nth root of real numbers                               |
| [`pow2`](https://se.mathworks.com/help/matlab/ref/double.pow2.html)         | Base 2 exponentiation and scaling of floating-point numbers |
| [`reallog`](https://se.mathworks.com/help/matlab/ref/double.reallog.html)   | Natural logarithm for nonnegative real arrays               |
| [`realpow`](https://se.mathworks.com/help/matlab/ref/double.realpow.html)   | Array power for real-only output                            |
| [`realsqrt`](https://se.mathworks.com/help/matlab/ref/double.realsqrt.html) | Square root for nonnegative real arrays                     |
| [`sqrt`](https://se.mathworks.com/help/matlab/ref/double.sqrt.html)         | Square root                                                 |
### Naturlig tall
Y = log(X) returns the natural logarithm ln(x) of each element in array X.

The log function’s domain includes negative and complex numbers, which can lead to unexpected results if used unintentionally. For negative and complex numbers z = u + i*w, the complex logarithm log(z) returns

## Komplekse tall
Skrive e-/vinkel-form i Matlab
```
% I = 0.5 vinkel 60 grader
% I = amplitude * (cosinus grader + j sinus grader)
I = 0.5 * (cosd(60) + 1j * sind(60))
```
Konjugere (Z*)
```
Z = 2+3i
Zc = conj(Z)

>> Zc = 2.0000 - 3.0000i
```
[Ekstrahere reell del](https://se.mathworks.com/help/matlab/ref/real.html)
```
Z = 2+3i;
X = real(Z)

>> X = 2
```
[Ekstrahere imaginær del](https://se.mathworks.com/help/matlab/ref/imag.html)
```
Z = 2+3i;
Y = imag(Z)

>> Y = 3
```
[Finne vinkel og størrelse](https://se.mathworks.com/help/matlab/ref/angle.html)
```
z = 2*exp(i*0.5)
>> z = 1.7552 + 0.9589i

r = abs(z)
>> r = 2

theta = angle(z)
>> theta = 0.5000

fprintf("Vo = %f V med vinkel %f grader", abs(Vo), rad2deg(angle(Vo)))
>> Vo = 28.118821 V med vinkel -51.330756 grader
```
# Symbolsk/algebra
## Grenseverdier
![[Matlab-1.png]]
![[Matlab-2.png|385]]
```
v_inf = limit(s * V(s), s, 0)
il_inf = limit(s * Il(s), s, 0)
limit((1 + x/n)^n, n, inf) % INFINITE
```
## Laplace
- ``laplace`` Laplacetransform
- ``ilaplace`` Invers Laplacetransform
- ``partfrac`` Delbrøkoppspalting
- ``simplify`` Forenkle uttrykk

## Lineær algebra
```
clear, clc
R1 = 6; R2 = 4; R3 = 6; R4 = 8;
Xc = -2i; Xl = 1i;
is1 = 6; vs2 = 2;

% Symbolske variabler
syms U1 U2 i2

% Likningene
l1 = is1 - U1/R1 - i2 == 0;
l2 = i2 - U2/(R3 + Xl) - (U2-vs2) /8 == 0;
l3 = i2 == (U1-U2) / (R2 + Xc);

% Løs likningene
svar = solve([l1, l2, l3], [U1, U2, i2])

% Hent ut et svar
U1 = vpa(svar.U1, 3)
```
#### forenkle likninger
```
V = simplify(svar.V)
```
*simplify($\frac{120\,{\left(s^2 +2\,s+1\right)}}{s\,{\left(10\,s^2 +21\,s+12\right)}}$)* = $\frac{120\,{{\left(s+1\right)}}^2 }{s\,{\left(10\,s^2 +21\,s+12\right)}}$





# Polynomer
[Polynomials- MATLAB & Simulink- MathWorks Nordic](https://se.mathworks.com/help/matlab/polynomials.html)
For et n-te polynom Må man skrive n antall siffer, selv om det bare er en 0.
Man skriver det i [] med , som delimeter.
```
p = [10, 20, 0, 3, 5]
```

## Røtter av et polynom
[roots - Polynomial roots - MATLAB- MathWorks Nordic](https://se.mathworks.com/help/matlab/ref/roots.html)
```
roots(P)
```
$$\left(\begin{array}{c}
-2\,\mathrm{i}\\
2\,\mathrm{i}
\end{array}\right)$$
## Røtter til et polynom
```
r = [10-20i, 1+3i] ???
poly(r)
```
for imaginære røtter, bruk solve
```
rotter = solve(komp,s)
```
## Multiplisere to polynom
```
a = conv(p,qw)
```

## Samle felles faktorer (faktorisere)
```
Teller = 2*k - s + k*s + 10*s^2 + s^3 - 10
collect(Teller)
----
s^3 + 10*s^2 + (k - 1)*s + 2*k - 10
```


# Brøker
## Hente ut teller og nevner fra en brøk
```
[Teller,Nevner]= numden(Fraction)
---
Teller = 2*k - s + k*s + 10*s^2 + s^3 - 10
Nevner = (s - 1)*(s + 1)*(s + 10)

```


# Transferfunction
```
tf(numerator,denominator)

H = tf([1 2 3], [1 2 3])
H = tf(poly([-5]) , poly([0, -1, -40]))
```
eller
```
s = tf('s')
Gp = 20*(1+s/10)/((1 + s)^2 * (1+s/50) * (1+s/100))
```

## Eks:
$$
H(s) = \frac{10(s+5)}{s²+2s+5}
$$
```
teller = 10*[1,5];
nevner = [1,2,5];
H=tf(teller,nevner)
--------------------------
H =
 
    10 s + 50
  -------------
  s^2 + 2 s + 5
```
eller
```
Gp =
 
                  100000 s + 1e06
  ------------------------------------------------
  10 s^4 + 1520 s^3 + 53010 s^2 + 101500 s + 50000
```



## Hente ut en verdi for transferfunksjon
[How to compute the value in one point through the transferfunction? - MATLAB Answers - MATLAB Central](https://se.mathworks.com/matlabcentral/answers/48561-how-to-compute-the-value-in-one-point-through-the-transferfunction)
```
evalfr(M,12j)
```

```matlab
s = tf('s')
G = 75 * (1 + s/10) / (s * (1 + s/2) * (1+s/40))

M = feedback(G, 1)

z = evalfr(M,12j)
fprintf("M(12j) = %f forsterkning \nmed vinkel %f grader", abs(z), rad2deg(angle(z)))
----
z = 1.1124 - 0.9411i

M(12j) = 1.457096 forsterkning 
med vinkel -40.233144 grader
```

## Forenkle transferfunksjon
```
TF = (s + 2) / (s + 5); % Originaluttrykk
TF = minreal(TF) % Forenkle
```

## Visualisere transferfunction
### Grafe pole-zero map
```
pzmap(H)
```

### Grafe step-/sprangrespons med grid
```
step(H)
grid;
```



### Grafe impulsresponsen med grid
```
impulse(H)
grid;
```

### Grafe bodeplot
$$
H(s) = \frac{{50 * ( 1 + \frac{s}{5} )}}{s * ( 1 + \frac{s}{1} )(1 + \frac{s}{40})}
$$
Gå fra en faktorisert transferfunksjon til en funksjon som man kan skrive i Matlab
I dette tilfellet, multiplisere inn $\frac{5}{5}$ og $\frac{40}{40}$. De kansellerer ut brøkene i parantesene. Da er det enkelt å lese av nullpunkter og polene: -5 og 0, -1, -40.

$$
H(s) * \frac{5}{5} *\frac{40}{40} = \frac{{400 * ( s + 5 )}}{s * (s + 1 )(s + 40)}
$$

```matlab
clc, clear all
H = 400 * tf(poly([-5]) , poly([0, -1, -40]))
bode(H)
grid
```

#### OBS: Z-domene blir feil, bruk `dbode`
```
TF = (s + 2) / (s + 5); % Originaluttrykk
TF = minreal(TF) % Forenkle

bodeplot(TF)
dbode(TF.Numerator, TF.Denominator, T)
```

#### Flere bodeplots sammen
```
bode(G, Gp, GR)
```

#### Grafe bodeplot med asymptoter
Trenger `asymp.m`-fil i path.
```
asymp(H)
```

## Spesielle kommandoer
###  Stepinfo
```
stepinfo(H)
-----------------
ans = struct with fields:
         RiseTime: 0.1269
    TransientTime: 1.4116
     SettlingTime: 1.4116
      SettlingMin: 0.8027
      SettlingMax: 1.4432
        Overshoot: 44.3235
       Undershoot: 0
             Peak: 1.4432
         PeakTime: 0.3316
```

### Skrive om funksjon med poler/zeros    (Faktorisere)
```
zpk(M)
--------------------
ans =
 
                 2000 (s+10) (s+0.6494)
  -----------------------------------------------------
  (s+100.4) (s+49.34) (s+0.6265) (s^2 + 1.668s + 4.186)
 
```

### Closed Loop Feedback-funksjon
```
M = feedback(G,1)
step(M)
grid;
```

### s to z-transformation
![[4 - Design av IIR-filtre-2025.03.26 12.44.07.png|550]]

### Endre fra lavpass til høypass
I s-domenet
![[4 - Design av IIR-filtre-2025.03.26 20.34.15.png|550]]

I z-domenet
Står ikke noe i boka



## Regulator



# Interaksjon/konsoll
## Display
```ml
disp(' ')
disp('Med dette programmet kan du loese ligninger skrevet paa uordnet form.')
disp('Eksempel:  (U1-U2)/3.5 + (U1-U3)/8 + U1/5 == 15')
```
## Formatert
For å få svaret printet som double istedetfor brøk med tanke på lesbarhet 
```MATLAB
fprintf('Vm = %0.3f V\n', abs(result));
```

#### Formatting operators
[Displays variable text centered on masked subsystem icon - MATLAB fprintf- MathWorks Nordic](https://se.mathworks.com/help/simulink/slref/fprintf.html)
![[Matlab-3.png]]

| Value Type            | Conversion   | Details                                                                                                                                 |
| --------------------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| Integer, signed       | `%d` or `%i` | Base 10                                                                                                                                 |
| Integer, unsigned     | `%u`         | Base 10                                                                                                                                 |
|                       | `%o`         | Base 8 (octal)                                                                                                                          |
|                       | `%x`         | Base 16 (hexadecimal), lowercase letters `a`–`f`                                                                                        |
|                       | `%X`         | Same as `%x`, uppercase letters `A`–`F`                                                                                                 |
| Floating-point number | `%f`         | Fixed-point notation (Use a precision operator to specify the number of digits after the decimal point.)                                |
|                       | `%e`         | Exponential notation, such as `3.141593e+00` (Use a precision operator to specify the number of digits after the decimal point.)        |
|                       | `%E`         | Same as `%e`, but uppercase, such as `3.141593E+00` (Use a precision operator to specify the number of digits after the decimal point.) |
|                       | `%g`         | The more compact of `%e` or `%f`, with no trailing zeros (Use a precision operator to specify the number of significant digits.)        |
|                       | `%G`         | The more compact of `%E` or `%f`, with no trailing zeros (Use a precision operator to specify the number of significant digits.)        |
| Characters or strings | `%c`         | Single character                                                                                                                        |
|                       | `%s`         | Character vector or string array. The type of the output text is the same as the type of `formatSpec`.                                  |

#### Snippets
Spenning med vinkel
```MATLAB
fprintf("Vo = %f V med vinkel %f grader", abs(Vo), rad2deg(angle(Vo)))
fprintf("vo(t) = %f * cos(10000t%f)", abs(Vo), rad2deg(angle(Vo)))

>> Vo = 28.118821 V med vinkel -51.330756 grader
>> vo(t) = 28.118821 * cos(10000t-51.330756)
```

Floating number *MED KUN 2 DESIMALER*
```
fprintf("i1 = %.2f A vinkel %.2f grader", abs(i1), rad2deg(angle(i1)))

>> i1 = 4.47 A vinkel 63.43 grader
```
![[Matlab-20240509154004467.jpg]]

Kompleks effekt
```
fprintf("S = %f VA", abs(S))
fprintf("P = %f W", real(S))
fprintf("Q = %f VAR", imag(S))
```

## Input
```
eq1 = input('Skriv ligning nr.1: ');
```




# Strukturer
## For-løkke
```
for k = 1:n
    fprintf('U%s %d%s = %f + %s%f = %f%s%f grader\n',vp,k,rp,u_rect_r(k),'j',u_rect_i(k), u_pol_abs(k),vt,u_pol_arg(k))
end
```



# Nyttige funksjoner
## Kommentarer
```
% KOMMENTAR
```
## Housecleaning
```
clear % Sletter gamle variabler
clc % Sletter skjermen for gamle utregninger
close % Lukker plots?
```


# Snippets og oppgaver
## Utgangspunkt med parallell- og serie-funksjon
```
clc, clear all, close
% parallel fuksjon
p = @(varargin)1/sum(1./[varargin{:}]);
% series funksjon
s = @(varargin)sum([varargin{:}]);
```

## Komplekse verdier
```matlab
fprintf("I = %.2f A vinkel %.2f grader", abs(I), rad2deg(angle(I)))
fprintf("I = %.2f * cos(10000t%.2f)", abs(I), rad2deg(angle(I)))

% Kompleks effekt levert av kilden
% Antar at spenning/strøm oppgitt er RMS-verdier
%Vrms = Vpeak / sqrt(2)
%Irms = Ipeak / sqrt(2)
S = (abs(Vs)^2) / conj(Zp2); % alt 1
S = Vs * conj(I1); % alt 2

fprintf("S = %.2f VA", abs(S))
fprintf("P = %.2f W", real(S))
fprintf("Q = %.2f VAR", imag(S))

% Effektfaktor
effektfaktor = real(S) / abs(S)
```



---

## ELE217 prosjektoppgave 2
noen eksempler på forloops, random, regnestykker og avansert plotting
```
EbN0_dB = -4:1:10
EbN0 = zeros(1,15);
for i = 1:1:15
    EbN0(i) = 10^(EbN0_dB(i)/10);
end
EbN0

theoretical_BER = 0.5 * erfc(sqrt(EbN0))
stoyvarians = 1 ./ (2 * EbN0)

% initialiserer arrays
simulated_BER = zeros(1,15);
Diff = zeros(1,15);

% a
antall_bits = 500000;
for i = 1:length(stoyvarians)
    data_send = ((rand(1,antall_bits) > 0.5) * 2) -1; % Får ut bits på -1 eller 1
    % b
    stoy = randn(1,antall_bits) * sqrt(stoyvarians(i)); % lager gaussisk støy
    data_inn = data_send + stoy; % AWGN-kanalen
    % c
    data_dekodet = sign(data_inn); % dekoder til -1 og 1
    %data_dekodet = (data_dekodet +1) / 2; % dekode til 0 og 1
    % d Summerer antall flippede bits
    simulated_BER(i) = sum(data_dekodet ~= data_send) / antall_bits;
    Diff(i) = simulated_BER(i) - theoretical_BER(i);
end
simulated_BER
Diff

figure;
semilogy(EbN0_dB, simulated_BER, 'bo-', 'LineWidth', 2); hold on;
semilogy(EbN0_dB, theoretical_BER, 'r--', 'LineWidth', 2);
grid on;
title(sprintf('BER for en BPSK overføring med %d bits', antall_bits));
subtitle('Figur 7')
xlabel('E_b/N_0 (dB)');
ylabel('Bit Error Rate (BER)');
legend('Simulert', 'Teoretisk');
```



## 2017 Vår Kont oppg 1
- 
```
clear, clc, close
Vg = 40; Xc = -6.67j; Xl1 = 60j; Xl2 = 20j; R = 10;

Zp = (Xl1 * (R + Xl2)) / (Xl1 + (R + Xl2));
Va = Zp / (Xc + Zp) * Vg;

Vb = Xl2 / (R + Xl2) * Va;

Vo = Va - Vb;
fprintf("Vo = %f V med vinkel %f grader", abs(Vo), rad2deg(angle(Vo)))
fprintf("vo(t) = %f * cos(10000t%f)", abs(Vo), rad2deg(angle(Vo)))

Zth = ((Xl1 + Xl2) * R) / ((Xl1 + Xl2) + R)
Vth = Vo;
fprintf("Vth = %f V med vinkel %f grader", abs(Vth), rad2deg(angle(Vth)))
fprintf("Vth(t) = %f * cos(10000t%f)", abs(Vth), rad2deg(angle(Vth)))

Zl = 10-50i;
Pl = (Vth^2) / (4*Zl)
```
## 2017 Vår Kont oppg 2
```
clear, clc, close

syms V Il s

l1 = Il - V / 5 - (V - 12/s) / (1 / (2*s)) == 0;
l2 = Il == (12/s - V) / (1 + s*0.5);

svar = solve([l1, l2], [V, Il]);

V(s) = simplify(svar.V)
Il(s) = simplify(svar.Il)

V = vpa(ilaplace(V(s)),3)
Il = vpa(ilaplace(Il(s)),3)
```

---

## 2018 Vår oppg 1
- Knutepunktslikninger
- Thevenin med kortslutningsstrøm
- Maksimal effektoverføring
- Kompleks effekt
```
clear, clc

z1 = 10i; z2 = 10; z3 = 5-5i; z4 = 1-2i; vs = 10;

% c
syms v1 v2
l1 = (v1-vs)/z1 + v1/z2 + (v1-v2)/z3 == 0;
l2 = (v2-v1)/z3 + v2/z4 == 0;

svar = solve([l1,l2], [v1, v2]);

v1 = svar.v1;
vth = svar.v2
fprintf("vth = %f V med vinkel %f grader", abs(vth), rad2deg(angle(vth)))
fprintf("vth(t) = %f * cos(20000t%f) V", abs(vth), rad2deg(angle(vth)))

%d
syms v1 i
l1 = (v1-vs)/z1 + v1/z2 + i == 0;
l2 = i == v1/z3;

svar = solve([l1,l2], [v1, i]);

i = vpa(svar.i)
zth = vth/i

%e
zl = conj(zth)
```
## 2018 Vår oppg 2
- Finne krets i frekvensdomenet
- Finne et potensiale
- Bruke grenseverditeoremet
```
clear, clc

syms s v t
V = 15/s; R = 625; C = 25e-9; L = 25e-3; v0 = 0; i0 = 0;

% b
%l1 = (v-V) / R  +  s*C*v  +  v / (s*L)
%svar = solve(l1, v)
%ilaplace(svar)

V(s) = 15 / (s + (s^2) * 15625 * 10e-9 + 25000)

% c
Il(s) = V(s) / (s * L)

% d
v_inf = limit(s * V(s), s, 0)
il_inf = vpa(limit(s * Il(s), s, 0))

% f
il(t) = ilaplace(Il(s))
% Spolen og kondensatoren virker på hverandre og skaper en
% vekselstrømseffekt

```

---

## 2019 Vår oppg 1
- Finne steady state-spenning og -strøm
- Finne kompleks effekt (gjennomsnittlig og reaktiv)
```
clc, clear all, close
Is1 = 6; Vs2 = 2;
R1 = 6; R2 = 8;
Z1 = 4-2j; Z2 = 6+1j;

syms V1 V2 I2
l1 = -Is1 + V1 / R1 + I2 == 0;
l2 = -I2 + V2 / Z2 + (V2-Vs2) / R2 == 0;
l3 = I2 == (V1-V2) / Z1;


svar = solve([l1, l2, l3],[V1, V2, I2])

V1 = svar.V1
V2 = svar.V2

fprintf("V1 = %f V med vinkel %f grader", abs(V1), rad2deg(angle(V1)))
fprintf("v1(t) = %f * cos(10^4t%f)", abs(V1), rad2deg(angle(V1)))

I2 = svar.I2

fprintf("I2 = %f V med vinkel %f grader", abs(I2), rad2deg(angle(I2)))
fprintf("i2(t) = %f * cos(10^4t + %f)", abs(I2), rad2deg(angle(I2)))

Vz1rms = (V1-V2)/sqrt(2);
I2rms = I2/sqrt(2);
S = vpa(Vz1rms * conj(I2rms),3)

fprintf("P2 = %f W", real(S))
fprintf("Q2 = %f VAR", imag(S))
```

## 2019 Vår oppg 2
- Finne uttrykk for spenning/strøm i s-domenet
- Laplacetransformere til tidsdomenet
```
clc, clear all, close
Vs = 12; R1 = 1; L = 0.5; R2 = 5; C = 2;


syms s Ils

l1 = Ils * R1 + Ils * 0.5*s + 1 + Ils * (1/(2*s)) + 10/s == 12/s;

Il(s) = solve(l1, [Ils])

Vc(s) = Il(s) * (1/(2*s) + 10/s)

syms t
il(t) = ilaplace(Il(s))
vc(t) = ilaplace(Vc(s))
```
## 2019 Vår oppg 5
- Transistor
```MATLAB
clc, clear all, close
R1 = 1e4; R2 = R1; Rc = 2e3; Re = 1e3; Rl = 1e3; Vcc = 10; Rs = 100;
Vbe = 0.7; beta = 100;


syms IR1 IR2 IC IE IB
R1 = 10E3; R2 = 10E3; RC = 2E3; RE = 1000;
B = 100; VBE = 0.7; VCC = 10;
EQ1 = VCC -IR1*R1 - IR2*R2 == 0;
EQ2 = VCC - IR1*R1 - VBE - IE*RE == 0;
EQ3 = IB + IC == IE;
EQ4 = IC == B*IB;
EQ5 = IR1 == IR2 + IB;
svar = solve([EQ1,EQ2,EQ3,EQ4,EQ5],[IB,IC,IE,IR1,IR2]);

Ib = double(svar.IB)
Ic = double(svar.IC)
Ie = double(svar.IE)
```


---
## 2020 Vår oppg 1
- Kompleks strøm og spenning
- Kompleks effekt
- Effektfaktor
```MATLAB
clc, clear all, close
% funksjon for resistorer i parallell
p = @(varargin)1/sum(1./[varargin{:}]);
% funksjon for resistorer i serie
s = @(varargin)sum([varargin{:}]);
---
Xl = 80j; R2 = 20; R1 = 10; Xc = -60j; Vs = 40;

Zp1 = p(R2, Xl)
Zs1 = Zp1 + R1
Zp2 = p(Zs1, Xc)

I1 = Vs / Zp2
fprintf("I1 = %.2f A vinkel %.2f grader", abs(I1), rad2deg(angle(I1)))
---
V1 = Vs * Zp1 / Zs1;
fprintf("V1 = %.2f A vinkel %.2f grader", abs(V1), rad2deg(angle(V1)))
---
% Kompleks effekt i Spole
% P (gjennomsnittlig) er null fordi spolen er perfekt reaktiv. 
% Gjør om til RMS-verdier
V1 = V1 / sqrt(2)
S = (abs(V1)^2) / conj(Xl)

fprintf("S = %f VA", abs(S))
fprintf("P = %f W", real(S))
fprintf("Q = %f VAR", imag(S))
---
% Kompleks effekt levert av kilden
%Vs = Vs / sqrt(2)
%I1 = I1 / sqrt(2)
S = (abs(Vs)^2) / conj(Zp2);
S = Vs * conj(I1);

fprintf("S = %f VA", abs(S))
fprintf("P = %f W", real(S))
fprintf("Q = %f VAR", imag(S))
---
% Effektfaktor
effektfaktor = real(S) / abs(S)

```
## 2020 Vår oppg 2
- Transienter
- Laplacetransformasjon
- Invers laplacetransformasjon
```MATLAB
clc, clear all, close

syms s Il Vl Vc
R = 20;
L = 40e-3;
C = 400e-6;

l1 = 0 == Vl + Il*R - Vc;
l2 = Vl == s*L*Il - L * 150e-3;
l3 = Vc == Il / (s*C) - 0.75/s;
svar = solve([l1, l2, l3],[Il, Vl, Vc]);

Il = svar.Il
Vl = svar.Vl
Vc = svar.Vc

% Invers Laplace
syms t
il(t) = ilaplace(Il)
vl(t) = ilaplace(Vl)
vc(t) = ilaplace(Vc)
```


---
## 2021 Vår Kont oppg 1
- Thevenin-ekvivalent
- Kompleks effekt
```MATLAB
clear, clc, close
Vg = 40; Xc = -6.67j; Xl1 = 60j; Xl2 = 20j; R = 10;
---
Zp = (Xl1 * (R + Xl2)) / (Xl1 + (R + Xl2));
Va = Zp / (Xc + Zp) * Vg;

Vb = Xl2 / (R + Xl2) * Va;

Vo = Va - Vb;
fprintf("Vo = %f V med vinkel %f grader", abs(Vo), rad2deg(angle(Vo)))
fprintf("vo(t) = %f * cos(10000t%f)", abs(Vo), rad2deg(angle(Vo)))
---
Zth = ((Xl1 + Xl2) * R) / ((Xl1 + Xl2) + R)
Vth = Vo;
fprintf("Vth = %f V med vinkel %f grader", abs(Vth), rad2deg(angle(Vth)))
fprintf("Vth(t) = %f * cos(10000t%f)", abs(Vth), rad2deg(angle(Vth)))
--
Zl = 10-50i;
Pl = (Vth^2) / (4*Zl)
```
## 2021 Vår Kont oppg 2
- Laplace-transformasjon
```MATLAB
clear, clc, close

syms V Il s

l1 = Il - V / 5 - (V - 12/s) / (1 / (2*s)) == 0;
l2 = Il == (12/s - V) / (1 + s*0.5);

svar = solve([l1, l2], [V, Il]);

V(s) = simplify(svar.V)
Il(s) = simplify(svar.Il)
---
V = vpa(ilaplace(V(s)),3)
Il = vpa(ilaplace(Il(s)),3)
```

---
## 2022 Vår Kont oppg 1
- Steady State
- Effektfaktor
```MATLAB
clc, clear all, close
Vs = 5; Zl = 12j; Zc = 8 - 12j;

Is = Vs / ((Zl * Zc) / (Zl + Zc))

fprintf("Is = %f V med vinkel %f grader", abs(Is), rad2deg(angle(Is)))
fprintf("Is(t) = %f * cos(10^4t%f)", abs(Is), rad2deg(angle(Is)))
---
effektfaktor = cos(rad2deg(angle(Is)))

```
## 2022 Vår Kont oppg 2
- Steady State
- Theveninekvivalent i frekvens- og tidsdomenet
```MATLAB
clc, clear all, close

Xl = 60j; Xc = -59.95j;
R1 = 30; R2 = 20; 
V1 = 240*(cosd(53.13) + sind(53.13)*j);
V2 = -96j;

syms Va Isc
l1 = (Va -V1) / Xl + Va/R1 + Va/Xc + (Va+V2)/R2 == 0;
Vth = solve(l1,Va);

fprintf("Vth = %f V med vinkel %f grader", abs(Vth), rad2deg(angle(Vth)))
fprintf("Vth(t) = %f * cos(10^4t%f)", abs(Vth), rad2deg(angle(Vth)))

Isc = V1 / Xl - V2 / R2;
Zth = double(Vth/Isc)
---
R = 50; L = 640e-3; C1 = 640e-6; C2 = 360e-6;
syms s V


eqn1 = 1/s + V/R + V/(s*L) + s*V*C1 + s*V*C2 == 0;
% Løser ligning
V = solve([eqn1], [V])


% V = -1 / (s*(1/R + 1/(s*L) + s*C1 + s*C2))
ilaplace(V)

```

---

## 2022 Høst oppg 2
- Dioder, knutepunkt, finn strømmer
```MATLAB
clc, clear all
syms v
l1 = v/1e3 + (v-10.6) / 5.6e3 + (v-11.3) / 220 == 0;
v = solve(l1, v)
i1 = vpa(v/1e3)
i2 = vpa((10.6-v)/5.6e3)
I3 = vpa((11.3-v)/220)
```

---

## 2022 Høst Kont oppg 2
- Thevenin-ekvivalent av steady-state-krets
```MATLAB
clc, clear all, close
Vs = 120; R = 10; Xl = 8j; Xc = -8j; I = 0.5 * (cosd(60) + 1j * sind(60));

syms V1 V2 Isc
l1 = (V1 - Vs) / R + V1 / Xl + (V1 - V2) / Xc == 0;
l2 = (V2 - V1) / Xc - I == 0;
svar = solve([l1,l2], [V1, V2]);

%V1 = svar.V1
%Vth = double(svar.V2)
Vth = svar.V2;

fprintf("Vth = %f V med vinkel %f grader", abs(Vth), rad2deg(angle(Vth)))
fprintf("Vth(t) = %f * cos(10^4t%f)", abs(Vth), rad2deg(angle(Vth)))

syms V1 Isc
l1 = (V1 - Vs) / R + V1 / Xl + (V1) / Xc == 0;
l2 = Isc == V1 /Xc + I;
svar = solve([l1,l2], [V1, Isc]);

Isc = svar.Isc;

Zth = double(Vth / Isc)
```
## 2022 Høst Kont oppg 3
- Finn uttrykket i s-planet
```MATLAB
clc, clear all, close
syms s I0
V1 = 100; 
Vc = 100/s; C = 10^9 / (125*s); 
R1 = 4e3; R2 = R1;
L = s/2;    

l1 = V1 == I0 * R2 + I0 * L;
svar = solve(l1,[s,I0])

I0 = V1 / (R2 + L)
i0 = ilaplace(I0)
```


---
## 2023 Vår oppg 2
- Steady state-oppgave hvor man reverse-engineerer vinkelfrekvens, kapasitans og induktans
```
clc, clear all
Is = 2*(cosd(30) + sind(30)*1j)

Z1 = 5 + 4j;
Z2 = -9j;

Zt = (Z1*Z2) / (Z1+ Z2)

i1 = Zt/Z1 * Is
fprintf("i1 = %.2f vinkel %.2f A", abs(i1), rad2deg(angle(i1)))

clc, clear all
w = 1000;
V = 80 * (cosd(130) + 1j * sind(130));
I = 20 * (cosd(40) + 1j * sind(40));

Zt = V / I

L = Zt / (w*j)

clc, clear all
Vs = 100; R = 8; Xl = 6j;
Vl = Vs * (Xl / (R+Xl))
fprintf("Vl = %.2f vinkel %.2f V", abs(Vl), rad2deg(angle(Vl)))

```
## 2023 Vår oppg 5
- Transistoroppgave: Forspenning/voltage divider med forenklet metode
- Lastlinjeanalyse
- Småsignalanalyse (forenklet)
- Forsterkning med og uten kondensator på emitter
```
clc, clear all
R1 = 27e3; R2 = 3.9e3; Rc = 3.3e3; Rl = 2.7e3; Rs = 330;
Vcc = 20;
Ie = 2.5e-3;
Beta = 200;

Rth = (R1 * R2)/(R1 + R2)

% Forsøker forenklet metode
Vb = Vcc * R2 / (R1 + R2);
Ve = Vb - 0.7;
Re = Ve / Ie

% Undersøker at beta * Re > 10 * R2
(Beta * Re) / (10 * R2)
disp("divident er større enn divisor, altså er kravet oppfylt")

% Andre verdier
Ib = Ie / (Beta + 1)
Ic = Ie + Ib
Vce = Vcc - Ic*(Rc + Re)

% Lastlinjeanalyse
Icsat = Vcc / (Rc + Re)

% Småsignalparameter
re = 25e-3 / Ie

% Forsterkning med resistans i last og kilde
Avnl = -Rc / re

% sjekk boka side 296 for Zi og Zo
Zut = ((Rc * Rl)/(Rc + Rl));
Avl = -Zut / re

Zi = (Rth * Beta * re)/(Rth + Beta * re);
Avs = Avl * Zi / (Zi + Rs)

% Fjerner kondensator Ce (Emitter gjennom motstander for AC)
Zut = 1 / (1/Rc + 1/Rl + 1/Re) ;
Avl = -Zut / (re + Re)

Zi = (Rth * (Beta * re + Re))/(Rth + (Beta * re + Re));
Avs = Avl * Zi / (Zi + Rs)

```
# PDFer
## Generelt
![[MATLAB generelt.pdf]]

## Komplekse tall
![[MATLAB Komplekse tall med MATLAB.pdf]]

##Laplacetransformering
![[MATLAB Laplace med MATLAB.pdf]]