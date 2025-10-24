# Quartus
## USB
- [GitHub - simon-77/Install-Quartus-and-ModelSim-on-Linux-openSUSE: Tutorial: Installation of Intel Quartus Prime Lite & ModelSim Starter Edition on Linux openSUSE Tumbleweed](https://github.com/simon-77/Install-Quartus-and-ModelSim-on-Linux-openSUSE)
- [Quartus II JTAG Server Error Code 89 - Intel Community](https://community.intel.com/t5/Intel-Quartus-Prime-Software/Quartus-II-JTAG-Server-Error-Code-89/m-p/162221)

## Text editor
[Preferred Text Editor command details to run specific parameters for the editor - Intel Community](https://community.intel.com/t5/Intel-Quartus-Prime-Software/Preferred-Text-Editor-command-details-to-run-specific-parameters/m-p/1402551)
sigasi-plugin i vscode

path:
```
which code
```

## RTL-viewer
1. Kompiler
2. Tools/Netlist Viewers/RTL Viewer

## Programmere/overføre til FPGA
Se [[F2_001 Lag et prosjekt C.pdf]] for instrukser.
Se [[FPGA-de2-115-user-manual.pdf]] for pinout.
Gjerne bruk pinout fra lærer
1. Legg inn pin-assigment
2. Kompiler
3. Gå til Programmer
4. Velg USB-blaster
5. Start



## Simulere i Questa
Emulerer hva som skjer på FPGA-kretsen på PCen. Den fungerer ikke parallellt, men sekvensielt, og kan derfor bruke lang tid på lange simuleringsøkter.

Se [[F3_001 Test av design i questa_B.pdf]] for instruks til hvordan simulere et prosjekt
1. Kompiler/syntetiser programmet
2. Lag testbench: Processing/Start/Start test bench template writer
	1. ``<filnavn>.vht``
3. Start Questa: Tools/Run Simulation Tool/RTL Simulation
	1. Ved feilmeldinger, rett de i Quartus
5. Compile i Qusta: Compile/Compile...
	1. Velg  ``<filnavn>.vht``
6. Åpne ``mux2.vht`` og endre ``init``
	1. Prosessen kjøres gjennom en gang, kronologisk.
7. Kompiler på nytt ???
8. Klikk Simulate/Start Simulation
	1. Velg ``work/<filnavn>_vhd_tst``
9. Åpne Wave: View/Wave|
10. Skriv kommando: ``run 10 us`` (eller et passende tidsrom)

Etter man har gjort endringer:
1. Kompiler på nytt
2. Skriv kommando: `restart`
3. Skriv kommando: `run <tidsrom>`


## Logikk analysator
Signal tap er en komponent på FPGA-kortet.
- Samler inn data om signalene osv. på FPGAen, så man kan analysere det i Quartus.

 Se [[F15_001 Bruksanvisning SignalTap_A2.pdf]].


---

# Troubleshooting
## Top-level-entity
```log
Error (12007): Top-level design entity "Lab2_del1" is undefined
```
Fiks:
- Assignment/Settings
- Top-level entity: `<skriv inn navnet på entity-navnet i koden>`