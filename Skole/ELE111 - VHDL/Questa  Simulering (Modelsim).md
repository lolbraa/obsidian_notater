Se [[#Simulere i Questa]].

[GitHub - UniversityOfPlymouth-Electronics/Quartus21\_Ubuntu: Setup instructions for Quartus 21.x and Questa for Ubuntu 20.04](https://github.com/UniversityOfPlymouth-Electronics/Quartus21_Ubuntu)

Starte modelsim alene
```
kristoffer@krisslaptoppop:~/intelFPGA_lite/23.1std/questa_fse/linux_x86_64$ ./vsim

/home/kristoffer/intelFPGA_lite/23.1std/questa_fse/linux_x86_64/vsim
```

Questa directory
```
/home/kristoffer/intelFPGA_lite/23.1std/questa_fse/linux_x86_64
```

modelsim.desktop laget med Arronax og [How to create a desktop shortcut for a command? - Ask Ubuntu](https://askubuntu.com/questions/396273/how-to-create-a-desktop-shortcut-for-a-command)
```
[Desktop Entry]
Categories=Utility;Application;
Comment[en_US]=This is my comment
Comment=This is my comment
Exec=/home/kristoffer/intelFPGA_lite/23.1std/questa_fse/linux_x86_64/vsim
GenericName[en_US]=
GenericName=
Icon=-symbolic
Name[en_US]=ModelSim
Name=ModelSim
StartupNotify=true
Terminal=true
TerminalOptions=
Type=Application
Version=
X-DBUS-ServiceName=
X-DBUS-StartupType=
X-KDE-SubstituteUID=false
X-KDE-Username=
Hidden=false

```

# Syntaks for Simulering (i `.vht`)
Simuleringsinstruksene implementeres 
- for parallelle i ``init``
```VHDL
init : PROCESS                                               
-- variable declarations                                     
BEGIN                                                        
	-- code that executes only once  
END PROCESS init;   
```

### Vente x sekunder
```VHDL
Wait for <tidsenheter> us;
```

```VHDL
s <=    '0' after 500 ns, '1' after 2*500 ns,
		'0' after 3*500 ns, '1' after 4*500 ns,
		'0' after 5*500 ns, '1' after 6*500 ns;
```

### Egen prosess med navn "velger"
```VHDL
velger : PROCESS
BEGIN
	s <= '0' after 500 ns, '1' after 2*500 ns;
	WAIT;
END PROCESS velger;

init : PROCESS
BEGIN
	x <= '0'; y <= '0';
	wait for 1 us; x <= '1'; y <= '1';
	wait for 1 us; x <= '0'; y <= '1';
	WAIT;
END PROCESS init;

END mux2_arch;
```
### Sette startverdi/konstanter (simulering)
```VHDL
ARCHITECTURE Lab2_del1_arch OF Lab2_del1_vhd_tst IS
-- constants
constant period : time := 10 ns;                                                 
-- signals                                                
SIGNAL clk : STD_LOGIC := '0'   
```
![[VHDL-20240903093218866.jpg|500]]

### Simulering av Process (sekvensiell kode)
![[VHDL-20240903112335564.jpg|500]]
#### Alltid sett klokkesignal i simulering
```VHDL
constant period : time := 10 ns;
...
p_clk : process is
	begin
	clk <= '0';
	--clk <= '0' after 0 ns, '1' after period/2;
	loop
		wait for period / 2;
		clk <= not clk;
	end loop;
wait;
end process p_clk;
```

### Teste over vektor
```VHDL
constant inputs: std_logic_vector := "001110101110000100100011111";
...
for i in inputs'range loop
	d <= inputs(i);
	wait for period;
end loop;
```


### Snippets
#### Sekvensiell testing
```VHDL
init : PROCESS                                               
-- variable declarations                                     
BEGIN                                                        
	-- code that executes only once    
	s <= '0';
	x <= '0';
	y <= '0';                  
	WAIT for 1 us;
	s <= '1';
	WAIT for 1 us;
	x <= '1';                                                     
END PROCESS init;   
```

#### Periodisk gjentakelse
![[VHDL-20240827091510358.jpg|400]]


### Reset fra boka
LISTING 14.3.2
Process for a reset pulse whose duration is a multiple of the clock period.
```VHDL
reset: process
begin
	reset_bar <= ' 0 ' ;
	for i in 1 to 2 loop
		wait until clk = ' 1 ' ;
	end loop;
	reset_bar <= ' 1 ' ;
	wait;
end process;
```


