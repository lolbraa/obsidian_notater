# Eclipse
Installere Eclipse IDE
- [3.1.2. Linux Installation](https://www.intel.com/content/www/us/en/docs/programmable/683525/21-3/linux-installation.html)
- [Getting Start Install Eclipse IDE into Nios EDS - Terasic Wiki](https://www.terasic.com.tw/wiki/Getting_Start_Install_Eclipse_IDE_into_Nios_EDS)

## Feilmelding ved åpning av .sopcinfo
"finner ikke CPU-informasjon"
Hjelp: [Solved: Nios II SBT Crashing on Linux - Intel Community](https://community.intel.com/t5/Intel-Quartus-Prime-Software/Nios-II-SBT-Crashing-on-Linux/m-p/1210994)
Måtte installere Java 8 til systemet.

```sh
sudo apt-get install openjdk-8-jre
cd ~/intelFPGA_lite/23.1std/quartus/linux64
mv jre64 jre64_old
ln -s /lib/jvm/java-1.8.0-openjdk-amd64/jre jre64
```


# NIOS 
1. Start Quartus
2. Opprett et nytt prosjekt
	- Sett riktig teknologi og kretsvariant (se på toppen av pakka) EP4C115F29C7N
	- Velg riktig Modelsim variant og sett spark til VHDL
3. Start Platform Designer
4. Legg til CPU
	- Finnes under: Processor and Peripherals/Embedded processors/NIOSII
	- Velg e variant
5. Legg til RAM
	- Finnes under: Basic Functions/On Chip Memory/ On Chip Memory (RAM or ROM) 
	- sett size til 64k
6. Legg til JTAG UART: 
	- Finnes under: Interface/Serial/JTAG Uart
	- Ingen konfig nødvendig
7. Koble opp forbindelser iht tegning to sider fram
8. Rediger automatisk genererte instans navn til noe kortere og unikt
9. Kjør kommando “System/Assign Base Adresses” og System/Assign Interrupt Numbers
10. Velg prosessoren og fane “Vectors” og sett Reset Vector og Exception Vector til det navn du valgte for RAM
11. Lagre med “File/Save As” til for eksempel my_MCU (min Micro Controller Unit)
12. Eksporter filer med “Generate/Generate HDL”, husk å eksporter som VHDL
13. Importer filene som ble eksportert fra Platform designer ved å legge til my_MPU.qip
14. Velg top nivå fil my_MCU.vhd og lag symbol
15. Importer heart.vhd inn I  prosjektet og lag symbol
16. Lag et ny skjemafil
17. Legg til my_MCU blokka og HEART blokka
18. Legg til 2 inngangspinner og gi de navn CLOCK_50 og KEY[0]
19. Legg til 1 utgangspinne og gi den navn LEDG[0]
20. Trekk alle ledninger
21. Lagre skjema
22. Sett skjemafila som top nivå
23. Importer pin assignmets fila DE2_115_pin_assignments.csv
24. Compiler designet
25. Last ned den genererte sof fila til DE2-115 kortet

Bilde av skjemafil
![[NIOS, SBI, komponenter og slikt-2025.04.09 10.09.02.png|550]]


# Lage egen komponent
![[SBI og komponenter-2025.02.20 14.28.20.jpg]]
![[SBI og komponenter-2025.02.20 14.28.29.jpg]]


Prosjektoppgave med egne outputs. 
- Lager interface "conduits"
- signal type: hva enn du vil kalle det
![[NIOS, SBI, komponenter og slikt-2025.04.09 10.07.40.png|550]]
![[NIOS, SBI, komponenter og slikt-2025.04.09 10.08.00.png|550]]

# HW-kode
Over SBI kan man gjøre tre ting:
- Read
	- Lese verdier fra HW-signal
- WriteStrobe
	- Skrive en verdi til et HW-signal som kun er på i ett klokkeslag, for å så resettes
- ReadWrite
	- Kommunikasjon begge veier

```VHDL
-- Kristoffer Loland Braa
-- Semesteroppgave, DMX_Master, april 2025
-- Dette er register-leddet hvor SW skriver til før det lastes inn i selve FIFO-HW
-- Den er basert på forelesers FIFO

library ieee;
use ieee.std_logic_1164.all;
use ieee.numeric_std.all;

entity dmx_fifo_register is
    port(
        CLK               : in  std_logic;
        RST               : in  std_logic;
        -- SBI-bus
        CHIPSELECT        : in  std_logic;
        WRITE             : in  std_logic;
        READ              : in  std_logic;
        ADDRESS           : in  std_logic_vector(1 downto 0);
        WRITEDATA         : in  std_logic_vector(31 downto 0);
        READDATA          : out std_logic_vector(31 downto 0);
        -- Signaler til/fra FIFO
        FIFO_WR           : out std_logic;
        FIFO_RD           : out std_logic;
        FIFO_CNT          : in  std_logic_vector(8 downto 0);
        FIFO_FULL         : in  std_logic;
        FIFO_EMPTY        : in  std_logic;
        FIFO_DATA_IN      : out std_logic_vector(31 downto 0);
        FIFO_DATA_OUT     : in  std_logic_vector(31 downto 0);

        -- Øvrige signaler
        TX_READY          : in std_logic;
        START_PULSE       : out  std_logic;
        BAUD_RATE_DIVIDER : out std_logic_vector(15 downto 0)
    );
end entity dmx_fifo_register;

architecture RTL of dmx_fifo_register is
    signal fifo_wr_int      : std_logic;
    signal fifo_rd_int      : std_logic;
    signal fifo_data_in_int : std_logic_vector(31 downto 0);
begin

    p_writestrobe_register : process(CLK) is
    begin
        if rising_edge(CLK) then
            if RST = '1' then
                fifo_wr_int <= '0';
                fifo_rd_int <= '0';
            elsif CHIPSELECT = '1' and WRITE = '1' and ADDRESS = "00" then
                fifo_wr_int <= WRITEDATA(0);
                fifo_rd_int <= WRITEDATA(1);
            else
                fifo_wr_int <= '0';
                fifo_rd_int <= '0';
            end if;
        end if;
    end process p_writesync_register;

    FIFO_WR <= fifo_wr_int;
    FIFO_RD <= fifo_rd_int;

    p_readwrite_register : process(CLK) is
    begin
        if rising_edge(CLK) then
            if RST = '1' then
                fifo_data_in_int <= (others => '0');
            elsif CHIPSELECT = '1' and WRITE = '1' and ADDRESS = "01" then
                fifo_data_in_int <= WRITEDATA(31 downto 0);
            end if;
        end if;
    end process p_readwrite_register;
    FIFO_DATA_IN <= fifo_data_in_int;

    p_read : process(CHIPSELECT, READ, ADDRESS, FIFO_CNT, FIFO_EMPTY, FIFO_FULL, fifo_data_in_int, FIFO_DATA_OUT, fifo_rd_int, fifo_wr_int) is
    begin
        if CHIPSELECT = '1' and READ = '1' then
            case ADDRESS is
                when "00" =>
                    READDATA <= (0 => fifo_wr_int, 1 => fifo_rd_int, others => '0');
                when "01" =>
                    READDATA(31 downto 0) <= fifo_data_in_int;
                when "10" =>
                    READDATA(31 downto 0) <= FIFO_DATA_OUT;
                --READDATA(31 downto 8) <= (others => '0');
                when "11" =>
                    READDATA(10 downto 2) <= FIFO_CNT;
                    --READDATA(1) <= FIFO_EMPTY;
                    --READDATA(0) <= FIFO_FULL;
                    READDATA(31 downto 7) <= (others => '0');
                when others => null;
            end case;
        end if;

    end process p_read;

end architecture RTL;

```