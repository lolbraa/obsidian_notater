Nettverkmaske: 	255.255.255.0



IP-kart
192.168.1.
		1	
			Ruter / Standard gateway
			Altibox ruter, login på altibox.no
				[LOGIN: stigsbraa@gmail.com, Wmds2Foe]
		3
			Raspberry Pi 3 B
			BraaVPN
			braavpn.local
				[LOGIN: braa, Wmds2Foe]
			Tjenester:
				Wireguard-tunnel og Tailscale
				SSH (åpen ut), DDNS, osv.
					DDNS skript i ~/cf/
					Oppdaterer braavpn.lolandbraa.no
				Tailscale
				Pihole (http://192.168.1.3/admin/login.php)
					Standard passord
					Upstream https://www.dns0.eu/ ?
		5
			Printer
			HP LaserJet P1100w Series
			support.hp.com/no-no/drivers/selfservice/HP-LaserJet-Pro-P1102w-Drucker/4110394/model/4110306
		6
			UniFi CloudKey
				[LOGIN: krissernbraa@hotmail.com, Wmds2Foe]
				SSH controllersoftware: [LOGIN: braa, Wmds2Foe]
				SSH Cloud Key: [LOGIN: krissernbraa@hotmail.com, Wmds2Foe]
				APenes spredningskart [AP Antenna Radiation Patterns – Ubiquiti Help Center](https://help.ui.com/hc/en-us/articles/115005212927-AP-Antenna-Radiation-Patterns)
		10
			BraaNAS (ny)
			Hostname: BraaNAS
			OS: Unraid
			Specs:
				CPU: Intel Pentium G3250 3.2 GHz
				RAM: 2x 
				Hovedkort: ASUS BB5M-G3250
					6 SATA: 4 SATA3 og 2 SATA2
					1 PCIEx16
					2 PCIEx1
				PSU: Silver Power SP-SS850 fra gamle Martins PC
			Disker:
				12TB...
		11 
			BraaKVM
			hostname kvm-1958
			Tailnet IP: 100.123.55.26
			Tailnet: braakvm.barn-banjo.ts.net
		65	
			FAM-BRAA-NAS (gammel)
			WD MyCloud EX4
			4x4TB 3.5tommer HDD
			PATH: "\\FAM-BRAA-NAS\Fam_Braa"
			PATH: "\\FAM-BRAA-NAS\Backup"
			PATH: "\\FAM-BRAA-NAS\Kristoffer"
			PATH: "\\FAM-BRAA-NAS\Public"
				"\photoframe" er en mappe som serveres med WebDAV internt på nettet. 
				iPad-appen Pixette indexer og cacher bilder/videoer herifra og viser.
				Appen er kjøpt på kristoffer@lolandbraa.no-Apple-kontoen.
				URL: http://192.168.1.65/Public/photoframe
				Username: photoframe
				Password: Wmds2Foe
				
			
			
			
			
gammelt:
		11
			Kristoffer PC
		40	
			Server Host
			ESXi Hypervisor 6.5
				[LOGIN: root, Wmds2Foe!]
		41	
			Server Host
			IMM2
				[LOGIN: admin, Wmds2Foe!]
		42	
			Server Host-VM 
			Test Windows Server 2019
				[LOGIN: Wmds2Foe!]
		43	
			Server Host-VM
			CentOS 8 Stream GUI
				[LOGIN: admin, Wmds2Foe]
				[LOGIN: root, Wmds2Foe]
		44
		database.norwaycraft.no
			Server Host-VM
			CentOS 8 Stream CLI
				SSH fra Windows CMD "ssh 192.168.1.44 -l admin"
				Web-interface på :9090
				[LOGIN: admin, Wmds2Foe]
				[LOGIN: root, Wmds2Foe!]
			MariaDB 
				CONFIFG PATH: "/etc/my.cnf.d/mariadb-server.cnf"
				Portforwardet til alle under 192.168.1.%
				[LOGIN: root@localhost, Wmds2Foe!] root-tilgang
				[LOGIN: admin@localhost, Wmds2Foe] tilgang til alle databaser
				[LOGIN: nc@192.168.1.%, Bogen] for NC-servere
				[LOGIN: wp@192.168.1.%, Wmds2Foe] for WordPress
		45
			Server Host-VM
			Debian 10
			NCv9 - Survival
				[Login: root, Wmds2Foe!]
				[Login: ncv9, Bogen]
		46
			Server Host-VM
			Debian 10
			NCv9 - Bygg og Creative
				[Login: root, Wmds2Foe!]
				[Login: ncv9, Bogen]
		47
			Server Host-VM
			Debian 10
			NCv9 - Minigames
				[Login: root, Wmds2Foe!]
				[Login: ncv9, Bogen]
		50	
			Server Host-VM 
			Windows 10 Pro
			Norwaycraft
		51	
			Server Host-VM
			Windows 10 Pro
			Martin
		52	
			Server PC
			Windows 10 Pro
			PATH: "\\SERVERPC\NCserver"
		53
			Server Host-VM
			Windows 10 Pro
			Kristoffer
