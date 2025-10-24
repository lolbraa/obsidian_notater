Surface Laptop 3 15", model 1872

[[Surface Laptop 3 and 4 English Service Guide.pdf]]

# Sikkerhet
[GitHub - iAnonymous3000/popos-hardening-guide: A step-by-step guide to securing Pop!\_OS Linux desktops. Covering system updates, user security, network hardening, disk encryption, and more, this guide is tailored for users looking to enhance their Pop!\_OS security posture.](https://github.com/iAnonymous3000/popos-hardening-guide?tab=readme-ov-file)
## ClamAV
```sh
sudo clamscan -r ~
```
## Lynis
[Get Started with Lynis - Installation Guide - CISOfy](https://cisofy.com/documentation/lynis/get-started/#first-run)
git clone til Nextcloud:/07 Verktøy/11 Sikkerhet/lynis
Måtte kopiere over til home for å kjøre.
```sh
$ lynis audit system
```


# Battery-drain og skrus av under sleep

https://www.reddit.com/r/pop_os/comments/n2hw7p/draining_too_much_battery_in_sleep_mode/
```
sudo kernelstub -a mem_sleep_default=deep 
```

Syslog etter en sleep death
```
Aug 22 10:59:51 krisslaptoppop systemd[1]: Reached target Sleep.
Aug 22 10:59:51 krisslaptoppop systemd[1]: Starting System Suspend...
Aug 22 12:09:57 krisslaptoppop systemd-modules-load[383]: Inserted module 'lp'
```
[Suspend doesn't work on SP3 · Issue #638 · linux-surface/linux-surface · GitHub](https://github.com/linux-surface/linux-surface/issues/638)

# VPN
## Tailscale
```sh
sudo tailscale set --exit-node=""
sudo tailscale set --exit-node="lolbraakvm"
sudo tailscale set --accept-routes --accept-dns --exit-node-allow-lan-access
```
## Wireguard ved siden av Tailscale
[Reddit - Dive into anything](https://www.reddit.com/r/WireGuard/comments/v0wmqw/is_it_possible_to_use_tailscale_and_wireguard/)

# OneNote i docker
- [Reddit - Dive into anything](https://www.reddit.com/r/linuxquestions/comments/pjkl4r/onenote_for_linux/)
- [GitHub - patrikx3/onenote: 📚 Linux Electron Onenote - A Linux compatible version of OneNote](https://github.com/patrikx3/onenote)
- [GitHub - Fmstrat/winapps: Run Windows apps such as Microsoft Office/Adobe in Linux (Ubuntu/Fedora) and GNOME/KDE as if they were a part of the native OS, including Nautilus integration.](https://github.com/Fmstrat/winapps)
- [GitHub - winapps-org/winapps: The winapps main project, forked from https://github.com/Fmstrat/winapps/](https://github.com/winapps-org/winapps)
- Alternativ [GitHub - xournalpp/xournalpp: Xournal++ is a handwriting notetaking software with PDF annotation support. Written in C++ with GTK3, supporting Linux (e.g. Ubuntu, Debian, Arch, SUSE), macOS and Windows 10. Supports pen input from devices such as Wacom Tablets.](https://github.com/xournalpp/xournalpp/)
- Endte med [winapps/docs/docker.md at main · winapps-org/winapps · GitHub](https://github.com/winapps-org/winapps/blob/main/docs/docker.md)
```sh
docker compose --file ~/.config/winapps/compose.yaml start # Power on the Windows VM
docker compose --file ~/.config/winapps/compose.yaml pause # Pause the Windows VM
docker compose --file ~/.config/winapps/compose.yaml unpause # Resume the Windows VM
docker compose --file ~/.config/winapps/compose.yaml restart # Restart the Windows VM
docker compose --file ~/.config/winapps/compose.yaml stop # Gracefully shut down the Windows VM
docker compose --file ~/.config/winapps/compose.yaml kill # Force shut down the Windows VM
```
- Disable autologin [How to disable auto login in Windows 11? - Super User](https://superuser.com/questions/1706978/how-to-disable-auto-login-in-windows-11)

Endte med å ikke få til winapps, men bruker dockeren med Tiny11 og RDPer inn med Remmina.
- [# Horizontal Scrolling?](https://www.reddit.com/r/OneNote/comments/l2wv8i/horizontal_scrolling/?rdt=36976) med dette skriptet [A solution for enabling horizontal scrolling in OneNote for Windows 10 · GitHub](https://gist.github.com/genebit/c9e1a189d6b438dac7294125705175a4)

## Permissions på filer laget i dockeren
Filer som lagres i Windows, men i POP OS sitt filsystem, lagres av Docker-brukeren og er derfor ikke mulig å endre direkte for kristoffer-brukeren.
```sh
sudo chown 1000:1000 MAPPE/./FILER/*/
```


---

# Troubleshooting wifi error
Masse feilmeldinger i dmesg

[Linux\* Support for Intel® Wireless Adapters](https://www.intel.com/content/www/us/en/support/articles/000005511/wireless.html)
[Intel® Wireless Wi-Fi Drivers for Linux\*](https://www.intel.com/content/www/us/en/download/824804/intel-wireless-wi-fi-drivers-for-linux.html)
[Making sure you're not a bot!](https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/)

> [!NOTE]- Eksempel fra boot
> ```
> iwlwifi 0000:00:14.3: Registered PHC clock: iwlwifi-PTP, with index: 0
> [   10.029686] iwlwifi 0000:00:14.3: Microcode SW error detected. Restarting 0x0.
> [   10.029790] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [   10.029791] iwlwifi 0000:00:14.3: Transport status: 0x0000004A, valid: 6
> [   10.029793] iwlwifi 0000:00:14.3: Loaded firmware version: 77.2753b721.0 Qu-c0-hr-b0-77.ucode
> [   10.029795] iwlwifi 0000:00:14.3: 0x00000091 | ADVANCED_SYSASSERT          
> [   10.029797] iwlwifi 0000:00:14.3: 0x200022F0 | trm_hw_status0
> [   10.029798] iwlwifi 0000:00:14.3: 0x00000000 | trm_hw_status1
> [   10.029799] iwlwifi 0000:00:14.3: 0x004C95A2 | branchlink2
> [   10.029800] iwlwifi 0000:00:14.3: 0x00001D6E | interruptlink1
> [   10.029801] iwlwifi 0000:00:14.3: 0x00001D6E | interruptlink2
> [   10.029803] iwlwifi 0000:00:14.3: 0x00005E58 | data1
> [   10.029804] iwlwifi 0000:00:14.3: 0x00010000 | data2
> [   10.029805] iwlwifi 0000:00:14.3: 0x00000000 | data3
> [   10.029806] iwlwifi 0000:00:14.3: 0x0037FA85 | beacon time
> [   10.029807] iwlwifi 0000:00:14.3: 0x00000000 | tsf low
> [   10.029808] iwlwifi 0000:00:14.3: 0x00000000 | tsf hi
> [   10.029809] iwlwifi 0000:00:14.3: 0x00000000 | time gp1
> [   10.029810] iwlwifi 0000:00:14.3: 0x000926E6 | time gp2
> [   10.029811] iwlwifi 0000:00:14.3: 0x00000001 | uCode revision type
> [   10.029813] iwlwifi 0000:00:14.3: 0x0000004D | uCode version major
> [   10.029814] iwlwifi 0000:00:14.3: 0x2753B721 | uCode version minor
> [   10.029815] iwlwifi 0000:00:14.3: 0x00000332 | hw version
> [   10.029816] iwlwifi 0000:00:14.3: 0x00C89002 | board version
> [   10.029817] iwlwifi 0000:00:14.3: 0x0000001C | hcmd
> [   10.029818] iwlwifi 0000:00:14.3: 0x02220000 | isr0
> [   10.029820] iwlwifi 0000:00:14.3: 0x00000000 | isr1
> [   10.029821] iwlwifi 0000:00:14.3: 0x08F00002 | isr2
> [   10.029822] iwlwifi 0000:00:14.3: 0x00C0001D | isr3
> [   10.029823] iwlwifi 0000:00:14.3: 0x00000000 | isr4
> [   10.029824] iwlwifi 0000:00:14.3: 0x00190103 | last cmd Id
> [   10.029825] iwlwifi 0000:00:14.3: 0x00005E58 | wait_event
> [   10.029826] iwlwifi 0000:00:14.3: 0x000000D4 | l2p_control
> [   10.029827] iwlwifi 0000:00:14.3: 0x00001420 | l2p_duration
> [   10.029828] iwlwifi 0000:00:14.3: 0x00000007 | l2p_mhvalid
> [   10.029829] iwlwifi 0000:00:14.3: 0x00000000 | l2p_addr_match
> [   10.029835] iwlwifi 0000:00:14.3: 0x00000000 | lmpm_pmg_sel
> [   10.029837] iwlwifi 0000:00:14.3: 0x00000000 | timestamp
> [   10.029839] iwlwifi 0000:00:14.3: 0x0000286C | flow_handler
> [   10.029895] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [   10.029897] iwlwifi 0000:00:14.3: Transport status: 0x0000004A, valid: 7
> [   10.029899] iwlwifi 0000:00:14.3: 0x20000070 | NMI_INTERRUPT_LMAC_FATAL
> [   10.029901] iwlwifi 0000:00:14.3: 0x00000000 | umac branchlink1
> [   10.029903] iwlwifi 0000:00:14.3: 0x804561EA | umac branchlink2
> [   10.029905] iwlwifi 0000:00:14.3: 0x8047372E | umac interruptlink1
> [   10.029906] iwlwifi 0000:00:14.3: 0x8047372E | umac interruptlink2
> [   10.029908] iwlwifi 0000:00:14.3: 0x00000400 | umac data1
> [   10.029910] iwlwifi 0000:00:14.3: 0x8047372E | umac data2
> [   10.029912] iwlwifi 0000:00:14.3: 0x00000000 | umac data3
> [   10.029914] iwlwifi 0000:00:14.3: 0x0000004D | umac major
> [   10.029916] iwlwifi 0000:00:14.3: 0x2753B721 | umac minor
> [   10.029917] iwlwifi 0000:00:14.3: 0x0009277D | frame pointer
> [   10.029919] iwlwifi 0000:00:14.3: 0xC0886260 | stack pointer
> [   10.029921] iwlwifi 0000:00:14.3: 0x0021010D | last host cmd
> [   10.029923] iwlwifi 0000:00:14.3: 0x00000000 | isr status reg
> [   10.029942] iwlwifi 0000:00:14.3: IML/ROM dump:
> [   10.029943] iwlwifi 0000:00:14.3: 0x00000003 | IML/ROM error/state
> [   10.029952] iwlwifi 0000:00:14.3: 0x0000591E | IML/ROM data1
> [   10.029961] iwlwifi 0000:00:14.3: 0x00000080 | IML/ROM WFPM_AUTH_KEY_0
> [   10.029967] iwlwifi 0000:00:14.3: Fseq Registers:
> [   10.029971] iwlwifi 0000:00:14.3: 0x60000000 | FSEQ_ERROR_CODE
> [   10.029973] iwlwifi 0000:00:14.3: 0x80290033 | FSEQ_TOP_INIT_VERSION
> [   10.029976] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_CNVIO_INIT_VERSION
> [   10.029979] iwlwifi 0000:00:14.3: 0x0000A492 | FSEQ_OTP_VERSION
> [   10.029983] iwlwifi 0000:00:14.3: 0x00000003 | FSEQ_TOP_CONTENT_VERSION
> [   10.029986] iwlwifi 0000:00:14.3: 0x4552414E | FSEQ_ALIVE_TOKEN
> [   10.029989] iwlwifi 0000:00:14.3: 0x02000300 | FSEQ_CNVI_ID
> [   10.029992] iwlwifi 0000:00:14.3: 0x01300504 | FSEQ_CNVR_ID
> [   10.029995] iwlwifi 0000:00:14.3: 0x02000300 | CNVI_AUX_MISC_CHIP
> [   10.030000] iwlwifi 0000:00:14.3: 0x01300504 | CNVR_AUX_MISC_CHIP
> [   10.030006] iwlwifi 0000:00:14.3: 0x05B0905B | CNVR_SCU_SD_REGS_SD_REG_DIG_DCDC_VTRIM
> [   10.030027] iwlwifi 0000:00:14.3: 0x0000025B | CNVR_SCU_SD_REGS_SD_REG_ACTIVE_VDIG_MIRROR
> [   10.030030] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_PREV_CNVIO_INIT_VERSION
> [   10.030033] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_WIFI_FSEQ_VERSION
> [   10.030052] iwlwifi 0000:00:14.3: 0xABE45E8E | FSEQ_BT_FSEQ_VERSION
> [   10.030055] iwlwifi 0000:00:14.3: 0x00000136 | FSEQ_CLASS_TP_VERSION
> [   10.030065] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0x8047323c
> [   10.030067] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xd0
> [   10.030101] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 4 fired (delay=0ms).
> [   10.048360] iwlwifi 0000:00:14.3: Device error - SW reset
> [   10.048644] ieee80211 phy0: Hardware restart was requested
> [   10.559248] Bluetooth: hci0: Waiting for firmware download to complete
> [   10.559254] Bluetooth: hci0: Firmware loaded in 1655016 usecs
> [   10.559290] Bluetooth: hci0: Waiting for device to boot
> [   10.573222] Bluetooth: hci0: Device booted in 13617 usecs
> [   10.574199] Bluetooth: hci0: Found Intel DDC parameters: intel/ibt-19-32-4.ddc
> [   10.576271] Bluetooth: hci0: Applying Intel DDC parameters completed
> [   10.577267] Bluetooth: hci0: Firmware revision 0.4 build 132 week 3 2024
> [   10.579253] Bluetooth: hci0: HCI LE Coded PHY feature bit is set, but its usage is not supported.
> [   10.644319] Bluetooth: MGMT ver 1.23
> [   10.647204] NET: Registered PF_ALG protocol family
> [   10.661633] Bluetooth: RFCOMM TTY layer initialized
> [   10.661643] Bluetooth: RFCOMM socket layer initialized
> [   10.661648] Bluetooth: RFCOMM ver 1.11
> [   11.488171] rfkill: input handler disabled
> [   12.112562] iwlwifi 0000:00:14.3: SecBoot CPU1 Status: 0x5929, CPU2 Status: 0x3
> [   12.112593] iwlwifi 0000:00:14.3: WFPM_LMAC1_PD_NOTIFICATION: 0x0
> [   12.112603] iwlwifi 0000:00:14.3: HPM_SECONDARY_DEVICE_STATE: 0x42
> [   12.112614] iwlwifi 0000:00:14.3: WFPM_MAC_OTP_CFG7_ADDR: 0x0
> [   12.112624] iwlwifi 0000:00:14.3: WFPM_MAC_OTP_CFG7_DATA: 0x0
> [   12.112626] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0xa05c18
> [   12.112628] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xa05c1c
> [   12.112631] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [   12.112725] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [   12.112727] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 6
> [   12.112729] iwlwifi 0000:00:14.3: Loaded firmware version: 77.2753b721.0 Qu-c0-hr-b0-77.ucode
> [   12.112732] iwlwifi 0000:00:14.3: 0x00000092 | ADVANCED_SYSASSERT          
> [   12.112735] iwlwifi 0000:00:14.3: 0x000022F0 | trm_hw_status0
> [   12.112738] iwlwifi 0000:00:14.3: 0x00000000 | trm_hw_status1
> [   12.112740] iwlwifi 0000:00:14.3: 0x004C95A2 | branchlink2
> [   12.112742] iwlwifi 0000:00:14.3: 0x0001539C | interruptlink1
> [   12.112744] iwlwifi 0000:00:14.3: 0x0001539C | interruptlink2
> [   12.112746] iwlwifi 0000:00:14.3: 0x00014F4A | data1
> [   12.112748] iwlwifi 0000:00:14.3: 0x0BADCAFE | data2
> [   12.112750] iwlwifi 0000:00:14.3: 0x00000000 | data3
> [   12.112752] iwlwifi 0000:00:14.3: 0x00000000 | beacon time
> [   12.112754] iwlwifi 0000:00:14.3: 0x00000000 | tsf low
> [   12.112756] iwlwifi 0000:00:14.3: 0x00000000 | tsf hi
> [   12.112758] iwlwifi 0000:00:14.3: 0x00000000 | time gp1
> [   12.112760] iwlwifi 0000:00:14.3: 0x0003C4F4 | time gp2
> [   12.112763] iwlwifi 0000:00:14.3: 0x00000001 | uCode revision type
> [   12.112765] iwlwifi 0000:00:14.3: 0x0000004D | uCode version major
> [   12.112767] iwlwifi 0000:00:14.3: 0x2753B721 | uCode version minor
> [   12.112769] iwlwifi 0000:00:14.3: 0x00000332 | hw version
> [   12.112771] iwlwifi 0000:00:14.3: 0x00C89002 | board version
> [   12.112773] iwlwifi 0000:00:14.3: 0x00000000 | hcmd
> [   12.112775] iwlwifi 0000:00:14.3: 0x00020000 | isr0
> [   12.112777] iwlwifi 0000:00:14.3: 0x00000000 | isr1
> [   12.112779] iwlwifi 0000:00:14.3: 0x08F00002 | isr2
> [   12.112781] iwlwifi 0000:00:14.3: 0x00C0001C | isr3
> [   12.112783] iwlwifi 0000:00:14.3: 0x00000000 | isr4
> [   12.112785] iwlwifi 0000:00:14.3: 0x00000000 | last cmd Id
> [   12.112787] iwlwifi 0000:00:14.3: 0x00014F4A | wait_event
> [   12.112789] iwlwifi 0000:00:14.3: 0x00000000 | l2p_control
> [   12.112791] iwlwifi 0000:00:14.3: 0x00000000 | l2p_duration
> [   12.112794] iwlwifi 0000:00:14.3: 0x00000000 | l2p_mhvalid
> [   12.112795] iwlwifi 0000:00:14.3: 0x00000000 | l2p_addr_match
> [   12.112798] iwlwifi 0000:00:14.3: 0x0000004B | lmpm_pmg_sel
> [   12.112799] iwlwifi 0000:00:14.3: 0x00000000 | timestamp
> [   12.112801] iwlwifi 0000:00:14.3: 0x0000F81C | flow_handler
> [   12.112843] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [   12.112845] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 7
> [   12.112847] iwlwifi 0000:00:14.3: 0x20000070 | NMI_INTERRUPT_LMAC_FATAL
> [   12.112849] iwlwifi 0000:00:14.3: 0x00000000 | umac branchlink1
> [   12.112851] iwlwifi 0000:00:14.3: 0x804561EA | umac branchlink2
> [   12.112853] iwlwifi 0000:00:14.3: 0x8047372E | umac interruptlink1
> [   12.112855] iwlwifi 0000:00:14.3: 0x804661DC | umac interruptlink2
> [   12.112857] iwlwifi 0000:00:14.3: 0x00000400 | umac data1
> [   12.112859] iwlwifi 0000:00:14.3: 0x804661DC | umac data2
> [   12.112861] iwlwifi 0000:00:14.3: 0x00000000 | umac data3
> [   12.112863] iwlwifi 0000:00:14.3: 0x0000004D | umac major
> [   12.112865] iwlwifi 0000:00:14.3: 0x2753B721 | umac minor
> [   12.112867] iwlwifi 0000:00:14.3: 0x0003C56D | frame pointer
> [   12.112869] iwlwifi 0000:00:14.3: 0xC0887EE4 | stack pointer
> [   12.112871] iwlwifi 0000:00:14.3: 0x00000000 | last host cmd
> [   12.112873] iwlwifi 0000:00:14.3: 0x00200040 | isr status reg
> [   12.112895] iwlwifi 0000:00:14.3: IML/ROM dump:
> [   12.112897] iwlwifi 0000:00:14.3: 0x00000003 | IML/ROM error/state
> [   12.112922] iwlwifi 0000:00:14.3: 0x00005929 | IML/ROM data1
> [   12.112932] iwlwifi 0000:00:14.3: 0x00000080 | IML/ROM WFPM_AUTH_KEY_0
> [   12.112938] iwlwifi 0000:00:14.3: Fseq Registers:
> [   12.112990] iwlwifi 0000:00:14.3: 0x60000000 | FSEQ_ERROR_CODE
> [   12.113006] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_TOP_INIT_VERSION
> [   12.113032] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_CNVIO_INIT_VERSION
> [   12.113036] iwlwifi 0000:00:14.3: 0x0000A492 | FSEQ_OTP_VERSION
> [   12.113055] iwlwifi 0000:00:14.3: 0x00000003 | FSEQ_TOP_CONTENT_VERSION
> [   12.113059] iwlwifi 0000:00:14.3: 0x4552414E | FSEQ_ALIVE_TOKEN
> [   12.113079] iwlwifi 0000:00:14.3: 0x02000300 | FSEQ_CNVI_ID
> [   12.113083] iwlwifi 0000:00:14.3: 0x01300504 | FSEQ_CNVR_ID
> [   12.113110] iwlwifi 0000:00:14.3: 0x02000300 | CNVI_AUX_MISC_CHIP
> [   12.113131] iwlwifi 0000:00:14.3: 0x01300504 | CNVR_AUX_MISC_CHIP
> [   12.113153] iwlwifi 0000:00:14.3: 0x05B0905B | CNVR_SCU_SD_REGS_SD_REG_DIG_DCDC_VTRIM
> [   12.113175] iwlwifi 0000:00:14.3: 0x0000025B | CNVR_SCU_SD_REGS_SD_REG_ACTIVE_VDIG_MIRROR
> [   12.113195] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_PREV_CNVIO_INIT_VERSION
> [   12.113198] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_WIFI_FSEQ_VERSION
> [   12.113218] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_BT_FSEQ_VERSION
> [   12.113222] iwlwifi 0000:00:14.3: 0x00000136 | FSEQ_CLASS_TP_VERSION
> [   12.113248] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0x8047323c
> [   12.113268] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xd0
> [   12.113273] iwlwifi 0000:00:14.3: Failed to start RT ucode: -110
> [   12.113276] iwlwifi 0000:00:14.3: Failed to start RT ucode: -110
> [   12.113277] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [   13.080143] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 4 fired (delay=0ms).
> [   13.108006] iwlwifi 0000:00:14.3: mac start retry 0
> [   13.108013] ------------[ cut here ]------------
> [   13.108014] Hardware became unavailable during restart.
> [   13.108082] WARNING: CPU: 6 PID: 197 at net/mac80211/util.c:1820 ieee80211_reconfig+0xfe/0x1270 [mac80211]
> [   13.108156] Modules linked in: rfcomm cmac algif_hash algif_skcipher af_alg snd_seq_dummy snd_hrtimer overlay ip6t_REJECT nf_reject_ipv6 xt_hl ip6t_rt ipt_REJECT nf_reject_ipv4 xt_LOG nf_log_syslog nft_limit xt_limit xt_addrtype xt_tcpudp xt_conntrack bnep nf_conntrack nf_defrag_ipv6 nf_defrag_ipv4 zram nft_compat 842_decompress 842_compress lz4hc_compress lz4_compress snd_sof_pci_intel_icl snd_sof_pci_intel_cnl snd_sof_intel_hda_generic soundwire_intel snd_sof_intel_hda_sdw_bpt snd_sof_intel_hda_common snd_soc_hdac_hda snd_sof_intel_hda_mlink snd_sof_intel_hda snd_hda_codec_hdmi soundwire_cadence snd_sof_pci snd_sof_xtensa_dsp nf_tables snd_sof nfnetlink snd_sof_utils binfmt_misc snd_soc_acpi_intel_match snd_soc_acpi_intel_sdca_quirks soundwire_generic_allocation snd_soc_acpi soundwire_bus snd_hda_codec_realtek snd_soc_sdca joydev crc8 snd_hda_codec_generic snd_hda_scodec_component snd_soc_avs snd_soc_hda_codec snd_hda_ext_core intel_uncore_frequency intel_uncore_frequency_common snd_soc_core snd_compress ac97_bus
> [   13.108192]  snd_pcm_dmaengine snd_hda_intel snd_intel_dspcfg snd_intel_sdw_acpi snd_hda_codec snd_hda_core input_leds hid_multitouch snd_hwdep intel_tcc_cooling x86_pkg_temp_thermal snd_pcm intel_powerclamp hid_generic coretemp processor_thermal_device_pci_legacy snd_seq_midi iwlmvm snd_seq_midi_event processor_thermal_device surface_hid processor_thermal_wt_hint surface_platform_profile surface_hid_core nls_iso8859_1 kvm_intel snd_rawmidi platform_temperature_control intel_rapl_msr processor_thermal_rfim mei_pxp mei_hdcp hid surface_battery surface_charger platform_profile gpio_keys surface_gpe mac80211 snd_seq processor_thermal_rapl kvm libarc4 intel_rapl_common btusb cmdlinepart snd_seq_device processor_thermal_wt_req btrtl snd_timer irqbypass processor_thermal_power_floor spi_nor btintel rapl processor_thermal_mbox int3403_thermal intel_cstate snd iwlwifi intel_pmc_core btbcm soundcore mtd mei_me pmt_telemetry intel_wmi_thunderbolt btmtk int340x_thermal_zone surfacepro3_button int3400_thermal pmt_class bluetooth
> [   13.108231]  cfg80211 8250_dw mei intel_soc_dts_iosf mac_hid surface_hotplug intel_pmc_ssram_telemetry soc_button_array surface_aggregator_registry acpi_thermal_rel surface_acpi_notify acpi_pad intel_vsec dptf_power acpi_tad sch_fq_codel kyber_iosched msr parport_pc ppdev lp parport efi_pstore ip_tables x_tables autofs4 dm_crypt raid10 raid456 async_raid6_recov async_memcpy async_pq async_xor async_tx xor raid6_pq raid1 raid0 linear system76_io(OE) system76_acpi(OE) i915 drm_buddy ttm polyval_clmulni nvme ghash_clmulni_intel i2c_algo_bit sha1_ssse3 nvme_core drm_display_helper intel_lpss_pci spi_intel_pci nvme_keyring spi_intel intel_lpss cec nvme_auth idma64 rc_core video wmi surface_aggregator crc_itu_t pinctrl_icelake aesni_intel
> [   13.108270] CPU: 6 UID: 0 PID: 197 Comm: kworker/6:3 Tainted: G           OE       6.16.3-76061603-generic #202508231538~1758010842~22.04~85d2e57 PREEMPT(voluntary) 
> [   13.108273] Tainted: [O]=OOT_MODULE, [E]=UNSIGNED_MODULE
> [   13.108274] Hardware name: Microsoft Corporation Surface Laptop 3/Surface Laptop 3, BIOS 19.101.140 04/11/2024
> [   13.108275] Workqueue: events_freezable ieee80211_restart_work [mac80211]
> [   13.108314] RIP: 0010:ieee80211_reconfig+0xfe/0x1270 [mac80211]
> [   13.108367] Code: c6 85 47 ff ff ff 00 41 c6 87 ad 05 00 00 00 4c 89 ff e8 05 6b fa ff 41 89 c5 85 c0 74 5d 48 c7 c7 90 13 17 c1 e8 42 ac 48 e7 <0f> 0b 4c 89 ff 31 c9 ba 04 00 00 00 be ff ff 00 00 e8 4c f0 ff ff
> [   13.108369] RSP: 0018:ffffcd2c40a37d38 EFLAGS: 00010246
> [   13.108371] RAX: 0000000000000000 RBX: 0000000000000000 RCX: 0000000000000000
> [   13.108372] RDX: 0000000000000000 RSI: 0000000000000000 RDI: 0000000000000000
> [   13.108372] RBP: ffffcd2c40a37df8 R08: 0000000000000000 R09: 0000000000000000
> [   13.108373] R10: 0000000000000000 R11: 0000000000000000 R12: 0000000000000000
> [   13.108374] R13: 00000000ffffff92 R14: ffff8c97257e8920 R15: ffff8c97257e8920
> [   13.108375] FS:  0000000000000000(0000) GS:ffff8c9aaf96a000(0000) knlGS:0000000000000000
> [   13.108377] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
> [   13.108378] CR2: 000074b53c001368 CR3: 0000000120640005 CR4: 0000000000770ef0
> [   13.108379] PKRU: 55555554
> [   13.108380] Call Trace:
> [   13.108381]  <TASK>
> [   13.108383]  ? sched_update_worker+0x64/0x80
> [   13.108388]  ? synchronize_rcu_expedited+0x1e6/0x220
> [   13.108390]  ? __pfx_autoremove_wake_function+0x10/0x10
> [   13.108394]  ? __pfx_wait_rcu_exp_gp+0x10/0x10
> [   13.108396]  ieee80211_restart_work+0xff/0x190 [mac80211]
> [   13.108430]  process_one_work+0x18e/0x3e0
> [   13.108434]  worker_thread+0x2bd/0x3f0
> [   13.108437]  ? __pfx_worker_thread+0x10/0x10
> [   13.108439]  kthread+0x10a/0x230
> [   13.108442]  ? __pfx_kthread+0x10/0x10
> [   13.108444]  ret_from_fork+0x11e/0x140
> [   13.108447]  ? __pfx_kthread+0x10/0x10
> [   13.108449]  ret_from_fork_asm+0x1a/0x30
> [   13.108452]  </TASK>
> [   13.108453] ---[ end trace 0000000000000000 ]---
> [   13.120626] iwlwifi 0000:00:14.3: Failed to synchronize multicast groups update
> [   13.133539] ------------[ cut here ]------------
> [   13.133541] WARNING: CPU: 6 PID: 197 at net/mac80211/driver-ops.c:41 drv_stop+0x11e/0x140 [mac80211]
> [   13.133593] Modules linked in: rfcomm cmac algif_hash algif_skcipher af_alg snd_seq_dummy snd_hrtimer overlay ip6t_REJECT nf_reject_ipv6 xt_hl ip6t_rt ipt_REJECT nf_reject_ipv4 xt_LOG nf_log_syslog nft_limit xt_limit xt_addrtype xt_tcpudp xt_conntrack bnep nf_conntrack nf_defrag_ipv6 nf_defrag_ipv4 zram nft_compat 842_decompress 842_compress lz4hc_compress lz4_compress snd_sof_pci_intel_icl snd_sof_pci_intel_cnl snd_sof_intel_hda_generic soundwire_intel snd_sof_intel_hda_sdw_bpt snd_sof_intel_hda_common snd_soc_hdac_hda snd_sof_intel_hda_mlink snd_sof_intel_hda snd_hda_codec_hdmi soundwire_cadence snd_sof_pci snd_sof_xtensa_dsp nf_tables snd_sof nfnetlink snd_sof_utils binfmt_misc snd_soc_acpi_intel_match snd_soc_acpi_intel_sdca_quirks soundwire_generic_allocation snd_soc_acpi soundwire_bus snd_hda_codec_realtek snd_soc_sdca joydev crc8 snd_hda_codec_generic snd_hda_scodec_component snd_soc_avs snd_soc_hda_codec snd_hda_ext_core intel_uncore_frequency intel_uncore_frequency_common snd_soc_core snd_compress ac97_bus
> [   13.133627]  snd_pcm_dmaengine snd_hda_intel snd_intel_dspcfg snd_intel_sdw_acpi snd_hda_codec snd_hda_core input_leds hid_multitouch snd_hwdep intel_tcc_cooling x86_pkg_temp_thermal snd_pcm intel_powerclamp hid_generic coretemp processor_thermal_device_pci_legacy snd_seq_midi iwlmvm snd_seq_midi_event processor_thermal_device surface_hid processor_thermal_wt_hint surface_platform_profile surface_hid_core nls_iso8859_1 kvm_intel snd_rawmidi platform_temperature_control intel_rapl_msr processor_thermal_rfim mei_pxp mei_hdcp hid surface_battery surface_charger platform_profile gpio_keys surface_gpe mac80211 snd_seq processor_thermal_rapl kvm libarc4 intel_rapl_common btusb cmdlinepart snd_seq_device processor_thermal_wt_req btrtl snd_timer irqbypass processor_thermal_power_floor spi_nor btintel rapl processor_thermal_mbox int3403_thermal intel_cstate snd iwlwifi intel_pmc_core btbcm soundcore mtd mei_me pmt_telemetry intel_wmi_thunderbolt btmtk int340x_thermal_zone surfacepro3_button int3400_thermal pmt_class bluetooth
> [   13.133699]  cfg80211 8250_dw mei intel_soc_dts_iosf mac_hid surface_hotplug intel_pmc_ssram_telemetry soc_button_array surface_aggregator_registry acpi_thermal_rel surface_acpi_notify acpi_pad intel_vsec dptf_power acpi_tad sch_fq_codel kyber_iosched msr parport_pc ppdev lp parport efi_pstore ip_tables x_tables autofs4 dm_crypt raid10 raid456 async_raid6_recov async_memcpy async_pq async_xor async_tx xor raid6_pq raid1 raid0 linear system76_io(OE) system76_acpi(OE) i915 drm_buddy ttm polyval_clmulni nvme ghash_clmulni_intel i2c_algo_bit sha1_ssse3 nvme_core drm_display_helper intel_lpss_pci spi_intel_pci nvme_keyring spi_intel intel_lpss cec nvme_auth idma64 rc_core video wmi surface_aggregator crc_itu_t pinctrl_icelake aesni_intel
> [   13.133733] CPU: 6 UID: 0 PID: 197 Comm: kworker/6:3 Tainted: G        W  OE       6.16.3-76061603-generic #202508231538~1758010842~22.04~85d2e57 PREEMPT(voluntary) 
> [   13.133736] Tainted: [W]=WARN, [O]=OOT_MODULE, [E]=UNSIGNED_MODULE
> [   13.133736] Hardware name: Microsoft Corporation Surface Laptop 3/Surface Laptop 3, BIOS 19.101.140 04/11/2024
> [   13.133738] Workqueue: events_freezable ieee80211_restart_work [mac80211]
> [   13.133776] RIP: 0010:drv_stop+0x11e/0x140 [mac80211]
> [   13.133809] Code: 85 c0 74 0f 48 8b 78 08 44 89 e2 48 89 de e8 89 60 06 00 65 ff 0d 52 01 11 ea 0f 85 2a ff ff ff 0f 1f 44 00 00 e9 20 ff ff ff <0f> 0b 5b 41 5c 41 5d 5d 31 c0 31 d2 31 f6 31 ff c3 cc cc cc cc 66
> [   13.133811] RSP: 0018:ffffcd2c40a37bb8 EFLAGS: 00010246
> [   13.133812] RAX: 0000000000000000 RBX: ffff8c97257e8920 RCX: 0000000000000000
> [   13.133813] RDX: 0000000000000000 RSI: 0000000000000000 RDI: 0000000000000000
> [   13.133814] RBP: ffffcd2c40a37bd0 R08: 0000000000000000 R09: 0000000000000000
> [   13.133815] R10: 0000000000000000 R11: 0000000000000000 R12: 0000000000000000
> [   13.133816] R13: 0000000000000000 R14: 0000000000000000 R15: 0000000000000000
> [   13.133817] FS:  0000000000000000(0000) GS:ffff8c9aaf96a000(0000) knlGS:0000000000000000
> [   13.133818] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
> [   13.133819] CR2: 000074b53c001368 CR3: 0000000120640005 CR4: 0000000000770ef0
> [   13.133820] PKRU: 55555554
> [   13.133821] Call Trace:
> [   13.133822]  <TASK>
> [   13.133824]  ieee80211_stop_device+0x7f/0x90 [mac80211]
> [   13.133877]  ieee80211_do_stop+0x7f7/0xb00 [mac80211]
> [   13.133918]  ? synchronize_rcu_expedited+0x1e6/0x220
> [   13.133922]  ? __pfx_autoremove_wake_function+0x10/0x10
> [   13.133925]  ieee80211_stop+0x6c/0x100 [mac80211]
> [   13.133967]  __dev_close_many+0x128/0x270
> [   13.133970]  dev_close_many+0x98/0x170
> [   13.133972]  netif_close+0x6e/0x90
> [   13.133974]  dev_close+0x3b/0xb0
> [   13.133977]  cfg80211_shutdown_all_interfaces+0x50/0x100 [cfg80211]
> [   13.134016]  ieee80211_restart_work+0x14f/0x190 [mac80211]
> [   13.134050]  process_one_work+0x18e/0x3e0
> [   13.134053]  worker_thread+0x2bd/0x3f0
> [   13.134056]  ? __pfx_worker_thread+0x10/0x10
> [   13.134058]  kthread+0x10a/0x230
> [   13.134060]  ? __pfx_kthread+0x10/0x10
> [   13.134062]  ret_from_fork+0x11e/0x140
> [   13.134065]  ? __pfx_kthread+0x10/0x10
> [   13.134067]  ret_from_fork_asm+0x1a/0x30
> [   13.134070]  </TASK>
> [   13.134070] ---[ end trace 0000000000000000 ]---
> [   13.330968] iwlwifi 0000:00:14.3: Failed to send recovery cmd blob was invalid 1
> [   13.331001] ------------[ cut here ]------------
> [   13.331003] WARNING: CPU: 1 PID: 794 at net/mac80211/util.c:2251 ieee80211_reconfig_disconnect+0x79/0x100 [mac80211]
> [   13.331070] Modules linked in: rfcomm cmac algif_hash algif_skcipher af_alg snd_seq_dummy snd_hrtimer overlay ip6t_REJECT nf_reject_ipv6 xt_hl ip6t_rt ipt_REJECT nf_reject_ipv4 xt_LOG nf_log_syslog nft_limit xt_limit xt_addrtype xt_tcpudp xt_conntrack bnep nf_conntrack nf_defrag_ipv6 nf_defrag_ipv4 zram nft_compat 842_decompress 842_compress lz4hc_compress lz4_compress snd_sof_pci_intel_icl snd_sof_pci_intel_cnl snd_sof_intel_hda_generic soundwire_intel snd_sof_intel_hda_sdw_bpt snd_sof_intel_hda_common snd_soc_hdac_hda snd_sof_intel_hda_mlink snd_sof_intel_hda snd_hda_codec_hdmi soundwire_cadence snd_sof_pci snd_sof_xtensa_dsp nf_tables snd_sof nfnetlink snd_sof_utils binfmt_misc snd_soc_acpi_intel_match snd_soc_acpi_intel_sdca_quirks soundwire_generic_allocation snd_soc_acpi soundwire_bus snd_hda_codec_realtek snd_soc_sdca joydev crc8 snd_hda_codec_generic snd_hda_scodec_component snd_soc_avs snd_soc_hda_codec snd_hda_ext_core intel_uncore_frequency intel_uncore_frequency_common snd_soc_core snd_compress ac97_bus
> [   13.331107]  snd_pcm_dmaengine snd_hda_intel snd_intel_dspcfg snd_intel_sdw_acpi snd_hda_codec snd_hda_core input_leds hid_multitouch snd_hwdep intel_tcc_cooling x86_pkg_temp_thermal snd_pcm intel_powerclamp hid_generic coretemp processor_thermal_device_pci_legacy snd_seq_midi iwlmvm snd_seq_midi_event processor_thermal_device surface_hid processor_thermal_wt_hint surface_platform_profile surface_hid_core nls_iso8859_1 kvm_intel snd_rawmidi platform_temperature_control intel_rapl_msr processor_thermal_rfim mei_pxp mei_hdcp hid surface_battery surface_charger platform_profile gpio_keys surface_gpe mac80211 snd_seq processor_thermal_rapl kvm libarc4 intel_rapl_common btusb cmdlinepart snd_seq_device processor_thermal_wt_req btrtl snd_timer irqbypass processor_thermal_power_floor spi_nor btintel rapl processor_thermal_mbox int3403_thermal intel_cstate snd iwlwifi intel_pmc_core btbcm soundcore mtd mei_me pmt_telemetry intel_wmi_thunderbolt btmtk int340x_thermal_zone surfacepro3_button int3400_thermal pmt_class bluetooth
> [   13.331146]  cfg80211 8250_dw mei intel_soc_dts_iosf mac_hid surface_hotplug intel_pmc_ssram_telemetry soc_button_array surface_aggregator_registry acpi_thermal_rel surface_acpi_notify acpi_pad intel_vsec dptf_power acpi_tad sch_fq_codel kyber_iosched msr parport_pc ppdev lp parport efi_pstore ip_tables x_tables autofs4 dm_crypt raid10 raid456 async_raid6_recov async_memcpy async_pq async_xor async_tx xor raid6_pq raid1 raid0 linear system76_io(OE) system76_acpi(OE) i915 drm_buddy ttm polyval_clmulni nvme ghash_clmulni_intel i2c_algo_bit sha1_ssse3 nvme_core drm_display_helper intel_lpss_pci spi_intel_pci nvme_keyring spi_intel intel_lpss cec nvme_auth idma64 rc_core video wmi surface_aggregator crc_itu_t pinctrl_icelake aesni_intel
> [   13.331184] CPU: 1 UID: 0 PID: 794 Comm: NetworkManager Tainted: G        W  OE       6.16.3-76061603-generic #202508231538~1758010842~22.04~85d2e57 PREEMPT(voluntary) 
> [   13.331187] Tainted: [W]=WARN, [O]=OOT_MODULE, [E]=UNSIGNED_MODULE
> [   13.331188] Hardware name: Microsoft Corporation Surface Laptop 3/Surface Laptop 3, BIOS 19.101.140 04/11/2024
> [   13.331189] RIP: 0010:ieee80211_reconfig_disconnect+0x79/0x100 [mac80211]
> [   13.331244] Code: c0 31 d2 31 f6 31 ff e9 55 5d 66 e8 41 f6 c4 40 74 2f 45 0f b6 ad ae 05 00 00 41 80 fd 01 0f 87 0f e6 07 00 41 83 e5 01 75 17 <0f> 0b 5b 41 5c 41 5d 41 5e 5d 31 c0 31 d2 31 f6 31 ff c3 cc cc cc
> [   13.331246] RSP: 0018:ffffcd2c42cab1e8 EFLAGS: 00010246
> [   13.331248] RAX: ffffffffc1600050 RBX: ffff8c972d47df08 RCX: ffff8c97257ea028
> [   13.331249] RDX: ffff8c972d47df08 RSI: 0000000000000040 RDI: ffff8c972d47df08
> [   13.331250] RBP: ffffcd2c42cab208 R08: 0000000000000000 R09: 0000000000000000
> [   13.331251] R10: 0000000000000000 R11: 0000000000000000 R12: 0000000000000040
> [   13.331252] R13: 0000000000000000 R14: 0000000000000001 R15: ffff8c97257e9ae8
> [   13.331252] FS:  00007e71e06e84c0(0000) GS:ffff8c9aaf6ea000(0000) knlGS:0000000000000000
> [   13.331254] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
> [   13.331255] CR2: 00007898f2dfdbb8 CR3: 0000000110dee002 CR4: 0000000000770ef0
> [   13.331256] PKRU: 55555554
> [   13.331257] Call Trace:
> [   13.331258]  <TASK>
> [   13.331261]  ieee80211_hw_restart_disconnect+0x13/0x20 [mac80211]
> [   13.331312]  iwl_mvm_disconnect_iterator+0x1f/0x30 [iwlmvm]
> [   13.331335]  __iterate_interfaces+0xa0/0x140 [mac80211]
> [   13.331385]  ? __pfx_iwl_mvm_disconnect_iterator+0x10/0x10 [iwlmvm]
> [   13.331406]  ? __pfx_iwl_mvm_disconnect_iterator+0x10/0x10 [iwlmvm]
> [   13.331424]  ieee80211_iterate_interfaces+0x3e/0x60 [mac80211]
> [   13.331473]  iwl_mvm_send_recovery_cmd+0x166/0x170 [iwlmvm]
> [   13.331507]  iwl_mvm_up+0x8ee/0xab0 [iwlmvm]
> [   13.331536]  __iwl_mvm_mac_start+0x115/0x1b0 [iwlmvm]
> [   13.331573]  iwl_mvm_mac_start+0x81/0x110 [iwlmvm]
> [   13.331597]  drv_start+0x52/0x120 [mac80211]
> [   13.331639]  ieee80211_do_open+0x301/0x740 [mac80211]
> [   13.331691]  ieee80211_open+0x6e/0xa0 [mac80211]
> [   13.331735]  __dev_open+0x136/0x300
> [   13.331739]  __dev_change_flags+0x1b9/0x230
> [   13.331741]  netif_change_flags+0x27/0x80
> [   13.331742]  do_setlink.constprop.0+0xb8a/0xec0
> [   13.331745]  ? psi_group_change+0x1f1/0x4f0
> [   13.331749]  ? set_next_task_idle+0x46/0x70
> [   13.331751]  ? ep_done_scan+0xe4/0x100
> [   13.331754]  __rtnl_newlink+0x2ef/0x3c0
> [   13.331756]  rtnl_newlink+0x4ad/0x920
> [   13.331758]  ? security_capable+0x7c/0x1f0
> [   13.331762]  ? __pfx_rtnl_newlink+0x10/0x10
> [   13.331763]  rtnetlink_rcv_msg+0x37b/0x450
> [   13.331765]  ? select_idle_sibling+0x18f/0xc80
> [   13.331768]  ? __pfx_rtnetlink_rcv_msg+0x10/0x10
> [   13.331769]  netlink_rcv_skb+0x59/0x110
> [   13.331773]  rtnetlink_rcv+0x15/0x30
> [   13.331775]  netlink_unicast+0x1e3/0x2e0
> [   13.331777]  netlink_sendmsg+0x214/0x470
> [   13.331779]  ____sys_sendmsg+0x3ab/0x3e0
> [   13.331782]  ___sys_sendmsg+0x99/0xf0
> [   13.331785]  __sys_sendmsg+0x8c/0x100
> [   13.331788]  __x64_sys_sendmsg+0x1d/0x30
> [   13.331791]  x64_sys_call+0x78e/0x2550
> [   13.331793]  do_syscall_64+0x80/0xcb0
> [   13.331797]  ? __x64_sys_futex+0x94/0x200
> [   13.331799]  ? __wake_up_common+0x79/0xb0
> [   13.331802]  ? arch_exit_to_user_mode_prepare.constprop.0+0xd/0xc0
> [   13.331804]  ? do_syscall_64+0xb6/0xcb0
> [   13.331806]  ? rw_verify_area+0x53/0x190
> [   13.331808]  ? vfs_write+0x10a/0x480
> [   13.331811]  ? arch_exit_to_user_mode_prepare.constprop.0+0xd/0xc0
> [   13.331813]  ? do_syscall_64+0xb6/0xcb0
> [   13.331815]  ? ksys_write+0xdb/0xf0
> [   13.331817]  ? arch_exit_to_user_mode_prepare.constprop.0+0xd/0xc0
> [   13.331819]  ? do_syscall_64+0xb6/0xcb0
> [   13.331821]  ? arch_exit_to_user_mode_prepare.constprop.0+0xd/0xc0
> [   13.331823]  ? irqentry_exit_to_user_mode+0x2d/0x1d0
> [   13.331825]  ? clear_bhb_loop+0x30/0x80
> [   13.331828]  ? clear_bhb_loop+0x30/0x80
> [   13.331829]  entry_SYSCALL_64_after_hwframe+0x76/0x7e
> [   13.331831] RIP: 0033:0x7e71e172799d
> [   13.331833] Code: 28 89 54 24 1c 48 89 74 24 10 89 7c 24 08 e8 6a 90 f6 ff 8b 54 24 1c 48 8b 74 24 10 41 89 c0 8b 7c 24 08 b8 2e 00 00 00 0f 05 <48> 3d 00 f0 ff ff 77 33 44 89 c7 48 89 44 24 08 e8 ae 90 f6 ff 48
> [   13.331834] RSP: 002b:00007ffe3f647760 EFLAGS: 00000293 ORIG_RAX: 000000000000002e
> [   13.331836] RAX: ffffffffffffffda RBX: 0000000000000012 RCX: 00007e71e172799d
> [   13.331837] RDX: 0000000000000000 RSI: 00007ffe3f6477a0 RDI: 000000000000000c
> [   13.331838] RBP: 00005f0e6645c030 R08: 0000000000000000 R09: 0000000000000000
> [   13.331839] R10: 0000000000000000 R11: 0000000000000293 R12: 0000000000000000
> [   13.331840] R13: 00007ffe3f6478f0 R14: 00007ffe3f6478ec R15: 0000000000000000
> [   13.331842]  </TASK>
> [   13.331842] ---[ end trace 0000000000000000 ]---
> [   13.331866] ------------[ cut here ]------------
> [   13.331867] WARNING: CPU: 1 PID: 794 at drivers/net/wireless/intel/iwlwifi/mvm/mac-ctxt.c:274 iwl_mvm_mac_ctxt_init+0x224/0x240 [iwlmvm]
> [   13.331892] Modules linked in: rfcomm cmac algif_hash algif_skcipher af_alg snd_seq_dummy snd_hrtimer overlay ip6t_REJECT nf_reject_ipv6 xt_hl ip6t_rt ipt_REJECT nf_reject_ipv4 xt_LOG nf_log_syslog nft_limit xt_limit xt_addrtype xt_tcpudp xt_conntrack bnep nf_conntrack nf_defrag_ipv6 nf_defrag_ipv4 zram nft_compat 842_decompress 842_compress lz4hc_compress lz4_compress snd_sof_pci_intel_icl snd_sof_pci_intel_cnl snd_sof_intel_hda_generic soundwire_intel snd_sof_intel_hda_sdw_bpt snd_sof_intel_hda_common snd_soc_hdac_hda snd_sof_intel_hda_mlink snd_sof_intel_hda snd_hda_codec_hdmi soundwire_cadence snd_sof_pci snd_sof_xtensa_dsp nf_tables snd_sof nfnetlink snd_sof_utils binfmt_misc snd_soc_acpi_intel_match snd_soc_acpi_intel_sdca_quirks soundwire_generic_allocation snd_soc_acpi soundwire_bus snd_hda_codec_realtek snd_soc_sdca joydev crc8 snd_hda_codec_generic snd_hda_scodec_component snd_soc_avs snd_soc_hda_codec snd_hda_ext_core intel_uncore_frequency intel_uncore_frequency_common snd_soc_core snd_compress ac97_bus
> [   13.331922]  snd_pcm_dmaengine snd_hda_intel snd_intel_dspcfg snd_intel_sdw_acpi snd_hda_codec snd_hda_core input_leds hid_multitouch snd_hwdep intel_tcc_cooling x86_pkg_temp_thermal snd_pcm intel_powerclamp hid_generic coretemp processor_thermal_device_pci_legacy snd_seq_midi iwlmvm snd_seq_midi_event processor_thermal_device surface_hid processor_thermal_wt_hint surface_platform_profile surface_hid_core nls_iso8859_1 kvm_intel snd_rawmidi platform_temperature_control intel_rapl_msr processor_thermal_rfim mei_pxp mei_hdcp hid surface_battery surface_charger platform_profile gpio_keys surface_gpe mac80211 snd_seq processor_thermal_rapl kvm libarc4 intel_rapl_common btusb cmdlinepart snd_seq_device processor_thermal_wt_req btrtl snd_timer irqbypass processor_thermal_power_floor spi_nor btintel rapl processor_thermal_mbox int3403_thermal intel_cstate snd iwlwifi intel_pmc_core btbcm soundcore mtd mei_me pmt_telemetry intel_wmi_thunderbolt btmtk int340x_thermal_zone surfacepro3_button int3400_thermal pmt_class bluetooth
> [   13.331953]  cfg80211 8250_dw mei intel_soc_dts_iosf mac_hid surface_hotplug intel_pmc_ssram_telemetry soc_button_array surface_aggregator_registry acpi_thermal_rel surface_acpi_notify acpi_pad intel_vsec dptf_power acpi_tad sch_fq_codel kyber_iosched msr parport_pc ppdev lp parport efi_pstore ip_tables x_tables autofs4 dm_crypt raid10 raid456 async_raid6_recov async_memcpy async_pq async_xor async_tx xor raid6_pq raid1 raid0 linear system76_io(OE) system76_acpi(OE) i915 drm_buddy ttm polyval_clmulni nvme ghash_clmulni_intel i2c_algo_bit sha1_ssse3 nvme_core drm_display_helper intel_lpss_pci spi_intel_pci nvme_keyring spi_intel intel_lpss cec nvme_auth idma64 rc_core video wmi surface_aggregator crc_itu_t pinctrl_icelake aesni_intel
> [   13.331982] CPU: 1 UID: 0 PID: 794 Comm: NetworkManager Tainted: G        W  OE       6.16.3-76061603-generic #202508231538~1758010842~22.04~85d2e57 PREEMPT(voluntary) 
> [   13.331984] Tainted: [W]=WARN, [O]=OOT_MODULE, [E]=UNSIGNED_MODULE
> [   13.331985] Hardware name: Microsoft Corporation Surface Laptop 3/Surface Laptop 3, BIOS 19.101.140 04/11/2024
> [   13.331986] RIP: 0010:iwl_mvm_mac_ctxt_init+0x224/0x240 [iwlmvm]
> [   13.332008] Code: 49 8b 3c 24 48 c7 c2 58 3d 5e c1 31 f6 e8 d4 c1 52 ff eb 96 f3 48 0f bc c0 89 83 58 07 00 00 83 f8 04 0f 85 e0 fe ff ff eb d6 <0f> 0b b8 f0 ff ff ff e9 2d ff ff ff e8 1b 09 33 e8 66 66 2e 0f 1f
> [   13.332009] RSP: 0018:ffffcd2c42cab380 EFLAGS: 00010202
> [   13.332011] RAX: 0000000000000050 RBX: ffff8c972d47df08 RCX: 0000000000000000
> [   13.332012] RDX: 0000000000000000 RSI: 0000000000000000 RDI: 0000000000000000
> [   13.332012] RBP: ffffcd2c42cab3c8 R08: 0000000000000000 R09: 0000000000000000
> [   13.332013] R10: 0000000000000000 R11: 0000000000000000 R12: ffff8c97257ea028
> [   13.332014] R13: 0000000000000000 R14: ffff8c97257ea058 R15: ffff8c972d47df08
> [   13.332015] FS:  00007e71e06e84c0(0000) GS:ffff8c9aaf6ea000(0000) knlGS:0000000000000000
> [   13.332016] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
> [   13.332017] CR2: 00007898f2dfdbb8 CR3: 0000000110dee002 CR4: 0000000000770ef0
> [   13.332018] PKRU: 55555554
> [   13.332019] Call Trace:
> [   13.332020]  <TASK>
> [   13.332021]  iwl_mvm_mld_mac_add_interface+0xc5/0x440 [iwlmvm]
> [   13.332045]  drv_add_interface+0x51/0x290 [mac80211]
> [   13.332082]  ieee80211_do_open+0x5c7/0x740 [mac80211]
> [   13.332126]  ieee80211_open+0x6e/0xa0 [mac80211]
> [   13.332168]  __dev_open+0x136/0x300
> [   13.332170]  __dev_change_flags+0x1b9/0x230
> [   13.332172]  netif_change_flags+0x27/0x80
> [   13.332174]  do_setlink.constprop.0+0xb8a/0xec0
> [   13.332176]  ? psi_group_change+0x1f1/0x4f0
> [   13.332178]  ? set_next_task_idle+0x46/0x70
> [   13.332180]  ? ep_done_scan+0xe4/0x100
> [   13.332182]  __rtnl_newlink+0x2ef/0x3c0
> [   13.332184]  rtnl_newlink+0x4ad/0x920
> [   13.332186]  ? security_capable+0x7c/0x1f0
> [   13.332189]  ? __pfx_rtnl_newlink+0x10/0x10
> [   13.332190]  rtnetlink_rcv_msg+0x37b/0x450
> [   13.332192]  ? select_idle_sibling+0x18f/0xc80
> [   13.332194]  ? __pfx_rtnetlink_rcv_msg+0x10/0x10
> [   13.332195]  netlink_rcv_skb+0x59/0x110
> [   13.332198]  rtnetlink_rcv+0x15/0x30
> [   13.332200]  netlink_unicast+0x1e3/0x2e0
> [   13.332202]  netlink_sendmsg+0x214/0x470
> [   13.332203]  ____sys_sendmsg+0x3ab/0x3e0
> [   13.332206]  ___sys_sendmsg+0x99/0xf0
> [   13.332210]  __sys_sendmsg+0x8c/0x100
> [   13.332213]  __x64_sys_sendmsg+0x1d/0x30
> [   13.332215]  x64_sys_call+0x78e/0x2550
> [   13.332217]  do_syscall_64+0x80/0xcb0
> [   13.332219]  ? __x64_sys_futex+0x94/0x200
> [   13.332221]  ? __wake_up_common+0x79/0xb0
> [   13.332223]  ? arch_exit_to_user_mode_prepare.constprop.0+0xd/0xc0
> [   13.332225]  ? do_syscall_64+0xb6/0xcb0
> [   13.332227]  ? rw_verify_area+0x53/0x190
> [   13.332229]  ? vfs_write+0x10a/0x480
> [   13.332231]  ? arch_exit_to_user_mode_prepare.constprop.0+0xd/0xc0
> [   13.332233]  ? do_syscall_64+0xb6/0xcb0
> [   13.332235]  ? ksys_write+0xdb/0xf0
> [   13.332237]  ? arch_exit_to_user_mode_prepare.constprop.0+0xd/0xc0
> [   13.332239]  ? do_syscall_64+0xb6/0xcb0
> [   13.332247]  ? arch_exit_to_user_mode_prepare.constprop.0+0xd/0xc0
> [   13.332249]  ? irqentry_exit_to_user_mode+0x2d/0x1d0
> [   13.332250]  ? clear_bhb_loop+0x30/0x80
> [   13.332252]  ? clear_bhb_loop+0x30/0x80
> [   13.332254]  entry_SYSCALL_64_after_hwframe+0x76/0x7e
> [   13.332255] RIP: 0033:0x7e71e172799d
> [   13.332256] Code: 28 89 54 24 1c 48 89 74 24 10 89 7c 24 08 e8 6a 90 f6 ff 8b 54 24 1c 48 8b 74 24 10 41 89 c0 8b 7c 24 08 b8 2e 00 00 00 0f 05 <48> 3d 00 f0 ff ff 77 33 44 89 c7 48 89 44 24 08 e8 ae 90 f6 ff 48
> [   13.332257] RSP: 002b:00007ffe3f647760 EFLAGS: 00000293 ORIG_RAX: 000000000000002e
> [   13.332259] RAX: ffffffffffffffda RBX: 0000000000000012 RCX: 00007e71e172799d
> [   13.332260] RDX: 0000000000000000 RSI: 00007ffe3f6477a0 RDI: 000000000000000c
> [   13.332261] RBP: 00005f0e6645c030 R08: 0000000000000000 R09: 0000000000000000
> [   13.332262] R10: 0000000000000000 R11: 0000000000000293 R12: 0000000000000000
> [   13.332263] R13: 00007ffe3f6478f0 R14: 00007ffe3f6478ec R15: 0000000000000000
> [   13.332264]  </TASK>
> [   13.332265] ---[ end trace 0000000000000000 ]---
> [   14.038001] debugfs: File 'netdev:wlp0s20f3' in directory 'iwlmvm' already present!
> [   14.038007] debugfs: Directory 'iwlmvm' with parent 'netdev:wlp0s20f3' already present!
> [   14.038009] iwlwifi 0000:00:14.3: Failed to create debugfs directory under netdev:wlp0s20f3
> [   14.053026] wlp0s20f3: authenticate with 14:16:9d:b5:93:61 (local address=c8:34:8e:0b:fe:b2)
> [   14.053922] wlp0s20f3: send auth to 14:16:9d:b5:93:61 (try 1/3)
> [   14.089465] wlp0s20f3: authenticated
> [   14.090534] wlp0s20f3: associate with 14:16:9d:b5:93:61 (try 1/3)
> [   14.094590] wlp0s20f3: RX AssocResp from 14:16:9d:b5:93:61 (capab=0x1411 status=0 aid=2)
> [   14.102047] wlp0s20f3: associated
> [   14.259942] wlp0s20f3: Limiting TX power to 20 (20 - 0) dBm as advertised by 14:16:9d:b5:93:61
> [   14.385541] Initializing XFRM netlink socket
> [   14.518212] kauditd_printk_skb: 26 callbacks suppressed
> [   14.518215] audit: type=1400 audit(1758621248.380:38): apparmor="STATUS" operation="profile_load" profile="unconfined" name="docker-default" pid=1470 comm="apparmor_parser"
> [   14.575925] evm: overlay not supported
> [   14.842405] bridge: filtering via arp/ip/ip6tables is no longer available by default. Update your scripts to load br_netfilter if you need this.
> [   14.880299] [UFW BLOCK] IN=wlp0s20f3 OUT= MAC=c8:34:8e:0b:fe:b2:a0:b4:39:16:b1:02:08:00 SRC=84.215.96.194 DST=158.37.231.201 LEN=152 TOS=0x00 PREC=0x00 TTL=49 ID=40721 DF PROTO=UDP SPT=4018 DPT=41641 LEN=132 
> [   15.193623] br-c5d2b3137422: port 1(vethec2b6fd) entered blocking state
> [   15.193631] br-c5d2b3137422: port 1(vethec2b6fd) entered disabled state
> [   15.193646] vethec2b6fd: entered allmulticast mode
> [   15.193961] vethec2b6fd: entered promiscuous mode
> [   15.226467] eth0: renamed from vethbbb3e44
> [   15.228115] br-c5d2b3137422: port 1(vethec2b6fd) entered blocking state
> [   15.228122] br-c5d2b3137422: port 1(vethec2b6fd) entered forwarding state
> [   15.486788] qemu: entered promiscuous mode
> [   15.488120] dockerbridge: port 1(qemu) entered blocking state
> [   15.488123] dockerbridge: port 1(qemu) entered disabled state
> [   15.488139] qemu: entered allmulticast mode
> [   15.762050] dockerbridge: port 1(qemu) entered blocking state
> [   15.762058] dockerbridge: port 1(qemu) entered forwarding state
> [   20.067600] rfkill: input handler enabled
> [   20.915335] nvme nvme0: using unchecked data buffer
> [   25.035896] rfkill: input handler disabled
> [   26.438384] warning: `ThreadPoolForeg' uses wireless extensions which will stop working for Wi-Fi 7 hardware; use nl80211
> [   36.318745] [UFW BLOCK] IN=wlp0s20f3 OUT= MAC=01:00:5e:00:00:01:a0:b4:39:16:b1:02:08:00 SRC=158.37.224.1 DST=224.0.0.1 LEN=32 TOS=0x00 PREC=0xC0 TTL=1 ID=21297 PROTO=2 
> [   36.574501] [UFW BLOCK] IN=wlp0s20f3 OUT= MAC=01:00:5e:00:00:01:a0:b4:39:16:b1:02:08:00 SRC=158.37.232.1 DST=224.0.0.1 LEN=32 TOS=0x00 PREC=0xC0 TTL=1 ID=21302 PROTO=2 
> [   36.995459] [UFW BLOCK] IN=wlp0s20f3 OUT= MAC=c8:34:8e:0b:fe:b2:a0:b4:39:16:b1:02:08:00 SRC=104.18.3.166 DST=158.37.231.201 LEN=1064 TOS=0x00 PREC=0x00 TTL=57 ID=3306 DF PROTO=TCP SPT=443 DPT=50358 WINDOW=16 RES=0x00 ACK URGP=0 
> [   43.227685] dptf_power INT3407:00: Unsupported event [0x82]
> ```

> [!NOTE]- Logg en gang det bare forsvant
> ```LOG
> [11064.816905] [UFW BLOCK] IN=wlp0s20f3 OUT= MAC=c8:34:8e:0b:fe:b2:52:54:00:c0:47:7c:08:00 SRC=192.168.0.13 DST=192.168.0.62 LEN=350 TOS=0x00 PREC=0x00 TTL=64 ID=48897 DF PROTO=UDP SPT=53733 DPT=47599 LEN=330 
> [11088.437685] [UFW BLOCK] IN=wlp0s20f3 OUT= MAC=c8:34:8e:0b:fe:b2:52:54:00:c0:47:7c:08:00 SRC=192.168.0.13 DST=192.168.0.62 LEN=350 TOS=0x00 PREC=0x00 TTL=64 ID=55762 DF PROTO=UDP SPT=53733 DPT=56576 LEN=330 
> [11114.125681] [UFW BLOCK] IN=wlp0s20f3 OUT= MAC=c8:34:8e:0b:fe:b2:d4:6e:0e:a4:19:54:08:00 SRC=192.168.0.13 DST=192.168.0.62 LEN=350 TOS=0x00 PREC=0x00 TTL=64 ID=1918 DF PROTO=UDP SPT=53733 DPT=48937 LEN=330 
> [11136.103002] [UFW BLOCK] IN=wlp0s20f3 OUT= MAC=c8:34:8e:0b:fe:b2:52:54:00:c0:47:7c:08:00 SRC=192.168.0.13 DST=192.168.0.62 LEN=350 TOS=0x00 PREC=0x00 TTL=64 ID=6168 DF PROTO=UDP SPT=53733 DPT=40446 LEN=330
> [11136.606622] iwlwifi 0000:00:14.3: Microcode SW error detected. Restarting 0x0.
> [11136.606733] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [11136.606745] iwlwifi 0000:00:14.3: Transport status: 0x0000024A, valid: 6
> [11136.606749] iwlwifi 0000:00:14.3: Loaded firmware version: 77.2753b721.0 Qu-c0-hr-b0-77.ucode
> [11136.606752] iwlwifi 0000:00:14.3: 0x00000091 | ADVANCED_SYSASSERT          
> [11136.606756] iwlwifi 0000:00:14.3: 0x0080A200 | trm_hw_status0
> [11136.606759] iwlwifi 0000:00:14.3: 0x00000000 | trm_hw_status1
> [11136.606761] iwlwifi 0000:00:14.3: 0x004C95A2 | branchlink2
> [11136.606763] iwlwifi 0000:00:14.3: 0x0000804C | interruptlink1
> [11136.606766] iwlwifi 0000:00:14.3: 0x0000804C | interruptlink2
> [11136.606768] iwlwifi 0000:00:14.3: 0x000080D2 | data1
> [11136.606771] iwlwifi 0000:00:14.3: 0x00010000 | data2
> [11136.606773] iwlwifi 0000:00:14.3: 0x00000000 | data3
> [11136.606776] iwlwifi 0000:00:14.3: 0x65C160CD | beacon time
> [11136.606778] iwlwifi 0000:00:14.3: 0x00000000 | tsf low
> [11136.606781] iwlwifi 0000:00:14.3: 0x00000000 | tsf hi
> [11136.606783] iwlwifi 0000:00:14.3: 0x00000000 | time gp1
> [11136.606785] iwlwifi 0000:00:14.3: 0x6CEE5668 | time gp2
> [11136.606788] iwlwifi 0000:00:14.3: 0x00000001 | uCode revision type
> [11136.606790] iwlwifi 0000:00:14.3: 0x0000004D | uCode version major
> [11136.606793] iwlwifi 0000:00:14.3: 0x2753B721 | uCode version minor
> [11136.606795] iwlwifi 0000:00:14.3: 0x00000332 | hw version
> [11136.606798] iwlwifi 0000:00:14.3: 0x00C89002 | board version
> [11136.606800] iwlwifi 0000:00:14.3: 0x80F2F400 | hcmd
> [11136.606803] iwlwifi 0000:00:14.3: 0x66F60000 | isr0
> [11136.606805] iwlwifi 0000:00:14.3: 0x01048000 | isr1
> [11136.606808] iwlwifi 0000:00:14.3: 0x08F0001A | isr2
> [11136.606810] iwlwifi 0000:00:14.3: 0x00C3028D | isr3
> [11136.606812] iwlwifi 0000:00:14.3: 0x00000000 | isr4
> [11136.606815] iwlwifi 0000:00:14.3: 0x03DC001C | last cmd Id
> [11136.606817] iwlwifi 0000:00:14.3: 0x000080D2 | wait_event
> [11136.606828] iwlwifi 0000:00:14.3: 0x00004288 | l2p_control
> [11136.606830] iwlwifi 0000:00:14.3: 0x0001D414 | l2p_duration
> [11136.606833] iwlwifi 0000:00:14.3: 0x000003BF | l2p_mhvalid
> [11136.606835] iwlwifi 0000:00:14.3: 0x000000E7 | l2p_addr_match
> [11136.606838] iwlwifi 0000:00:14.3: 0x00000000 | lmpm_pmg_sel
> [11136.606840] iwlwifi 0000:00:14.3: 0x00000000 | timestamp
> [11136.606842] iwlwifi 0000:00:14.3: 0x0000785C | flow_handler
> [11136.606965] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [11136.606970] iwlwifi 0000:00:14.3: Transport status: 0x0000024A, valid: 7
> [11136.606976] iwlwifi 0000:00:14.3: 0x20000070 | NMI_INTERRUPT_LMAC_FATAL
> [11136.606981] iwlwifi 0000:00:14.3: 0x00000000 | umac branchlink1
> [11136.606985] iwlwifi 0000:00:14.3: 0x804561EA | umac branchlink2
> [11136.606990] iwlwifi 0000:00:14.3: 0x8047372E | umac interruptlink1
> [11136.607003] iwlwifi 0000:00:14.3: 0x8047372E | umac interruptlink2
> [11136.607008] iwlwifi 0000:00:14.3: 0x00000400 | umac data1
> [11136.607014] iwlwifi 0000:00:14.3: 0x8047372E | umac data2
> [11136.607019] iwlwifi 0000:00:14.3: 0x00000000 | umac data3
> [11136.607035] iwlwifi 0000:00:14.3: 0x0000004D | umac major
> [11136.607040] iwlwifi 0000:00:14.3: 0x2753B721 | umac minor
> [11136.607045] iwlwifi 0000:00:14.3: 0x6CEE56FE | frame pointer
> [11136.607049] iwlwifi 0000:00:14.3: 0xC0886260 | stack pointer
> [11136.607053] iwlwifi 0000:00:14.3: 0x0053010C | last host cmd
> [11136.607064] iwlwifi 0000:00:14.3: 0x00000000 | isr status reg
> [11136.607104] iwlwifi 0000:00:14.3: IML/ROM dump:
> [11136.607108] iwlwifi 0000:00:14.3: 0x00000003 | IML/ROM error/state
> [11136.607147] iwlwifi 0000:00:14.3: 0x00005BEB | IML/ROM data1
> [11136.607186] iwlwifi 0000:00:14.3: 0x00000080 | IML/ROM WFPM_AUTH_KEY_0
> [11136.607221] iwlwifi 0000:00:14.3: Fseq Registers:
> [11136.607254] iwlwifi 0000:00:14.3: 0x60000000 | FSEQ_ERROR_CODE
> [11136.607287] iwlwifi 0000:00:14.3: 0x80290033 | FSEQ_TOP_INIT_VERSION
> [11136.607320] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_CNVIO_INIT_VERSION
> [11136.607355] iwlwifi 0000:00:14.3: 0x0000A492 | FSEQ_OTP_VERSION
> [11136.607413] iwlwifi 0000:00:14.3: 0x00000003 | FSEQ_TOP_CONTENT_VERSION
> [11136.607447] iwlwifi 0000:00:14.3: 0x4552414E | FSEQ_ALIVE_TOKEN
> [11136.607480] iwlwifi 0000:00:14.3: 0x02000300 | FSEQ_CNVI_ID
> [11136.607512] iwlwifi 0000:00:14.3: 0x01300504 | FSEQ_CNVR_ID
> [11136.607545] iwlwifi 0000:00:14.3: 0x02000300 | CNVI_AUX_MISC_CHIP
> [11136.607579] iwlwifi 0000:00:14.3: 0x01300504 | CNVR_AUX_MISC_CHIP
> [11136.607614] iwlwifi 0000:00:14.3: 0x05B0905B | CNVR_SCU_SD_REGS_SD_REG_DIG_DCDC_VTRIM
> [11136.607648] iwlwifi 0000:00:14.3: 0x0000025B | CNVR_SCU_SD_REGS_SD_REG_ACTIVE_VDIG_MIRROR
> [11136.607681] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_PREV_CNVIO_INIT_VERSION
> [11136.607712] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_WIFI_FSEQ_VERSION
> [11136.607748] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_BT_FSEQ_VERSION
> [11136.607781] iwlwifi 0000:00:14.3: 0x00000136 | FSEQ_CLASS_TP_VERSION
> [11136.607823] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0x8047323c
> [11136.607856] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xd0
> [11136.607910] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 4 fired (delay=0ms).
> [11136.625936] iwlwifi 0000:00:14.3: Device error - reprobe!
> [11136.639424] iwlwifi 0000:00:14.3: LED command failed: -5
> [11136.639444] iwlwifi 0000:00:14.3: LED command failed: -5
> [11136.661518] iwlwifi 0000:00:14.3: Failed to send LINK_CONFIG_CMD (action:3): -5
> [11136.661525] iwlwifi 0000:00:14.3: Failed to send MAC_CONFIG_CMD (action:3): -5
> [11136.661529] iwlwifi 0000:00:14.3: mcast filter cmd error. ret=-5
> [11136.661530] iwlwifi 0000:00:14.3: Failed to synchronize multicast groups update
> [11136.661549] wlp0s20f3: deauthenticating from d4:6e:0e:a4:19:53 by local choice (Reason: 3=DEAUTH_LEAVING)
> [11136.661581] iwlwifi 0000:00:14.3: Failed to send flush command (-5)
> [11136.661583] iwlwifi 0000:00:14.3: flush request fail
> [11136.661605] iwlwifi 0000:00:14.3: Failed to send MAC_CONFIG_CMD (action:2): -5
> [11136.661606] iwlwifi 0000:00:14.3: failed to update MAC c8:34:8e:0b:fe:b2
> [11136.661608] iwlwifi 0000:00:14.3: Failed to synchronize multicast groups update
> [11136.661613] iwlwifi 0000:00:14.3: Failed to send LINK_CONFIG_CMD (action:2): -5
> [11136.661614] iwlwifi 0000:00:14.3: failed to update link
> [11136.661615] iwlwifi 0000:00:14.3: Failed to send MAC_CONFIG_CMD (action:2): -5
> [11136.661616] iwlwifi 0000:00:14.3: failed to update MAC c8:34:8e:0b:fe:b2
> [11136.661618] iwlwifi 0000:00:14.3: failed to update power mode
> [11136.661627] iwlwifi 0000:00:14.3: Failed to trigger RX queues sync (-5)
> [11136.661644] iwlwifi 0000:00:14.3: Failed to send flush command (-5)
> [11136.661645] iwlwifi 0000:00:14.3: flush request fail
> [11136.661650] iwlwifi 0000:00:14.3: Failed to send rate scale config (-5)
> [11136.661662] wlp0s20f3: failed to remove key (0, d4:6e:0e:a4:19:53) from hardware (-5)
> [11136.661685] iwlwifi 0000:00:14.3: Failed to send flush command (-5)
> [11136.661734] iwlwifi 0000:00:14.3: Failed to send LINK_CONFIG_CMD (action:2): -5
> [11136.661736] iwlwifi 0000:00:14.3: Failed to send LINK_CONFIG_CMD (action:3): -5
> [11136.661739] iwlwifi 0000:00:14.3: PHY ctxt cmd error. ret=-5
> [11136.661753] wlp0s20f3: failed to remove key (1, ff:ff:ff:ff:ff:ff) from hardware (-5)
> [11136.671627] iwlwifi 0000:00:14.3: Failed to send LINK_CONFIG_CMD (action:3): -5
> [11136.671634] iwlwifi 0000:00:14.3: Failed to send MAC_CONFIG_CMD (action:3): -5
> [11136.704487] iwlwifi 0000:00:14.3: Unregistering PHC clock: iwlwifi-PTP, with index: 0
> [11136.817088] iwlwifi 0000:00:14.3: Detected crf-id 0x3617, cnv-id 0x2000300 wfpm id 0x80000000
> [11136.817108] iwlwifi 0000:00:14.3: PCI dev 34f0/0074, rev=0x332, rfid=0x10a100
> [11136.817110] iwlwifi 0000:00:14.3: Detected Intel(R) Wi-Fi 6 AX201 160MHz
> [11136.826248] iwlwifi 0000:00:14.3: TLV_FW_FSEQ_VERSION: FSEQ Version: 89.3.35.37
> [11136.827485] iwlwifi 0000:00:14.3: loaded firmware version 77.2753b721.0 Qu-c0-hr-b0-77.ucode op_mode iwlmvm
> [11138.884498] iwlwifi 0000:00:14.3: SecBoot CPU1 Status: 0x588e, CPU2 Status: 0x3
> [11138.884542] iwlwifi 0000:00:14.3: WFPM_LMAC1_PD_NOTIFICATION: 0x0
> [11138.884580] iwlwifi 0000:00:14.3: HPM_SECONDARY_DEVICE_STATE: 0x42
> [11138.884608] iwlwifi 0000:00:14.3: WFPM_MAC_OTP_CFG7_ADDR: 0x0
> [11138.884636] iwlwifi 0000:00:14.3: WFPM_MAC_OTP_CFG7_DATA: 0x0
> [11138.884639] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0xa05c18
> [11138.884643] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xa05c1c
> [11138.884647] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [11138.884764] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [11138.884768] iwlwifi 0000:00:14.3: Transport status: 0x00000042, valid: 6
> [11138.884773] iwlwifi 0000:00:14.3: Loaded firmware version: 77.2753b721.0 Qu-c0-hr-b0-77.ucode
> [11138.884778] iwlwifi 0000:00:14.3: 0x00000090 | ADVANCED_SYSASSERT          
> [11138.884784] iwlwifi 0000:00:14.3: 0x000022F0 | trm_hw_status0
> [11138.884788] iwlwifi 0000:00:14.3: 0x00000000 | trm_hw_status1
> [11138.884792] iwlwifi 0000:00:14.3: 0x004C95A2 | branchlink2
> [11138.884796] iwlwifi 0000:00:14.3: 0x004B1D1E | interruptlink1
> [11138.884800] iwlwifi 0000:00:14.3: 0x004B1D1E | interruptlink2
> [11138.884803] iwlwifi 0000:00:14.3: 0x00014F4A | data1
> [11138.884807] iwlwifi 0000:00:14.3: 0x00000000 | data2
> [11138.884811] iwlwifi 0000:00:14.3: 0x00000000 | data3
> [11138.884815] iwlwifi 0000:00:14.3: 0x00000000 | beacon time
> [11138.884819] iwlwifi 0000:00:14.3: 0x00000000 | tsf low
> [11138.884823] iwlwifi 0000:00:14.3: 0x00000000 | tsf hi
> [11138.884827] iwlwifi 0000:00:14.3: 0x00000000 | time gp1
> [11138.884830] iwlwifi 0000:00:14.3: 0x0003C431 | time gp2
> [11138.884834] iwlwifi 0000:00:14.3: 0x00000001 | uCode revision type
> [11138.884838] iwlwifi 0000:00:14.3: 0x0000004D | uCode version major
> [11138.884842] iwlwifi 0000:00:14.3: 0x2753B721 | uCode version minor
> [11138.884846] iwlwifi 0000:00:14.3: 0x00000332 | hw version
> [11138.884850] iwlwifi 0000:00:14.3: 0x18C89002 | board version
> [11138.884854] iwlwifi 0000:00:14.3: 0x00000000 | hcmd
> [11138.884858] iwlwifi 0000:00:14.3: 0x00020000 | isr0
> [11138.884862] iwlwifi 0000:00:14.3: 0x00000000 | isr1
> [11138.884866] iwlwifi 0000:00:14.3: 0x08F00002 | isr2
> [11138.884870] iwlwifi 0000:00:14.3: 0x00C0001C | isr3
> [11138.884874] iwlwifi 0000:00:14.3: 0x00000000 | isr4
> [11138.884878] iwlwifi 0000:00:14.3: 0x00000000 | last cmd Id
> [11138.884881] iwlwifi 0000:00:14.3: 0x00014F4A | wait_event
> [11138.884885] iwlwifi 0000:00:14.3: 0x00000000 | l2p_control
> [11138.884889] iwlwifi 0000:00:14.3: 0x00000000 | l2p_duration
> [11138.884893] iwlwifi 0000:00:14.3: 0x00000000 | l2p_mhvalid
> [11138.884896] iwlwifi 0000:00:14.3: 0x00000000 | l2p_addr_match
> [11138.884900] iwlwifi 0000:00:14.3: 0x0000004B | lmpm_pmg_sel
> [11138.884904] iwlwifi 0000:00:14.3: 0x00000000 | timestamp
> [11138.884908] iwlwifi 0000:00:14.3: 0x0000F81C | flow_handler
> [11138.884968] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [11138.884971] iwlwifi 0000:00:14.3: Transport status: 0x00000042, valid: 7
> [11138.884976] iwlwifi 0000:00:14.3: 0x20000070 | NMI_INTERRUPT_LMAC_FATAL
> [11138.884980] iwlwifi 0000:00:14.3: 0x00000000 | umac branchlink1
> [11138.884984] iwlwifi 0000:00:14.3: 0x804561EA | umac branchlink2
> [11138.884988] iwlwifi 0000:00:14.3: 0x8047372E | umac interruptlink1
> [11138.884992] iwlwifi 0000:00:14.3: 0x80473240 | umac interruptlink2
> [11138.884996] iwlwifi 0000:00:14.3: 0x00000400 | umac data1
> [11138.885000] iwlwifi 0000:00:14.3: 0x80473240 | umac data2
> [11138.885004] iwlwifi 0000:00:14.3: 0x00000000 | umac data3
> [11138.885008] iwlwifi 0000:00:14.3: 0x0000004D | umac major
> [11138.885012] iwlwifi 0000:00:14.3: 0x2753B721 | umac minor
> [11138.885015] iwlwifi 0000:00:14.3: 0x0003C4A1 | frame pointer
> [11138.885019] iwlwifi 0000:00:14.3: 0xC0887EE4 | stack pointer
> [11138.885023] iwlwifi 0000:00:14.3: 0x00000000 | last host cmd
> [11138.885027] iwlwifi 0000:00:14.3: 0x00200040 | isr status reg
> [11138.885066] iwlwifi 0000:00:14.3: IML/ROM dump:
> [11138.885069] iwlwifi 0000:00:14.3: 0x00000003 | IML/ROM error/state
> [11138.885107] iwlwifi 0000:00:14.3: 0x0000588E | IML/ROM data1
> [11138.885145] iwlwifi 0000:00:14.3: 0x00000080 | IML/ROM WFPM_AUTH_KEY_0
> [11138.885180] iwlwifi 0000:00:14.3: Fseq Registers:
> [11138.885211] iwlwifi 0000:00:14.3: 0x60000000 | FSEQ_ERROR_CODE
> [11138.885242] iwlwifi 0000:00:14.3: 0x80290033 | FSEQ_TOP_INIT_VERSION
> [11138.885274] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_CNVIO_INIT_VERSION
> [11138.885305] iwlwifi 0000:00:14.3: 0x0000A492 | FSEQ_OTP_VERSION
> [11138.885337] iwlwifi 0000:00:14.3: 0x00000003 | FSEQ_TOP_CONTENT_VERSION
> [11138.885368] iwlwifi 0000:00:14.3: 0x4552414E | FSEQ_ALIVE_TOKEN
> [11138.885416] iwlwifi 0000:00:14.3: 0x02000300 | FSEQ_CNVI_ID
> [11138.885448] iwlwifi 0000:00:14.3: 0x01300504 | FSEQ_CNVR_ID
> [11138.885480] iwlwifi 0000:00:14.3: 0x02000300 | CNVI_AUX_MISC_CHIP
> [11138.885514] iwlwifi 0000:00:14.3: 0x01300504 | CNVR_AUX_MISC_CHIP
> [11138.885550] iwlwifi 0000:00:14.3: 0x05B0905B | CNVR_SCU_SD_REGS_SD_REG_DIG_DCDC_VTRIM
> [11138.885584] iwlwifi 0000:00:14.3: 0x0000025B | CNVR_SCU_SD_REGS_SD_REG_ACTIVE_VDIG_MIRROR
> [11138.885616] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_PREV_CNVIO_INIT_VERSION
> [11138.885649] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_WIFI_FSEQ_VERSION
> [11138.885680] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_BT_FSEQ_VERSION
> [11138.885712] iwlwifi 0000:00:14.3: 0x00000136 | FSEQ_CLASS_TP_VERSION
> [11138.885779] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0x8047323c
> [11138.885811] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xd0
> [11138.885850] iwlwifi 0000:00:14.3: Failed to start RT ucode: -110
> ```

Forsøkt å skru av power save state
[wireless - How to permanently set Wi-Fi "power management" flag to off? - Ask Ubuntu](https://askubuntu.com/questions/1294591/how-to-permanently-set-wi-fi-power-management-flag-to-off)
```
[connection]
wifi.powersave = 2
```

Forsøkt
[\[SOLVED\] iwlwifi: Microcode SW error detected. Restarting 0x0. / Kernel & Hardware / Arch Linux Forums](https://bbs.archlinux.org/viewtopic.php?id=254766)
/etc/modprobe.d/iwl.conf:
```
options iwlwifi 11n_disable=1 swcrypto=0 bt_coex_active=0 power_save=0
options iwlmvm power_scheme=1 
options iwlwifi d0i3_disable=1 
options iwlwifi uapsd_disable=1 
options iwlwifi lar_disable=1
```

Forsøkt [iwlwifi - Debian Wiki](https://wiki.debian.org/iwlwifi#Troubleshooting) ~~- Ser ut til å fungere~~ Fungerte en uke, så kom det plutselig kraftig tilbake
`/etc/modprobe.d/iwlmvm.conf`
```
options iwlmvm power_scheme=1
```

Kan forsøke: [\[SOLVED\] Intel AX201 iwlwifi: ... failed with error -110... Intel AMT / Kernel & Hardware / Arch Linux Forums](https://bbs.archlinux.org/viewtopic.php?id=297679)
I found a workaround reloading manually the module iwlwifi.
It has been tested on linux mint.
```
mario@asus-mint:~$ sudo rmmod iwlwifi
[sudo] contraseña para mario:                  
rmmod: ERROR: Module iwlwifi is in use by: iwlmvm
mario@asus-mint:~$ sudo rmmod iwlmvm
mario@asus-mint:~$ sudo rmmod iwlwifi
mario@asus-mint:~$ lsmod | grep iwlwifi
mario@asus-mint:~$ sudo modprobe iwlwifi
mario@asus-mint:~$ lsmod | grep iwl
iwlmvm                864256  0
iwlwifi               610304  1 iwlmvm
mac80211             1728512  1 iwlmvm
cfg80211             1339392  3 iwlmvm,iwlwifi,mac80211
mario@asus-mint:~$ 
```
Fungerte hvert fall en stund?
```
sudo rmmod iwlwifi
sudo rmmod iwlmvm
sudo modprobe iwlwifi
```

~~Pretending to be Windows 11 did not work however a Lenovo support representative recently encountered this error and it is due to Intel AMT being enabled in the BIOS. Disabling it has enabled the iwlwifi to work correctly as expected.~~
~~Perhaps AMT does not work on Linux which was why the system was being restrictive when compared to Windows?~~

~~Forsøkt lastet ned backports firmware pakket av debian [iwlwifi - Debian Wiki](https://wiki.debian.org/iwlwifi#Troubleshooting)~~
~~[Debian -- Package Download Selection -- firmware-iwlwifi\_20250410-2\~bpo12+1\_all.deb](https://packages.debian.org/bookworm-backports/all/firmware-iwlwifi/download)~~


# 28.08.2024 Installere POP_OS og dual-boote
## Dual boot
Beholder den gamle installasjonen av Windows, og lager nye partisjoner for Pop. 
- [weywot/Pop\_OS\_Dual\_Boot.md at main · spxak1/weywot · GitHub](https://github.com/spxak1/weywot/blob/main/Pop_OS_Dual_Boot.md#3222-install-windows-without-planning-for-pop_os-easier-and-most-common-for-users-already-having-windows-installed)

| Partisjon | Størrelse |
| --------- | --------- |
| /boot/efi | 512MB     |
| /recovery | 4096MB    |
| swap      | 20GB      |
| /         | 245GB     |

## Oppsett
- Surface-kernel
	- Fant denne i etterkant for installering av Surface-drivere
	- Hoppet over secure-boot, for pop_os støtter ikke det
	- [Installation and Setup · linux-surface/linux-surface Wiki · GitHub](https://github.com/linux-surface/linux-surface/wiki/Installation-and-Setup)
- [GitHub - iAnonymous3000/popos-hardening-guide: A step-by-step guide to securing Pop!\_OS Linux desktops. Covering system updates, user security, network hardening, disk encryption, and more, this guide is tailored for users looking to enhance their Pop!\_OS security posture.](https://github.com/iAnonymous3000/popos-hardening-guide)
	- det er ikke installert ssh-server by default
- Måtte skru av HiDPI Daemon fordi skjerm-scale resatt mellom hver boot.
- Tailscale
```sh
sudo tailscale up
tailscale set --accept-routes --exit-node=100.115.47.67 --exit-node-allow-lan-access=true
```
- Installerte [Howdy](https://github.com/boltgolt/howdy?tab=readme-ov-file) med /dev/video0 som vist her [Setup facial recognition for authentication (howdy). - System76 Support](https://support.system76.com/articles/setup-face-recognition/)
- Hibernate? [Enable Hibernation (Suspend to Disk) - System76 Support](https://support.system76.com/articles/enable-hibernation/)
- File explorer? [Make Linux Mi
- nt’s Nemo the default file manager app on Pop!\_OS and Ubuntu – Matt Callahan's Blog 📝](https://mfcallahan.com/2022/06/24/make-nemo-the-default-file-manager-on-ubuntu/)
	- Valgte Nemo
- Quartus
	- Sette systemvariabel som på WIndows?
	- [How to set and list environment variables on Linux - Linux Tutorials - Learn Linux Configuration](https://linuxconfig.org/how-to-set-and-list-environment-variables-on-linux)
	- Legge til i appdrawer [Add appimage and self-installed apps to Launcher](https://www.reddit.com/r/pop_os/comments/oejk1c/add_appimage_and_selfinstalled_apps_to_launcher/)
	- Se mer [[VHDL-syntaks#Quartus]]
- AppImageLauncher github installere .deb




# 27.08.2024 Oppgradere SSD fra 256GB til 512GB
Kr 673 [512 Gb M.2 2230 Ssd for steam deck eller Surface pc | FINN torget](https://www.finn.no/366820616)
1. Skrudde av bitlocker (ca 1-2 timer)
2. Macrium.com Reflect Home for å kopiere alle partisjoner fra intern til ekstern ssd (ca 1.5 time, x2 fordi første feilet)
3. Åpnet opp og byttet (ca 10 min) [Site Unreachable](https://www.ifixit.com/Guide/Microsoft+Surface+Laptop+3+13.5-Inch+SSD+Replacement/144783)
4. Brukte Clonezilla til å boote i og kopiere ekstern til ny intern (ca 10 min effektivt) https://www.tomshardware.com/how-to/clone-your-ssd-or-hard-drive
5. Alt fungerte bra på første forsøk
![[Screenshot_20240827_224333.jpg|500]]
![[Screenshot_20240827_224404.jpg|336]]

## research 
- Trenger en M.2 2230. Unormal størrelse
- Må være Gen 3?

Informasjon:
[List: 2TB, 1TB, 512GB M.2 2230 SSDs (July 2024) – upgrades for Surface Pro/Laptop, SteamDeck, XBox Series X, etc. – Dan S. Charlton](https://dancharblog.wordpress.com/2024/01/01/upgrade-sl3-or-spx-to-1tb/#steamdeck-surface-laptop-3-laptop-4)


[SSD removal in compatible Surface devices - Surface | Microsoft Learn](https://learn.microsoft.com/en-us/surface/surface-ssd-removal-guide)
[encryption - Use (Windows) BitLocker-encrypted drive on Ubuntu - Ask Ubuntu](https://askubuntu.com/questions/617950/use-windows-bitlocker-encrypted-drive-on-ubuntu)

## Priser
- 130$ [Surface Laptop 3 (Models 1867, 1868, 1872) SSD - Genuine](https://www.ifixit.com/products/surface-laptop-3-models-1867-1868-1872-ssd-genuine?variant=40212909064295)
- [List: 2TB, 1TB, 512GB M.2 2230 SSDs (July 2024) – upgrades for Surface Pro/Laptop, SteamDeck, XBox Series X, etc. – Dan S. Charlton](https://dancharblog.wordpress.com/2024/01/01/upgrade-sl3-or-spx-to-1tb/)


## 1
KBG40ZNS512G BG4A KIOXIA
- [512 Gb M.2 2230 Ssd for steam deck eller Surface pc | FINN torget](https://www.finn.no/bap/forsale/ad.html?finnkode=366820616&ci=3)
- [cSSD-BG4-product-brief.pdf](https://americas.kioxia.com/content/dam/kioxia/shared/business/ssd/client-ssd/asset/productbrief/cSSD-BG4-product-brief.pdf)
![[KrissLaptop-20240821125125884.jpg|500]]


## 2
Kingston
OM3PDP35128-A01

9997345-926.A00GSO
9349833 - 2149
EDFKOS03
DC+3.3V 1A
SN: 500268768550F8CE
PSID:
50026876855DF8CEE748740A268EAC92

- [OM3PDP3512B-A01 Kingston Technology | Memory - Modules, Cards | DigiKey](https://www.digikey.com/en/products/detail/kingston-technology/OM3PDP3512B-A01/15822183)

![[KrissLaptop-20240821125350648.jpg|385]]