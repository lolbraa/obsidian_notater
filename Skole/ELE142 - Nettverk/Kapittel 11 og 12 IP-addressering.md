#Nettverk 
Det er vanskelig å få til parallell trafikk i et nettverk.
- I et **WLAN** må alle parter vente på at en pakke er sendt/mottatt før en ny kan sendes. Det er derfor om og med å fordele dette utover.
- I et **LAN** snakker "alle med alle" og må derfor vente på tur. Det er derfor viktig med subnetting (skille LAN i mindre biter) og unicast - en-til-en-kommunikasjon.
- Når en **broadcast** skjer på et subnet blir pakken sendt til alle klienter.

# IPv4
2^8 \* 4 plasser = 32-bit addresse, (0.0.0.0 til 255.255.255.255)

## Subnet Mask
IPv4 er delt i to deler, **Network- og Host-portion**.
- Subnet Mask bestemmer hvilke deler som er host-portion.
- Prefix `/n` er antall ledende enere.
- Oktett grensen er /8, /16 og /24
![[Kapittel 11 og 12 IP-addressering-1.png]]

| **Subnet Mask** | **32-bit Address**                  | **Prefix Length** |
| --------------- | ----------------------------------- | ----------------- |
| 255.0.0.0       | 11111111.00000000.00000000.00000000 | /8                |
| 255.255.0.0     | 11111111.11111111.00000000.00000000 | /16               |
| 255.255.255.0   | 11111111.11111111.11111111.00000000 | /24               |
| 255.255.255.128 | 11111111.11111111.11111111.10000000 | /25               |
| 255.255.255.192 | 11111111.11111111.11111111.11000000 | /26               |
| 255.255.255.224 | 11111111.11111111.11111111.11100000 | /27               |
| 255.255.255.240 | 11111111.11111111.11111111.11110000 | /28               |
| 255.255.255.248 | 11111111.11111111.11111111.11111000 | /29               |
| 255.255.255.252 | 11111111.11111111.11111111.11111100 | /30               |


Subnette et /24-nettverk
![[Kapittel 11 og 12 IP-addressering-2.png]]
## Network Address
![[Kapittel 11 og 12 IP-addressering-3.png]]
![[Kapittel 11 og 12 IP-addressering-4.png]]

## Protokoller
### Unicast
En til en
> Unicast transmission refers to one device sending a message to one other device in one-to-one communications.
>A unicast packet has a destination IP address that is a unicast address which goes to a single recipient. A source IP address can only be a unicast address, because the packet can only originate from a single source. This is regardless of whether the destination IP address is a unicast, broadcast or multicast.
### Broadcast
Sender man en pakke til broadcast-addressen blir pakken sendt til alle på nettverket. Enten regnes ut basert på subnetmask, eller 255.255.255.255 (fungerer på alle nettverk).
Broadcast går til alle på nettverket, frem til nærmeste ruter.
Påvirker ytelsen drastisk (over 100 klienter).
**IP med alle enere er *Brodcast address***

### Multicast
Trafikk går til alle som har meldt seg på
> Multicast transmission reduces traffic by allowing a host to send a single packet to a selected set of hosts that subscribe to a multicast group.
> A multicast packet is a packet with a destination IP address that is a multicast address. IPv4 has reserved the 224.0.0.0 to 239.255.255.255 addresses as a multicast range.
> Each multicast group is represented by a single IPv4 multicast destination address. When an IPv4 host subscribes to a multicast group, the host processes packets addressed to this multicast address, and packets addressed to its uniquely allocated unicast address.

## Offentlig og private addresser
Public IPv4 addresses are addresses which are globally routed over the internet. Public IPv4 addresses must be unique.
Both IPv4 and IPv6 addresses are managed by the Internet Assigned Numbers Authority (IANA). The IANA manages and allocates blocks of IP addresses to the Regional Internet Registries (RIRs). The five RIRs are shown in the figure.
RIRs are responsible for allocating IP addresses to ISPs who provide IPv4 address blocks to organizations and smaller ISPs. Organizations can also get their addresses directly from an RIR (subject to the policies of that RIR).

| **Network Address and Prefix** | **RFC 1918 Private Address Range** |
| ------------------------------ | ---------------------------------- |
| 10.0.0.0/8                     | 10.0.0.0 - 10.255.255.255          |
| 172.16.0.0/12                  | 172.16.0.0 - 172.31.255.255        |
| 192.168.0.0/16                 | 192.168.0.0 - 192.168.255.255      |
### Network Address Translation (NAT)
NAT is used to translate between private IPv4 and public IPv4 addresses. 
>This is usually done on the router that connects the internal network to the ISP network. Private IPv4 addresses in the organization’s intranet will be translated to public IPv4 addresses before routing to the internet.

## Spesielle addresser
There are certain addresses, such as the network address and broadcast address, that cannot be assigned to hosts. There are also special addresses that can be assigned to hosts, but with restrictions on how those hosts can interact within the network.
### **Loopback addresses**
Loopback addresses (127.0.0.0 /8 or 127.0.0.1 to 127.255.255.254) are more commonly identified as only 127.0.0.1, these are special addresses used by a host to direct traffic to itself. For example, it can be used on a host to test if the TCP/IP configuration is operational, as shown in the figure. Notice how the 127.0.0.1 loopback address replies to the **ping** command. Also note how any address within this block will loop back to the local host, which is shown with the second **ping** in the figure.
### **Link-Local addresses**
Link-local addresses (169.254.0.0 /16 or 169.254.0.1 to 169.254.255.254) are more commonly known as the Automatic Private IP Addressing (APIPA) addresses or self-assigned addresses. They are used by a Windows DHCP client to self-configure in the event that there are no DHCP servers available. Link-local addresses can be used in a peer-to-peer connection but are not commonly used for this purpose.



---
# IPv6
128-bit.
Skriver heksadesimale tall (ikke case-sensitive) skilt med kolon.
Trenger ikke subnet mask.
> Dropper leading zeros.
> Kan komprimere ETT felt med kun kolon til dobbel-kolon.
![[Kapittel 11 og 12 IP-addressering-5.png]]
	![[Pasted image 20240403092943.png]]


## Protokoller
### Unicast
Har en LLA (?) lokal (nesten som mac) og en GUA global (?).
Unik interface på en enhet som bruker IPv6.
>An IPv6 unicast address uniquely identifies an interface on an IPv6-enabled device.

#### Global Unicast Address(GUA)
Globalt unik - fungerer ut mot WAN.
Foreløpig brukes kun globale adresser som har de tre første bits satt til 001 (se figur).
Dette fører til at alle GUA adresser begynner med 2 eller 3 (se figur). Dette er ca. 1/8 av tilgjengelige IPv6 adresser.
![[Kapittel 11 og 12 IP-addressering-6.png]]
Global Routing Prefix: Prefix eller nettverksdel av addressen som deles ut sentralt.
Subnet ID: Organisasjon kan dele opp nettverket sitt i subnets.
Interface ID: IPv6-ekvivalent til IPv4 host-addresse. Identifiserer en spesifikk enhet.
#### Link-local addresse (LLA)
Kreves på alle IPv6-enheter og brukes for å kommunisere med enheter på samme link.
Kan ikke rutes og kun på aktuell link.
- En IPv6 link-local address lar enheter kommunisere med andre enheter på samme link.
- Pakker med source/destination satt til en LLA kan ikke rutes videre.
- Hvis en LLA ikke konfigureres manuelt på en interface, vil det opprettes en automatisk.
- IPv6 LLAer er i fe80::/10 område
![[Kapittel 11 og 12 IP-addressering-7.png]]
### Anycast
Byttet broadcast til en smartere modell.
>An IPv6 anycast address is any IPv6 unicast address that can be assigned to multiple devices. A packet sent to an anycast address is routed to the nearest device having that address. Anycast addresses are beyond the scope of this course.
### Multicast
Trafikk går til alle som har meldt seg på.
>An IPv6 multicast address is used to send a single IPv6 packet to multiple destinations.
Unlike IPv4, IPv6 does not have a broadcast address. However, there is an IPv6 all-nodes multicast address that essentially gives the same result.

## Overgangsordninger
- Dual stack: Kjører begge samtidig
- Tunneling: Kjører IPv6 innkapslet over et IPv4 nettverk
- Translation (NAT64): Lager en tabell og «oversetter» mellom v6 og v4
![[Kapittel 11 og 12 IP-addressering-8.png]]
## Subnetting
IPv6 er designet med tanke på subnetting fra grunnen av. Et eget subnet felt i IPv6 GUA brukes for å lage subnets.
![[Kapittel 11 og 12 IP-addressering-9.png]]
- Subnetting av 2001:db8:acad::/48 Global Routing Prefix adresse med 16 bit subnet ID.
- Tillater 65.536 /64 subnets.
- Global Routing Prefix (første 48 bit) er fells for alle sammen.
- Bare subnet ID hexteten økes for hvert subnet.