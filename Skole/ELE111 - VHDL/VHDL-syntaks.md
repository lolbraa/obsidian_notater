Program: Intel Quartus med Questa for simulering
systemklokke på 20ns

Instrukser til [[Quartus]]

# VHDL Syntaks
## Anatomi
`.vhd`-filer er programkoden.
`.vht`-filer er kode som kjøres under simulering.

## Datatyper
### Constant
Tildeles verdi en gang ved deklarasjon
```VHDL
architecture RTL of constant_eksempel is
	constant hundre : integer := 100;
	signal tall : integer range 0 to hundre;
	
	constant CLK_period : time := 100 ns;
	
	constant busWidth : integer := 16;
	signal data_bus : std_logic_vector(busWidth - 1 downto 0) ;
begin
...
```

### Integer
heiltal med eit bestemt talområde
- Angi talområde med range.
- Gir feilmelding ved overflow
- Kan brukes til matematikk (det kan ikke std_logic_vector)
- Kan ikke kobles til pinner (bruk std_logic/-vector)
	- Bør ikke brukes som port i entity

Må inkludera biblioteket numeric_std

```VHDL
use ieee.numeric_std.all;
...
signal K : integer range 0 to 15;
signal L : integer range -16 to 15;
```

### Unsigned/signed
Signed /unsigned
- Kan utføra matematikk på sigend / unsigned, altså `+-*`
- Full kontroll på antall bit
```VHDL
signal positivt : unsigned(3 downto 0);
signal fortegnstall : signed(3 downto 0);
```
- Ser ut som binærtall i koden
	- positivt <= "1001"; -- 9
	- fortegnstall <= "1001"; -- -7
- Gir Wrap-around ved overflow.
	- Ingen feilmelding eller warning.
	- Enklare design av tellere.
- Kan ha metaverdier som 'X' og 'U - Feilsøking lettare

### Array
1. Definere en egen datatype i starten av architecture med eget navn, lengde og innholds-datatype.
2. Deklarere et signal av den typen.
3. Tildele verdi med `:=`
```VHDL

```
#### Enumerated array?

### Variabler (internt i prosesser)
Variabler 
- kan kun brukes i prosesser
- kan kun skrives/leses i prosesser (?)
- oppdateres med en gang i en sekvensiell prosess, der hvor signaler ikke får tildelt verdi før prosessen er ferdig. 
	- Variabler har fordel ved å kunne brukes med en gang på neste linje for operasjoner, feks en if-statement
- brukes sjeldent, evt. kun for å holde midlertidige verdier som feks. å telle 


```VHDL
    p_vipper: process(clk)
        variable internal_register : std_logic;
    begin
        if rising_edge(clk) then
            internal_register := A and B;
            Y <= internal_register or C;
        end if;
    end process p_vipper;
    
```

## Konvertering mellom datatyper
Bruker `to_unsigned` til og fra Integer.
Bruker `unsigned` til og fra std_logic_vector (?)..

1. Konverter std_logic_vector til signed eller unsigend
	- unsigned og signed er std_logic_vector som er tolka som binærtal
		- Representerer talverdi
	- funksjonar:
		- signed();
		- unsigned();
2. konverter signed eller unsigned til integer
	- funksjon: to_integer()

```VHDL
library ieee;
use ieee.std_logic_1164.all;
use ieee.numeric_std.all;
	entity hallo_tabell is
	port(
	SW : in std_logic_vector(2 downto 0);
	HEX0 : out std_logic_vector(6 downto 0)
	);
end entity hallo_tabell;

architecture RTL of hallo_tabell is
	signal adresse : std_logic_vector(2 downto 0);
	
	type tabell is array (0 to 7) of std_logic_vector(6 downto 0);
	constant ROM : tabell := ("0001001","0001000","1000111",
	"1000111","1000000","1111111","1111111","11111111");
begin
	adresse <= SW(2 downto 0);
	HEX0 <= ROM(to_integer(unsigned(adresse)));
end architecture RTL;
```

3. konverter integer til signed eller unsigned
	- Må angi antall bit i sigend, unsigned
```VHDL
to_signed(tall, bit)
to_unsigned(tall.bit)
```

4. konverter signed eller unsigned til std_logic_vector
	- funksjon: std_logic_vector();
![[image.4SWTT2.png|300]]

> [!NOTE]- Code Snippet
> ```VHDL fold
> signal UnsCnt : unsigned(7 downto 0) := (others => '0');
> signal SigCnt : signed(7 downto 0) := (others => '0');
> 
> signal Uns4 : signed(3 downto 0) := "1000";
> signal Sig4: unsigned(3 downto 0) := "1000";
> 
> signal Uns8: signed(7 downto 0) := (others => '0');
> signal Sig8: unsigned(7 downto 0) := (others => '0');
> 
> signal Int4: integer range 0 to 15 := 0;
> ```
> ---
> ```VHDL
> entity konvertering is
>     port(
>         SW : in std_logic_vector(17 downto 0);
>         LEDG : out std_logic_vector(7 downto 0)
>     );
> end entity konvertering;
> 
> architecture RTL of konvertering is
>     signal a,b :integer range 0 to 15;
>     signal c : integer range 0 to 255;
>     signal b_slv : std_logic_vector(3 downto 0);
>     signal c_slv : std_logic_vector(7 downto 0);
> begin
>     a <= to_integer(unsigned(SW(3 downto 0)));
>     b_slv <= SW(7 downto 4);
>     b <= to_integer(unsigned(b_slv));
>     c <= a+b;
>     c_slv <= std_logic_vector(to_unsigned(c,8));
> 
>     LEDG <= c_slv;
> end architecture RTL;
>```

## Signals
En slags intern variabel. Heter signaler for det er faktisk signaler internt i FPGA.


[[Questa  Simulering (Modelsim)]]
## Tildeling
### Sette "a" for "b"
```VHDL
a <= b;
```



## Process (sekvensiell kode)
Se [[F6_000 process B.pdf]]

Asynkron
- Reset er uavhengig av klokke
- Reset verkar med ein gong
Synkron
- Reset blir synkronisert med klokke-signalet
- Reset får effekt først på neste aktive klokk

Rising_edge eller falling (?) er spesiell syntaks som kun skal brukes for ren klokkesignal. Klokkesignalet rutes gjennom FPGA-blokkenes interne klokketraces.
### Oversikt over programkode
```vhdl
architecture RTL of eksempel is
	-- parallell deklarasjonsdel
	-- signal
	-- typer
	-- constant
	-- component
begin
	-- parallell kode,
		--alle kodelinjene blir utført samtidig.
		--rekkefølgen på kodelinjer likegyldig
	process_1 : process ( sensitivitetsliste) is
		-- sekvensiell deklarasjonsdel
			-- variable
			-- constant
			-- typer
	begin
		-- sekvensiell kode
			-- kodelinjene blir utfør ein etter ein.
			-- rekkefølgen på kodelinjer viktig.
	end process process_1;
end architecture RTL;
```

### Variabler
Se [[#Variabler (internt i prosesser)]].

### Sensitivitetslista: 
- Her listes alle signaler som skal føre til at prosessen kjøres…
### Snippets
> [!NOTE]- Code Snippet
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity procestest is
>     port(
>         enable : in std_logic;
>         rst : in std_logic;
>         D : in std_logic;
>         Q : out std_logic
>     )
> end procestest;
> 
> architecture RTL of processtest is
> 
> begin
>     pLatch: process(D,enable)
>         if enable = '1' then
>             Q <= D;
>         end if;
>     end process pLatch;
>     
> end RTL;
> ```
> 

> [!NOTE]- Code Snipper for-løkke
> ```vhdl
> p_d : process is
> constant D_vektor : std_logic_vector := "0111010010";
> 	begin
> 	wait for 3*period/10;
> 	for i in D_vektor'range loop
> 		D <= D_vektor(i);
> 		wait for period/10;
> 	end loop;
> end process p_d;
> ```



## Løkker
En loop kan utføres 0 eller mange ganger
En loop fortsetter til den avsluttes av en av følgende grunner:
- en iterasjonsfølge  er gjennomført
- utførelse av EXIT statement
- utførelse av RETURN statement
- utførelse av NEXT statement som peker på en lable utenfor loopen

Uendelig løkke: Dersom der ikke settes inn betingelser for hvor mange ganger løkken skal 
kjøre, eller når den skal avsluttes, vil den kjøre i det uendelige.



### For-løkke
![[Pasted image 20241028112711.png]]
### While-løkke
Kan ikke brukes til syntetisering/hardware, samt alt annet som ikke har en ende, da det kan føre til "uendelig" hardware.

### Komparator
LIM INN FRA CANVAS
```VHDL

```

## If
Hvis man ikke har en fullstendig if-statement med else, vil man få en asynkron latch - som oftest ikke ønsket.
Eksempelet er med en xor og en mux

> [!NOTE]- Code Snippet
> 
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity if_eksempel is
>     port(
>         a,b,c,d : in std_logic;
>         enable : in std_logic;
>         sel : in std_logic_vector(1 downto 0);
>         x,y : out std_logic
>     );
> end entity if_eksempel;
> 
> architecture RTL of if_eksempel is
> begin
> 
>     xor_2 : process(a,b)
>     begin
>         -- eventuelt følgende, og så kutte else-delen
>         -- y <= '0';
>         if a /= b then
>             y <= '1';
>         else
>             y <= '0';
>         end if;
>     end process xor_2;
> 
>     mux_4 : process(a,b,c,d,sel)
>     begin
>         if enable = '1' then
>             if sel = "00" then
>                 x <= a;
>             elsif sel = "01" then
>                 x <= b;
>             elsif sel = "10" then
>             x <= c;
>             elsif sel = "11" then
>                 x <= d;
>             else
>                 x <= '0';
>             end if;
>         else
>             x <= 'Z';
>         end if;
>     end process mux_4;
> end architecture RTL;
> ```

> [!NOTE]- Code Snippet
> 
> ```VHDL
> architecture RTL of if_eksempel is
>     
> begin
>     
>     mux_4:process(a,b,c,d,sel)
>     begin
>     if enable = '1' then
>         if sel = "00" then
>             x <= a;
>         elsif sel = "01" then
>             x <= b;    
>         elsif sel = "10" then
>             x <= c;
>         elsif sel ="11" then    
>             x <= d;
>         else
>             x <= '0';
>         end if; -- sel
>     else
>         x <= 'Z';
>     end if; -- enable
>     end process;
> 
>     xor_2 : process(a,b)
>     begin
>         y <= '0';
>         if a /= b then
>             y <= '1';
>         --else
>             --y <= '0';
>         end if;
>     end process xor_2;
> 
> 	mux_Num_Sel: process(a,b,sel) is
>    begin
>     if sel < 5 then
>         x <= a;
>     --elsif sel >5 then
>     else
>         x <= b;
>     end if;
>     end process max_Num_Sel;
> 
> end architecture RTL;
> ```



## Latch
```VHDL
	-- Qa lås 
    Qa_latch : process(D, clk)
    begin
        if clk = '1' then
            Qa <= D;
        end if;
    end process;
```

[[VHDL-20240903112402506.jpg|D-flip-flop og D-latch]]
## Vippe
```VHDL
	-- Qb vippe trigga på positiv klokkkeflanke
    Qb_vippe : process(clk)
    begin
        if rising_edge(clk) then
            Qb <= D;
        end if;
    end process;
	
	-- Qc vippe trigga på negativ klokkkeflanke
    Qc_vippe : process(clk)
    begin
        if falling_edge(clk) then
            Qc <= D;
        end if;
    end process;
```




## Components
Når èn entity bruker en annen entity som en del av designet. Modulært, hierarkisk design.
- Componenten er en entity definert tidligere i dokumentet eller i en annen fil.
- Initiater som concurrent statement (parallell)
	- `port map`
		- Kobler porter i komponenten med signal i denne entitien (`a => a`)
		- Kan koble
			- signaler: `x => a`
			- konstant verdi på inn-porten: `y => '1'`
			- matematisk uttrykk med konstanter (ikke signal)
				- `Z => ‘0’ or ‘1’` -- er lov
				- `F => a and b` -- ikkje lov
			- ingen tilkobling: `x => open`

```VHDL
component half_adder is
	port(
		a : in std_logic;
		b : in std_logic;
		sum : out std_logic;
		carry_out : out std_logic
	);
end component half_adder;
half_adder_1: half_adder
	port map(
		a => a,
		b => b,
		sum => sum_1,
		carry_out => carry_1
	);

```
> [!CODE]- I fila half_adder.vhd (som brukes som component i eksempelet over)
> ```VHDL
> entity half_adder is
> 	port(
> 		a : in std_logic;
> 		b : in std_logic;
> 		sum : out std_logic;
> 		carry_out : out std_logic
> 	);
> end entity half_adder;
> ```

### Snippet
> [!NOTE]- Komplett eksempel
> ```VHDL
> architecture struct of full_adder is
> signal sum_1 : std_logic;     -- output signal sum from first half adder 
> signal carry_1 : std_logic;   -- output signal carry out from first half adder 
> signal carry_2 : std_logic;   -- output signal carry out from second half adder 
> 	component half_adder is
> 	port(
> 	a : in std_logic;
> 	b : in std_logic;
> 	sum : out std_logic;
> 	carry_out : out std_logic
> 	);
> 	end component half_adder;
> 	component or2_port is
> 	port(
> 	x : in std_logic;
> 	y : in std_logic;
> 	z : out std_logic
> 	);
> end component or2_port;
> begin
> half_adder_1: half_adder
> 	port map(
> 		a => a,
> 		b => b,
> 		sum => sum_1,
> 		carry_out => carry_1);
> half_adder_2: half_adder
> 	port map(
> 		a => sum_1,
> 		b => carry_in,
> 		sum => sum,
> 		carry_out => carry_2);
> or_port: or2_port
> 	port map(
> 		x => carry_1,
> 		y => carry_2,
> 		z => carry_out);    
> end architecture struct;
> ```
> ![[Pasted image 20240911092236.png]]



---

# Spesielle greier
## 7segment
[VHDL code for Seven-Segment Display on Basys 3 FPGA - FPGA4student.com](https://www.fpga4student.com/2017/09/vhdl-code-for-seven-segment-display.html)

## Minne
Minnet lagres i bytes på 8 bit.
Flere bytes linkes sammen til å lage word. Double word = 2 byte, triple word = 3 bytes, quadruple word = 3 bytes.

SRAM realiseres med transistorer. Raskere, men dyrere. Bruker de derfor som cache. Den kan også realiseres i prosessoren siden det er samme materialer.

DRAM realiseres med en kondensator og en transistor. Billigere, men tregere. Bruker andre komponenter, og er derfor egne brikker.

### Realisering med enkelt minne (?)
M9K er et SRAM minne på 9216-bits (8192 pluss paritetsbit). 
Et krav for å bruke en M9K blokk er at enten må inngangene eller utgangene, eller begge, være synkronisert med klokken. Hvis betingelsene er møtt, lages en 32x8 RAM-modul

> [!NOTE]- ROM_hallo.vhd
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity ROM_hallo is
>     port(
>         adresse : in std_logic_vector(2 downto 0);
>         data_ut : out std_logic_vector(6 downto 0)
>     );
> end entity ROM_hallo;
> 
> architecture RTL of ROM_hallo is
>     type ROM_ARRAY is array(0 to 7) of std_logic_vector(6 downto 0);
>     constant HALLO_ROM : ROM_ARRAY := ("0001001","0001000","1000111",
>         "1000111","1000000","1111111","1111111","1111111");
>     
> begin
>     data_ut <= HALLO_ROM(to_integer(unsigned(adresse)));
> end architecture RTL;
> ```

> [!NOTE]- ram16x8.vhd
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity ram16x8 is
>     port(
>         clk : in std_logic;
>         adresse : in std_logic_vector(3 downto 0);
>         data_inn : in std_logic_vector(7 downto 0);
>         data_ut : out std_logic_vector(7 downto 0);
>         we_n,cs_n,oe_n : in std_logic
>     );
> end entity ram16x8;
> 
> architecture RTL of ram16x8 is
>     type ram_array is array(0 to 15) of std_logic_vector(7 downto 0);
>     signal memory : ram_array;
>     signal adresse_int : integer range 0 to 15;
> 
> begin
>     adresse_int <= to_integer(unsigned(adresse));
> 
>     p_ram: process(clk)
>     begin
>         if rising_edge(clk) then
>             if cs_n = '0' then
>                 if we_n = '0' then
>                     memory(adresse_int) <= data_inn;
>                 end if;
>                 if oe_n = '0' then
>                     data_ut <= memory(adresse_int);
>                 end if;
>             end if;
>         end if;
>     end process;
> 
> end architecture RTL;
> ```

> [!NOTE]- dua_port_ram16x8.vhd
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity ram16x8 is
>     port(
>         clk : in std_logic;
>         write_adresse : in std_logic_vector(3 downto 0);
>         read_adresse : in std_logic_vector(3 downto 0);
>         data_inn : in std_logic_vector(7 downto 0);
>         data_ut : out std_logic_vector(7 downto 0);
>         we_n,cs_n,oe_n : in std_logic
>     );
> end entity ram16x8;
> 
> architecture RTL of ram16x8 is
>     type ram_array is array(0 to 15) of std_logic_vector(7 downto 0);
>     signal memory : ram_array;
>     signal write_adresse_int : integer range 0 to 15;
>     signal read_adresse_int : integer range 0 to 15;
> 
> begin
>     write_adresse_int <= to_integer(unsigned(write_adresse));
>     read_adresse_int <= to_integer(unsigned(read_adresse));
> 
>     p_ram: process(clk)
>     begin
>         if rising_edge(clk) then
>             if cs_n = '0' then
>                 if we_n = '0' then
>                     memory(write_adresse_int) <= data_inn;
>                 end if;
>                 if oe_n = '0' then
>                     data_ut <= memory(read_adresse_int);
>                 end if;
>             end if;
>         end if;
>     end process;
> 
> end architecture RTL;
> ```
> 

### Realisering med Megawizard
Se [[F10_000 Bruksanvisning_ RAM med MegaWizard_B.pdf]].

### Realisering med SRAM-brikke
Timing er viktig, ref. datasheet.
Se [[F11_000 Ekstern SRAM_A.pdf]].
> [!NOTE]- sram.vd
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity sram is
>     port(
>         SW : in std_logic_vector(17 downto 0);
>         KEY : in std_logic_vector(3 downto 0);
>         LEDR : out std_logic_vector(17 downto 0);
>         SRAM_ADDR : out std_logic_vector(19 downto 0);
>         SRAM_DQ : inout std_logic_vector(15 downto 0);
>         SRAM_WE_N : buffer std_logic;
>         SRAM_CE_N : out std_logic;
>         SRAM_OE_N : out std_logic;
>         SRAM_UB_N : out std_logic;
>         SRAM_LB_N : out std_logic;
>         HEX0,HEX1,HEX2,HEX3,HEX4,HEX5,HEX6,HEX7 : out std_logic_vector(6 downto 0)
>     );
> end entity sram;
> 
> architecture RTL of sram is
> 
> component hex_7seg
>     port(
>         siffer : in  std_logic_vector(3 downto 0);
>         HEX    : out std_logic_vector(6 downto 0)
>     );
> end component hex_7seg;
> 
>     signal adr : std_logic_vector(4 downto 0);
>     signal dataInn : std_logic_vector(7 downto 0);
>     signal dataUt : std_logic_vector(7 downto 0);
> begin
>     SRAM_CE_N <= '0';
>     SRAM_OE_N <= '0';
>     SRAM_LB_N <= '0';
>     SRAM_UB_N <= '0';
>     SRAM_WE_N <= SW(17);
> 
>     adr <= SW(15 downto 11);
>     dataInn <= SW(7 downto 0);
> 
> 
>     SRAM_DQ <= "00000000" & dataInn when SRAM_WE_N = '0'
>         else (others => 'Z');
>     dataUt <= SRAM_DQ(7 downto 0);
> 
>     SRAM_ADDR(19 downto 5) <= (others => '0');
>     SRAM_ADDR(4 downto 0) <= adr;
> 
>     dataUtLOW : hex_7seg port map(siffer => dataUt(3 downto 0), HEX => HEX0);
>     dataUtHIGH : hex_7seg port map(siffer => dataUt(7 downto 4), HEX => HEX1);
>     
>     HEX2 <= (others => '1');
>     HEX3 <= (others => '1');
> 
>     dataInnLOW : hex_7seg port map(siffer => dataInn(3 downto 0), HEX => HEX4);
>     dataInnHIGH : hex_7seg port map(siffer => dataInn(7 downto 4), HEX => HEX5);
> 
>     adresseLOW : hex_7seg port map(siffer => adr(3 downto 0), HEX => HEX6);
>     adresseHIGH : hex_7seg port map(siffer => "000" & adr(4), HEX => HEX7);
> 
> 
> end architecture RTL;
> 
> 
> ```

## Teller
> [!NOTE]- teller0_15.vhd
> 
> ```vhdl
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity teller0_15 is
>     port(
>         clk : in std_logic;
>         rst_n : in std_logic;
>         count : out std_logic_vector(3 downto 0)
>     );
> end entity teller0_15;
> 
> 
> 
> architecture RTL of teller0_15 is
>     signal teller : integer range 0 to 15;
>     
> begin
>     p_tell : process (clk) is
>     begin
>         if rising_edge(clk) then
>             if rst_n = '0' then
>                 teller <= 0;
>             else
>                 if teller >= 15 then
>                     teller <= 0;
>                 else
>                     teller <= teller + 1;
>                 end if;
>             end if;
>         end if;
>     end process p_tell;
>     count <= std_logic_vector(to_unsigned(teller,4));
>     
> end architecture RTL;
> 
> ```

> [!NOTE]- teller0_15_opp_ned.vhd
> 
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity teller0_15 is
>     port(
>         clk : in std_logic;
>         rst_n : in std_logic;
>         opp : in std_logic;
>         count : out std_logic_vector(3 downto 0)
>     );
> end entity teller0_15;
> 
> 
> 
> architecture RTL of teller0_15 is
>     signal teller : integer range 0 to 15;
>     
> begin
>     p_tell : process (clk) is
>     begin
>         if rising_edge(clk) then
>             if rst_n = '0' then
>                 teller <= 0;
>             else
>                 if opp = '1' then
>                     if teller >= 15 then
>                         teller <= 0;
>                     else
>                         teller <= teller + 1;
>                     end if;
>                 else
>                     if teller <= 0 then
>                         teller <= 15;
>                     else
>                         teller <= teller - 1;
>                     end if;
>                 end if;
>             end if;
>         end if;
>     end process p_tell;
>     count <= std_logic_vector(to_unsigned(teller,4));
>     
> end architecture RTL;
> 
> ```
> ![[Pasted image 20240924083607.png]]
> 

## Register
> [!NOTE]- register_4_en.vhd
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity register_4_en is
>     port(
>         clk : in std_logic;
>         outEnable : in std_logic;
>         D : in std_logic_vector(3 downto 0);
>         Q : out std_logic_vector(3 downto 0)
>     );
> end entity register_4_en;
> 
> 
> architecture RTL of register_4_en is
>     signal Q_int : std_logic_vector(3 downto 0);
>     
> begin
>     p_register: process(clk) is 
>     begin
>         if rising_edge(clk) then
>             Q_int <= D;
>         end if;
>     end process p_register;
> 
>     Q <= Q_int when outEnable = '1' else (others => 'Z');
>     
> end architecture RTL;
> 
> ```
> ![[VHDL-20240930104804808.jpg|500]]


## Skiftregister
> [!NOTE]- skiftregister.vhd
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity skiftregister is
>     port(
>         clk : in std_logic;
>         rst : in std_logic;
>         SI : in std_logic;
>         SO : out std_logic
>     );
> end entity skiftregister;
> 
> architecture RTL of skiftregister is
>     signal Q : std_logic_vector(3 downto 0);
> begin
>     p_skiftreg: process(clk) is
>     begin
>         if rising_edge(clk) then
>             if rst = '1' then
>                 Q <= (others => '0');
>             else
>                 -- Q(0) <= Q(1);
>                 -- Q(1) <= Q(2);
>                 -- Q(2) <= Q(3);
>                 -- Q(3) <= SI;
>                 -- oneliner under erstatter de fire over
>                 Q <= SI & Q(3 downto 1);
>             end if;
>         end if;
>     end process p_skiftreg;
>     
>     SO <= Q(0);
> 
> end architecture RTL;
> ```
> ![[VHDL-20240930110757877.jpg|500]]

> [!NOTE]- skiftregister.vht
> ```VHDL
> -- Copyright (C) 2024  Intel Corporation. All rights reserved.
> -- Your use of Intel Corporation's design tools, logic functions 
> -- and other software and tools, and any partner logic 
> -- functions, and any output files from any of the foregoing 
> -- (including device programming or simulation files), and any 
> -- associated documentation or information are expressly subject 
> -- to the terms and conditions of the Intel Program License 
> -- Subscription Agreement, the Intel Quartus Prime License Agreement,
> -- the Intel FPGA IP License Agreement, or other applicable license
> -- agreement, including, without limitation, that your use is for
> -- the sole purpose of programming logic devices manufactured by
> -- Intel and sold by Intel or its authorized distributors.  Please
> -- refer to the applicable agreement for further details, at
> -- https://fpgasoftware.intel.com/eula.
> 
> -- ***************************************************************************
> -- This file contains a Vhdl test bench template that is freely editable to   
> -- suit user's needs .Comments are provided in each section to help the user  
> -- fill out necessary details.                                                
> -- ***************************************************************************
> -- Generated on "09/30/2024 11:18:54"
>                                                             
> -- Vhdl Test Bench template for design  :  skiftregister
> -- 
> -- Simulation tool : Questa Intel FPGA (VHDL)
> -- 
> 
> LIBRARY ieee;                                               
> USE ieee.std_logic_1164.all;                                
> 
> ENTITY skiftregister_vhd_tst IS
> END skiftregister_vhd_tst;
> ARCHITECTURE skiftregister_arch OF skiftregister_vhd_tst IS
> -- constants            
> constant periode : time := 20 ns;                                     
> -- signals                                                   
> SIGNAL clk : STD_LOGIC;
> SIGNAL rst : STD_LOGIC;
> SIGNAL SI : STD_LOGIC;
> SIGNAL SO : STD_LOGIC;
> COMPONENT skiftregister
> 	PORT (
> 	clk : IN STD_LOGIC;
> 	rst : IN STD_LOGIC;
> 	SI : IN STD_LOGIC;
> 	SO : OUT STD_LOGIC
> 	);
> END COMPONENT;
> BEGIN
> 	i1 : skiftregister
> 	PORT MAP (
> -- list connections between master ports and signals
> 	clk => clk,
> 	rst => rst,
> 	SI => SI,
> 	SO => SO
> 	);
> init : PROCESS                                               
> -- variable declarations                                     
> BEGIN                                                        
> 	-- code that executes only once  
> 	rst <= '0', '1' after 3*periode, '0' after 5*periode;
> WAIT;                                                       
> END PROCESS init;                                           
> always : PROCESS                                              
> -- optional sensitivity list                                  
> -- (        )                                                 
> -- variable declarations                                      
> BEGIN                                                         
>         -- code executes for every event on sensitivity list  
> 	SI <= '0' after 9*periode, '1' after 11*periode, '0' after 13*periode, '1' after 15*periode; 
> WAIT;                                                        
> END PROCESS always;           
> 
> p_klokke : PROCESS 
> begin
> 	clk <= '0';
> 	loop
> 		wait for periode/2;
> 		clk <= not clk;
> 	end loop;
> 	wait;
> end process p_klokke;
> 
> END skiftregister_arch;
> 
> ```
> ![[VHDL-20240930113630929.jpg|500]]

### Støyfilter
Hvis ikke tre bits mottatt på rad  er identiske, blir ikke den nye biten oppdatert/verifisert.
> [!NOTE]- stoyfilter.vhd
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity stoyfilter is
>     port(
>         clk : in std_logic;
>         rst : in std_logic;
>         SI : in std_logic;
>         SO : out std_logic
>     );
> end entity stoyfilter;
> 
> architecture RTL of stoyfilter is
>     signal Q : std_logic_vector(3 downto 0);
> begin
>     p_filter: process(clk) is
>     begin
>         if rising_edge(clk) then
>             if rst = '1' then
>                 Q <= (others => '0');
>                 SO <= '0';
>             else
>                 Q <= SI & Q(3 downto 1);
>                 if Q(2 downto 0) = "000" then 
>                     SO <= '0';
>                 elsif Q(2 downto 0) = "111" then
>                     SO <= '1';
>                 else
>                     null; -- SO beholder gammel verdi
>                 end if;
>             end if;
>         end if;
>     end process p_filter;
> end architecture RTL;
> 
> ```

> [!NOTE]- stoyfilter.vht
> 
> ```VHDL
> -- Copyright (C) 2024  Intel Corporation. All rights reserved.
> -- Your use of Intel Corporation's design tools, logic functions 
> -- and other software and tools, and any partner logic 
> -- functions, and any output files from any of the foregoing 
> -- (including device programming or simulation files), and any 
> -- associated documentation or information are expressly subject 
> -- to the terms and conditions of the Intel Program License 
> -- Subscription Agreement, the Intel Quartus Prime License Agreement,
> -- the Intel FPGA IP License Agreement, or other applicable license
> -- agreement, including, without limitation, that your use is for
> -- the sole purpose of programming logic devices manufactured by
> -- Intel and sold by Intel or its authorized distributors.  Please
> -- refer to the applicable agreement for further details, at
> -- https://fpgasoftware.intel.com/eula.
> 
> -- ***************************************************************************
> -- This file contains a Vhdl test bench template that is freely editable to   
> -- suit user's needs .Comments are provided in each section to help the user  
> -- fill out necessary details.                                                
> -- ***************************************************************************
> -- Generated on "09/30/2024 11:48:13"
>                                                             
> -- Vhdl Test Bench template for design  :  stoyfilter
> -- 
> -- Simulation tool : Questa Intel FPGA (VHDL)
> -- 
> 
> LIBRARY ieee;                                               
> USE ieee.std_logic_1164.all;                                
> 
> ENTITY stoyfilter_vhd_tst IS
> END stoyfilter_vhd_tst;
> ARCHITECTURE stoyfilter_arch OF stoyfilter_vhd_tst IS
> -- constants             
> constant periode : time := 20 ns;                       
> constant data_in_vektor : std_logic_vector := "000000111000111100001110111100100000010000";                 
> -- signals                                                   
> SIGNAL clk : STD_LOGIC;
> SIGNAL rst : STD_LOGIC;
> SIGNAL SI : STD_LOGIC;
> SIGNAL SO : STD_LOGIC;
> COMPONENT stoyfilter
> 	PORT (
> 	clk : IN STD_LOGIC;
> 	rst : IN STD_LOGIC;
> 	SI : IN STD_LOGIC;
> 	SO : OUT STD_LOGIC
> 	);
> END COMPONENT;
> BEGIN
> 	i1 : stoyfilter
> 	PORT MAP (
> -- list connections between master ports and signals
> 	clk => clk,
> 	rst => rst,
> 	SI => SI,
> 	SO => SO
> 	);
>                       
> 
> p_klokke : PROCESS 
> begin
> 	clk <= '0';
> 	loop
> 		wait for periode/2;
> 		clk <= not clk;
> 	end loop;
> 	wait;
> end process p_klokke;
> 
> init : PROCESS                                               
> -- variable declarations                                     
> BEGIN                                                        
>         -- code that executes only once           
> 	rst <= '1', '0' after 2*periode;         
> WAIT;                                                       
> END PROCESS init;                                           
> always : PROCESS                                              
> -- optional sensitivity list                                  
> -- (        )                                                 
> -- variable declarations                                      
> BEGIN                                                         
>         -- code executes for every event on sensitivity list  
> 		for i in data_in_vektor'range loop
> 			SI <= data_in_vektor(i);
> 			wait until clk = '0';
> 		end loop;
> WAIT;                                                        
> END PROCESS always;     
> 
> END stoyfilter_arch;
> 
> ```


### Ringteller
> [!NOTE]- ringteller.vhd
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity ringteller is
>     port(
>         clk : in std_logic;
>         data_inn : in std_logic_vector(3 downto 0);
>         rst : in std_logic;
>         Q : buffer std_logic_vector(3 downto 0)
>     );
> end entity ringteller;
> 
> architecture RTL of ringteller is
>     
> begin   
>     
>     p_ringteller: process(clk)
>     begin
>         if rising_edge(clk) then
>             if rst = '1' then
>                 Q <= data_inn;
>             else
>                 Q <=  Q(0) & Q(3 downto 1);
>             end if;
>         end if;
>     end process p_ringteller;
> end architecture RTL;
> ```

> [!NOTE]- ringteller.vht
> ```VHDL
> -- Copyright (C) 2024  Intel Corporation. All rights reserved.
> -- Your use of Intel Corporation's design tools, logic functions 
> -- and other software and tools, and any partner logic 
> -- functions, and any output files from any of the foregoing 
> -- (including device programming or simulation files), and any 
> -- associated documentation or information are expressly subject 
> -- to the terms and conditions of the Intel Program License 
> -- Subscription Agreement, the Intel Quartus Prime License Agreement,
> -- the Intel FPGA IP License Agreement, or other applicable license
> -- agreement, including, without limitation, that your use is for
> -- the sole purpose of programming logic devices manufactured by
> -- Intel and sold by Intel or its authorized distributors.  Please
> -- refer to the applicable agreement for further details, at
> -- https://fpgasoftware.intel.com/eula.
> 
> -- ***************************************************************************
> -- This file contains a Vhdl test bench template that is freely editable to   
> -- suit user's needs .Comments are provided in each section to help the user  
> -- fill out necessary details.                                                
> -- ***************************************************************************
> -- Generated on "09/30/2024 12:25:16"
>                                                             
> -- Vhdl Test Bench template for design  :  ringteller
> -- 
> -- Simulation tool : Questa Intel FPGA (VHDL)
> -- 
> 
> LIBRARY ieee;                                               
> USE ieee.std_logic_1164.all;                                
> 
> ENTITY ringteller_vhd_tst IS
> END ringteller_vhd_tst;
> ARCHITECTURE ringteller_arch OF ringteller_vhd_tst IS
> -- constants         
> constant periode : time := 20 ns;                       
> constant data_in_vektor : std_logic_vector := "000000111000111100001110111100100000010000";                 
> -- signals                                                                                      
> SIGNAL clk : STD_LOGIC;
> SIGNAL data_inn : STD_LOGIC_VECTOR(3 DOWNTO 0);
> SIGNAL Q : STD_LOGIC_VECTOR(3 DOWNTO 0);
> SIGNAL rst : STD_LOGIC;
> COMPONENT ringteller
> 	PORT (
> 	clk : IN STD_LOGIC;
> 	data_inn : IN STD_LOGIC_VECTOR(3 DOWNTO 0);
> 	Q : BUFFER STD_LOGIC_VECTOR(3 DOWNTO 0);
> 	rst : IN STD_LOGIC
> 	);
> END COMPONENT;
> BEGIN
> 	i1 : ringteller
> 	PORT MAP (
> -- list connections between master ports and signals
> 	clk => clk,
> 	data_inn => data_inn,
> 	Q => Q,
> 	rst => rst
> 	);
> 
>                       
> 
> p_klokke : PROCESS 
> begin
> 	clk <= '0';
> 	loop
> 		wait for periode/2;
> 		clk <= not clk;
> 	end loop;
> 	wait;
> end process p_klokke;
> 
> 
> 
> 
> init : PROCESS                                               
> -- variable declarations                                     
> BEGIN                                                        
>         -- code that executes only once        
> 	data_inn <= "1100" after 0ns;
> 	rst <= '1', '0' after 2*periode;
> WAIT;                                                       
> END PROCESS init;                                           
> always : PROCESS                                              
> -- optional sensitivity list                                  
> -- (        )                                                 
> -- variable declarations                                      
> BEGIN                                                         
>         -- code executes for every event on sensitivity list  
> WAIT;                                                        
> END PROCESS always;                                          
> END ringteller_arch;
> 
> ```
> ![[VHDL-20240930123340973.jpg|500]]

### Ringteller 8 bit



## Metastabilitet
[[F18 000 Timing og synkronisering A.pdf]]
Ettersom vipper består av fysiske transistorer, bruker de tid på å endre tilstand. Såkalt setup- og hold-time.

![[VHDL-20241015093051050.jpg|500]]

Slår klokka så fort at man "henter" signalet fra en vippe før det er satt opp, eller endrer tilstanden før den har stabilisert seg, kan man oppnå metastabilitet: En tilstand hvor vippen er i en udefinert tilstand, midt mellom tilstandene. Det kan fikse seg etter noen klokkeslag.

![[VHDL-20241015092850624.jpg|500]]

Har man to ulike klokker oppstår det fort ustabilitet. 
1. Skal man hente et signal fra et klokkesignal hvor kilden har klokkesignal lavere enn endeklokka, kan man bruke to vipper. Den første vippa kan oppnå metastabilitet, men vippe 2 får et signal.
2. Har destinasjonsklokka lavere frekvens, må man ha en handshake.
![[VHDL-20241015093908858.jpg|500]]


### Flankedeteksjon
![[VHDL-20241015093949267.jpg|500]]

### Synkronisering av innsignal

Bruker helst 2 registre; best practice. Kan bruke 1, se pdf over.
```VHDL
p_sync_to_register : process (clk) is
begin
	if rising_edge(clk) then
		dff1 <= data_inn;
		dff2 <= dff1;
	end if;
end process p_sync_to_register;
data_ut <= dff2;
```


## TIlstandsmaskin
Se [[F19_000 Tilstandsmaskiner_A.pdf]].

### Eksempel
> [!NOTE]- Tilstandsdiagram
> ![[VHDL-20241021120535110.jpg|500]]

> [!NOTE]- Architecture antiprell hvor utgangen settes sammen med tilstandstabellen
> ```VHDL
> architecture RTL of antiprell is
>     type tilstand_type is (start, vent, funnet_1, ligger_hoegt, til_null);
>     signal tilstand : tilstand_type;
> 
> begin
> 
>     p_tilstand : process(clk)  begin
>         if rising_edge(clk) then 
>             if reset_clk = '0' then
>                 tilstand <= start;
>             else
>                 case tilstand is
>                     when start =>
>                         passering <= '0';
>                         tilstand <= vent;
> 
>                     when vent => 
>                         passering <= '0';
>                         if input = '1' then
>                             tilstand <= funnet_1;
>                         else
>                             tilstand <= start;
>                         end if;
> 
>                     when funnet_1 =>
>                         passering <= '0';
>                         if input = '1' then
>                             tilstand <= ligger_hoegt;
>                         else
>                             tilstand <= vent;
>                         end if;
> 
>                     when ligger_hoegt =>
>                         passering <= '1';
>                         if input = '0' then
>                             tilstand <= til_null;
>                         end if;
>                         
>                     when til_null =>
>                         passering <= '1';
>                         if input = '1' then
>                             tilstand <= ligger_hoegt;
>                         else
>                             tilstand <= vent;
>                         end if;
>                 end case;
>             end if;
>         end if;
>     end process p_tilstand;
> ```

> [!NOTE]- Architecture antiprell hvor utgangen settes i en seperat prosess
> 
> ```VHDL
> architecture RTL of antiprell is
>     type tilstand_type is (start, vent, funnet_1, ligger_hoegt, til_null);
>     signal tilstand : tilstand_type;
> 
> begin
> 
>     p_tilstand : process(clk)  begin
>         if rising_edge(clk) then 
>             if reset_clk = '0' then
>                 tilstand <= start;
>             else
>                 case tilstand is
>                     when start =>
>                         tilstand <= vent;
>                     when vent => 
>                         if input = '1' then
>                             tilstand <= funnet_1;
>                         else
>                             tilstand <= start;
>                         end if;
>                     when funnet_1 =>
>                         if input = '1' then
>                             tilstand <= ligger_hoegt;
>                         else
>                             tilstand <= vent;
>                         end if;
>                     when ligger_hoegt =>
>                         if input = '0' then
>                             tilstand <= til_null;
>                         end if;
>                     when til_null =>
>                         if input = '1' then
>                             tilstand <= ligger_hoegt;
>                         else
>                             tilstand <= vent;
>                         end if;
>                 end case;
>                             
> 
>                 case tilstand is
>                     when start =>
>                         null;
>                     when vent =>
>                         null;
>                     when funnet_1 =>
>                         null;
>                     when ligger_hoegt =>
>                         null;
>                     when til_null =>
>                         null;
>                 end case;
>             end if;
>         end if;
>     end process p_tilstand;
>     
>     p_passering : process(tilstand) is
>     begin
>         case tilstand is
>             when ligger_hoegt =>
>             when til_null =>
>                 passering <= '1';
>             when others =>
>                 passering <= '0';
>         end case;
>     end process;
> 
> end architecture RTL;
> ```


## Generate: Bruk loop til å repetere hardware
Sier til syntese at du skal lage denne hardwaren flere ganger.

> [!NOTE]- Full adderer som komponent i en fire bits adderer
> full_adderer.vhd (component)
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity full_adderer is
>     port(
>         A : in std_logic;
>         B : in std_logic;
>         C_in : in std_logic;
> 
>         sum : out std_logic;
>         C_out : out std_logic
>     );
> end entity full_adderer;
> 
> architecture RTL of full_adderer is
>     
> begin
>     sum <= (A xor B) xor C_in;
>     C_out <= (A and B) or ((A xor B) and C_in);
> end architecture RTL;
> ```
> fire_bits_adderer.vhd
> ```VHDL
> library ieee;
> use ieee.std_logic_1164.all;
> use ieee.numeric_std.all;
> 
> entity fire_bits_adderer is
>     port(
>         A : in std_logic_vector(3 downto 0);
>         B : in std_logic_vector(3 downto 0);
>         sum : out std_logic_vector(4 downto 0)
>     );
> end entity fire_bits_adderer;
> 
> 
> architecture RTL of fire_bits_adderer is
>     component full_adderer
>         port(
>             A     : in  std_logic;
>             B     : in  std_logic;
>             C_in  : in  std_logic;
>             sum   : out std_logic;
>             C_out : out std_logic
>         );
>     end component full_adderer;
> 
>     signal carry : std_logic_vector(4 downto 0);
>     
> begin
>     carry(0) <= '0';
>     g_adderer : for i in 0 to 3 generate
>     begin
>         full_adderer_inst : component full_adderer
>             port map(
>                 A     => A(i),
>                 B     => B(i),
>                 C_in  => carry(i),
>                 sum   => sum(i),
>                 C_out => carry(i+1)
>             );
>     end generate;
>         
>     sum(4) <= carry(4);
> end architecture RTL;
> ```

## Generic
Mer fleksibel initialisering hvor man kan feks. lage n-bits adderer.

