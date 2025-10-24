Todo:
- [x] Start_pulse_key - kunne sende start via fysisk knapp
- [x] tx_ready til lampe
- [x] Hvordan fungerer egt. reset fra SBI/MCU, den må vel ikke synkroniseres? Aktiv høy?
	- Håndteres av MCU, synkronisering og invertering. Aktiv høy.
- [x] Datablad: Hva er det som defineres som en komponent; hele opplegget liksom, eller kun MCU-komponenten?
	- Kom
- [x] Implementere reset, evt sjekk av FIFO_CNT for å gi error ved skriving
- [x] Fikse Write strobe på start pulse igjen ???
- [ ] Interrupt med knapp?
- [ ] Sette opp interrupt fra HW som poller SW om data kontinuerlig?
- [ ] Implementere generics/konfigurasjon?
- [ ] 
- [ ] Hva er memorymap?
- [ ] Rydde opp i VHDL-kommentarer
- [ ] 

# Protokoll
## RS485
- Bus kontra en til en
- Tre ledere for common mode rejection
- Logisk en er spenningsdifferansen mellom de to lederne

![[Prosjektoppgave-2025.02.19 08.34.06.png]]

## DMX
Kan lastes ned fra [ESTA sine nettsider](http://tsp.esta.org/tsp/documents/published_docs.php)

![[Prosjektoppgave-2025.02.19 08.56.58.png|550]]

Asynchronous frame with one byte of data, a start bit, and two stop bits. 11-bit word.  
- Data value: 0-255
- A sequence of words called a packet is sent to control multiple lights. 
- In idle mode, the line is high. A packet begins with a break, a low state that occurs for at least 88 µs. 
- After the break, a mark after break (MAB) is transmitted. This is an 8 µs high pulse. Next is a start code (SC). This is a frame with a zero value to signal the beginning of a packet. A zero indicates dimmers.
- No address is transmitted. Each light is assigned an address (1 to 512) **but that address is determined by the dimming code position in the packet**. Frame 1 after the start code is for dimmer 1, frame 2 after the start code is for dimmer 2, and so on. The light dimmer circuits count the frames to determine if the code is for them. The sequence value after the start code determines the target dimmer. 
	- Er en pakke informasjon om ALLE 512 adresser?
	- The DMX signal repeats all 512 intensities as fast as 44 times per second
- The packet ends with a break.  


Frenzel, Louis E.. _Handbook of Serial Communications Interfaces : A Comprehensive Compendium of Serial Digital Input/Output (I/o) Standards_, Elsevier Science & Technology, 2015. _ProQuest Ebook Central_, http://ebookcentral.proquest.com/lib/hogskbergen-ebooks/detail.action?docID=2189944.  

- A DMX512 universe is made up of 512 channels, with each channel containing a value between 0 and 255
- Each slave device in the chain can "look at" a different set of channels in order to be controlled by the master controller. 
- Many of the more modern control desks instead of featuring multiple OUT connectors have an [unshielded twisted pair](https://en.wikipedia.org/wiki/Unshielded_twisted_pair "Unshielded twisted pair") connector (such as [Cat 5](https://en.wikipedia.org/wiki/Cat_5 "Cat 5"), [Cat 5e](https://en.wikipedia.org/wiki/Cat_5e "Cat 5e") or [Cat 6](https://en.wikipedia.org/wiki/Cat_6 "Cat 6")). Such cables and systems can control up to 524,288 universes of DMX512 (32,768 subnets × 16 universes per subnet)[[5]](https://en.wikipedia.org/wiki/DMX512#cite_note-5) using the [Art-Net](https://en.wikipedia.org/wiki/Art-Net "Art-Net") IV protocol, or 65,536 universes using the sACN protocol, and the existing Ethernet in buildings.

### Pakker
En Pakke er en lang rekke med Frames/Slots.
- En pakke starter med break, så slot med start-code, deretter opptil 512 slots med data.
- Altså totalt 513 slots.


- The data format is fixed at one start bit, eight data bits (least significant first[[11]](https://en.wikipedia.org/wiki/DMX512#cite_note-11)), two stop bits and no [parity](https://en.wikipedia.org/wiki/Parity_bit "Parity bit")
- Each frame consists of:
	- Break condition (lav)
	- Mark-After-Break (kort høy)
	- Slot 0, containing the one-byte Start Code
	- Up to 512 slots of channel data, each containing one byte

En 
![[Prosjektoppgave-2025.03.21 19.49.35.png]]
*By Jonathan Laventhol at en.wikipedia, CC BY-SA 3.0, https://commons.wikimedia.org/w/index.php?curid=20344039*

#### Struktur og Adresser
Fra [Wikipedia](https://en.wikipedia.org/wiki/DMX512#Protocol):
	The start of a packet is signified by a [break](https://en.wikipedia.org/wiki/UART#Break_condition "UART") followed by a "mark" (a logical one), known as the "Mark After Break" (MAB). The break, which signals the end of one packet and the start of another, causes receivers to start reception and also serves as a frame (position reference) for data bytes within the packet. [Framed](https://en.wikipedia.org/wiki/Frame_\(networking\) "Frame (networking)") data bytes are known as _slots_. Following the break, up to 513 slots are sent.

Det jeg kjenner som **Adresser** kalles også **Framed Data Bytes** og **Slots**.

#### Start Code
Fra [Wikipedia](https://en.wikipedia.org/wiki/DMX512#Protocol):
	**The first slot is reserved for a "Start Code" that specifies the type of data in the packet. A start code of 0x00 ([hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal "Hexadecimal") zero) is the standard value** used for all DMX512 compatible devices, which includes most lighting fixtures and dimmers. Other start codes are used for Text packets (0x17), System Information Packets (0xCF), for the [RDM](https://en.wikipedia.org/wiki/RDM_\(lighting\) "RDM (lighting)") extension to DMX (0xCC), and various proprietary systems. ESTA maintains a database of alternate start codes.[[12]](https://en.wikipedia.org/wiki/DMX512#cite_note-12)

## Timing
Fra [Wikipedia](https://en.wikipedia.org/wiki/DMX512#Timing)
	Maximum times are not specified because as long as a packet is sent at least once per second, the BREAK, MAB, inter-slot time, and the mark between the last slot of the packet and the break (MBB) can be as long as desired.
	A maximum-sized packet, which has 512 _channels_ (slots following the start code), takes approximately 23 ms to send, corresponding to a maximum [refresh rate](https://en.wikipedia.org/wiki/Refresh_rate "Refresh rate") of about 44 Hz. For higher refresh rates, packets having fewer than 512 channels can be sent.


|                    | Min Break (μs) | Min MAB (μs) |     |
| ------------------ | -------------- | ------------ | --- |
| Transmitted        | 92             | 12           |     |
| Receiver recognize | 88             | 8            |     |


Hvis jeg velger 4 µs som enable-klokke så burde det fungere som grunnenhet for DMX-overføring.
	- Da blir
		- Break = 100 µs = 25 * 4 µs
		- Mark After Break = 3 * 4 µs
		- Databit = 1 * 4 µs
		- Frame = 11 * 4 µs = 44 µs
		- Pakke = 513 frames + break + mark after break = 

Konklusjon:

| Del av pakke       | Lengde      | Antall enables |
| ------------------ | ----------- | -------------- |
| Startbit ("break") | ca. 100 µs  | 20 slag        |
| Mark After Break   | 12 µs       | 3 slag         |
| Data-/stopbits     | 4 µs        | 1 slag         |
|                    |             |                |
| *Frame*            | *44 µs*     | *11 slag*      |
| *Pakke*            | *22 684 µs* | *5671 slag*    |
|                    |             |                |
| målt               | 22,727 kHz  |                |
| bereggnet          | 22 kHz      |                |
|                    |             |                |
| Baudrate           |             |                |

$$
\text{Baudrate} = \frac{1}{\frac{\text{CLOCK\_50}}{\text{baud\_rate\_divider}}} = \frac{2200 \text{ klokkeslag}}{50.000.000 \text{ klokkeslag}}
$$


400 ns for å lese/skrive fra NIOS

# HW Kretsutførelse

## Research
Trenger +-X volt ut fra +5V rail eller signal. Kan bruke 
- CMOS-som en halv H-bridge
- en OPAMP koblet til 0V og +5V
	- negativ-terminal koblet til signal
	- pluss-terminal koblet til bias-nettverk som gir +2.5V. Da vil den gå i metning med en gang, og dermed gi +-2.5V.
- MAX485EPA+ transceiver [Title Unavailable \| Site Unreachable](https://no.farnell.com/analog-devices/max485epa/rs422-rs485-txrx-2-5mbps-5-25v/dp/2511738?CMP=e14c-legacy-e14c-direct-ugc&COM=e14c-legacy-&osetc=e14c-direct)


- [DMX Explained; DMX512 and RS-485 Protocol Detail for Lighting Applications - element14 Community](https://community.element14.com/technologies/open-source-hardware/b/blog/posts/dmx-explained-dmx512-and-rs-485-protocol-detail-for-lighting-applications)
- [Introduction to DMX - SparkFun Learn](https://learn.sparkfun.com/tutorials/introduction-to-dmx/all)

- [RS-485 - Wikipedia](https://en.wikipedia.org/wiki/RS-485)
- [DMX512 - Wikipedia](https://en.wikipedia.org/wiki/DMX512)




Termineres med 120ohm mellom datalinjene
[DMX512 Termination](http://www.dmx512.com/web/light/dmx512/term.htm)

## Jording / signal common
RS485 og RS422 krever ikke eksplisitt jording, men DMX krever det (?).

Fra [Wikipedia](https://en.wikipedia.org/wiki/DMX512#Electrical):
	The E1.11 (DMX512 2004) electrical specification addresses the connection of DMX512 signal common to earth ground. **Specifically, the standard recommends that transmitter ports (DMX512 controller OUT port) have a low impedance connection between signal common and ground; such ports are referred to as _grounded_. It is further recommended that receivers have a high impedance connection between signal common and ground; such ports are referred to as _isolated_.**
	The standard also allows for isolated transmitter ports and non-isolated receivers. It also recommends that systems ground the signal common at only one point, in order to avoid the formation of disruptive [ground loops](https://en.wikipedia.org/wiki/Ground_loop_\(electricity\) "Ground loop (electricity)").
	Grounded receivers that have a hard connection between signal common and ground are permitted but their use is strongly discouraged. Several possible grounding configurations that are commonly used with EIA485 are specifically disallowed by E1.11.

## Utførelse
Bruker et MAX485-brett jeg hadde liggende.

![[Prosjektoppgave-2025.03.19 09.22.26.png|550]]


- VCC og GND kobles til GPIO pinner på linje seks fra toppen. 5V på venstre, GND på høyre
- RO: brukes ikke
- RE_n
	- Settes positiv for å sende (?)
- 
	- GPIO[2]
- DE, Driver Enable
	- Settes positiv for å sende
	- GPIO[1]
- DI, Driver Input
	- Her sendes signalet
	- GPIO[0]
- A: noninverting driver output
- B: inverting driver output
- FPGA sender ut 3.3v



# HW VHDL utførelse
Bygger videre på semesteroppgave høst 2024 om å lage en UART (RS232).
Tenker å endre:
- Enable-klokke
	- Hvis jeg velger 4 eller 5 µs som basisklokke så burde det fungere som grunnenhet for DMX-overføring.
	- Da blir
		- Break = 100 µs = 20 * 5 µs
		- Mark After Break = 
- Tilstandsmaskinen for sending
	- Aktivt høy ut
	- Endre pakkestrukturen
		- Break-condition
		- Mark-after-break - er vel det samme som start-bittet i RS232
		- Første byte er startcode
		- Loope over resterende 511 pakker
	- LSB først
- Fjerne alt unødvendig


## Grensesnitt SW <-> HW
> [!NOTE]- Hvordan overføre informasjon fra SW til HW?
> 
> I HW skjer "alt" parallelt og er derfor lynraskt (kun en propogation delay), mens i SW skjer alt sekvensielt og bruker tid.
> - HW er "dyrt"
> - SW skriving til registre er langsomt
> 
> Jeg ser to ulike utførelser for hvordan man skal overføre verdi til en frame, avhengig av hvor mye man ønsker at SW gjør:
> 1. SW skriver verdi for hver enkelt frame
> 	- + Sparer HW register ved at man kun trenger et 8-bits register.
> 	- + Kan være mer "snappy" ved at den nyeste informasjonen taes med for hver neste frame.
> 	- - Skrive-delay mellom frames: Hvordan laste ut verdi uten at skriving til register tar for lang tid mellom hver frame?
> 	- SW kan skrive med en gang man er ferdig med å laste; bruke et load-ready-flagg?
> 2. SW skriver alle 512 verdier til et register, og så skiller HW frames fra hverandre
> 	- + Burde ikke være noe problem med delay mellom frames.
> 	- - Dyrt i HW med et 512 byte register, 0.5 KB.
> 
> 
> 3. Kan gjøre som I2C-coren: La SW skrive 4 byte/32 bit om gangen i en for-loop, og så lagrer/viderebehandler HW verdiene med en gang den merker at det er skrevet.
> 	- Hvordan lage en trigger i VHDL? Hva hvis det skrives 0
> 	- Evt. at SW skriver rett til en egendefinert RAM. Idk hvordan det utføres.
> 

#### Start_pulse
~~Start_pulse fra SW er et slags start_pulse continous.~~ 
~~En prosess i dmx_master_HW tar seg av å kun sende en puls når tx_ready, sammen med logikk for å håndtere start_pulse_key.~~

## Grensesnitt FPGA <-> omverdenen
Innganger:
- RESET_KEY - KEY[0]
- START_PULSE_KEY - KEY[1]

Utganger
- DI, Driver Input - GPIO[0]
- DE, Driver Enable - GPIO[1]
- TX_READY_OUT - LEDG[0]
- FIFO_EMPTY_OUT - LEDG[1]
- FIFO_FULL_OUT - LEDG[2]
- HEARTBEAT - LEDR[0]



# SW C utførelse
Deler opp filene i (også i .c og .h)
- Driver-filer for OS på PC til SW på NIOS
- Logikk som kjører i SW på NIOS
- Driver-filer for SW på NIOS til HW 


## Interrupt
[Nios II Exception Handling](https://johnloomis.org/NiosII/interrupts/exception2.html)
```c
// filepath: /home/kristoffer/Nextcloud/02_Programmering/VHDL_Quartusfiles/ELE113/Semesteroppgave_DMX/dmx_master/software/dmx_master_sw/dmx_app.c
#include <stdio.h>
#include <fcntl.h>
#include <unistd.h>

int char_pending(void) {
    int flags = fcntl(STDIN_FILENO, F_GETFL);
    fcntl(STDIN_FILENO, F_SETFL, flags | O_NONBLOCK);

    int c = getchar();

    if (c != EOF) {
        // Put it back so normal scanning can still read it
        ungetc(c, stdin);
        // Restore flags
        fcntl(STDIN_FILENO, F_SETFL, flags);
        return 1; // A character is pending
    }

    // Restore flags
    fcntl(STDIN_FILENO, F_SETFL, flags);
    return 0; // No character pending
}

// Example usage in your code:
void mode_manual()
{
    int input;
    while (1)
    {
        // Check if user pressed something:
        if (char_pending()) {
            int ch = getchar();
            // If 'q' pressed, break to menu:
            if (ch == 'q' || ch == 'Q')
                break;
            else
                ungetc(ch, stdin); // Put back if you didn't handle it
        }

        input = scan_int("Fyll inn verdi som skal sendes til alle adresser:", 0, 255);
        for (int addr = 0; addr < 129; addr++) {
            write_data((input << 24) | (input << 16) | (input << 8) | input);
        }
        printf("TRYKK ENTER FOR Å SENDE (eller 'q' for meny)\n");
        scan_enter();
        write_start_pulse();
    }
}
```


# Scope
UART: LSB, 250kb/s
Trigger: Edge falling eller Pulse Width low >90µs



# Muntlig eksamens notater
Gjennomgang av prosjekt
1. Introduksjon og vise fram i praksis
2. Fortelle om DMX
3. Fortelle om hvordan jeg løste oppgaven
	1. Pakker/konstruksjon og Timing
	2. Overføring fra SW til HW
	3. Vise registerkartet
4. Se nærmere på koden
	1. Modifikasjoner til UART
	2. Forklare registeret og FIFOet
	3. Software driver og applikasjon
5. Fortelle om testingen
	1. Generering av tilfeldige data ved bruk av system-tidspunkt i sekunder
	2. UVVM for å skrive SBI
	3. UVVM for å motta UART
	4. Tilpasning med BREAK-tilstanden
6. Hva jeg gjerne skulle gjort
	1. Puttet start_pulse på egen linje - hadde egentlig gjort, men gjorde om av dårlige grunner
	2. Lese nåværende innstillinger fra HW
	3. Legge inn flere sjekker, spesielt ift. FIFO
	4. Innterrupts