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

> [!NOTE]- Logg en gang det forsvant og kom tilbake igjen
> 
> ```LOG
> [51970.259872] iwlwifi 0000:00:14.3: Microcode SW error detected. Restarting 0x0.
> [51970.259972] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [51970.259975] iwlwifi 0000:00:14.3: Transport status: 0x0000004A, valid: 6
> [51970.259979] iwlwifi 0000:00:14.3: Loaded firmware version: 77.6eaf654b.0 Qu-c0-hr-b0-77.ucode
> [51970.259983] iwlwifi 0000:00:14.3: 0x00000091 | ADVANCED_SYSASSERT          
> [51970.259987] iwlwifi 0000:00:14.3: 0x000022F3 | trm_hw_status0
> [51970.259990] iwlwifi 0000:00:14.3: 0x00000000 | trm_hw_status1
> [51970.259993] iwlwifi 0000:00:14.3: 0x004C9742 | branchlink2
> [51970.259996] iwlwifi 0000:00:14.3: 0x000076A8 | interruptlink1
> [51970.259999] iwlwifi 0000:00:14.3: 0x000076A8 | interruptlink2
> [51970.260002] iwlwifi 0000:00:14.3: 0x00006154 | data1
> [51970.260004] iwlwifi 0000:00:14.3: 0x00010000 | data2
> [51970.260007] iwlwifi 0000:00:14.3: 0x00000000 | data3
> [51970.260010] iwlwifi 0000:00:14.3: 0x674051ED | beacon time
> [51970.260013] iwlwifi 0000:00:14.3: 0x00000000 | tsf low
> [51970.260015] iwlwifi 0000:00:14.3: 0x00000000 | tsf hi
> [51970.260018] iwlwifi 0000:00:14.3: 0x00000000 | time gp1
> [51970.260021] iwlwifi 0000:00:14.3: 0x21F57D5C | time gp2
> [51970.260023] iwlwifi 0000:00:14.3: 0x00000001 | uCode revision type
> [51970.260026] iwlwifi 0000:00:14.3: 0x0000004D | uCode version major
> [51970.260029] iwlwifi 0000:00:14.3: 0x6EAF654B | uCode version minor
> [51970.260032] iwlwifi 0000:00:14.3: 0x00000332 | hw version
> [51970.260035] iwlwifi 0000:00:14.3: 0x00C89002 | board version
> [51970.260038] iwlwifi 0000:00:14.3: 0x80F6F400 | hcmd
> [51970.260040] iwlwifi 0000:00:14.3: 0x66F20400 | isr0
> [51970.260043] iwlwifi 0000:00:14.3: 0x00000000 | isr1
> [51970.260045] iwlwifi 0000:00:14.3: 0x08F00002 | isr2
> [51970.260048] iwlwifi 0000:00:14.3: 0x00C1400F | isr3
> [51970.260051] iwlwifi 0000:00:14.3: 0x00000000 | isr4
> [51970.260054] iwlwifi 0000:00:14.3: 0x0396001C | last cmd Id
> [51970.260056] iwlwifi 0000:00:14.3: 0x00006154 | wait_event
> [51970.260059] iwlwifi 0000:00:14.3: 0x000000B4 | l2p_control
> [51970.260062] iwlwifi 0000:00:14.3: 0x00001C20 | l2p_duration
> [51970.260064] iwlwifi 0000:00:14.3: 0x0000000F | l2p_mhvalid
> [51970.260067] iwlwifi 0000:00:14.3: 0x00000006 | l2p_addr_match
> [51970.260070] iwlwifi 0000:00:14.3: 0x00000002 | lmpm_pmg_sel
> [51970.260072] iwlwifi 0000:00:14.3: 0x00000000 | timestamp
> [51970.260075] iwlwifi 0000:00:14.3: 0x0000D08C | flow_handler
> [51970.260140] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [51970.260143] iwlwifi 0000:00:14.3: Transport status: 0x0000004A, valid: 7
> [51970.260146] iwlwifi 0000:00:14.3: 0x20000070 | NMI_INTERRUPT_LMAC_FATAL
> [51970.260150] iwlwifi 0000:00:14.3: 0x00000000 | umac branchlink1
> [51970.260153] iwlwifi 0000:00:14.3: 0x804561EA | umac branchlink2
> [51970.260155] iwlwifi 0000:00:14.3: 0x80473712 | umac interruptlink1
> [51970.260158] iwlwifi 0000:00:14.3: 0x80473712 | umac interruptlink2
> [51970.260161] iwlwifi 0000:00:14.3: 0x00000400 | umac data1
> [51970.260164] iwlwifi 0000:00:14.3: 0x80473712 | umac data2
> [51970.260166] iwlwifi 0000:00:14.3: 0x00000000 | umac data3
> [51970.260169] iwlwifi 0000:00:14.3: 0x0000004D | umac major
> [51970.260172] iwlwifi 0000:00:14.3: 0x6EAF654B | umac minor
> [51970.260174] iwlwifi 0000:00:14.3: 0x21F57DF0 | frame pointer
> [51970.260177] iwlwifi 0000:00:14.3: 0xC0886260 | stack pointer
> [51970.260180] iwlwifi 0000:00:14.3: 0x0094010C | last host cmd
> [51970.260182] iwlwifi 0000:00:14.3: 0x00000000 | isr status reg
> [51970.260206] iwlwifi 0000:00:14.3: IML/ROM dump:
> [51970.260209] iwlwifi 0000:00:14.3: 0x00000003 | IML/ROM error/state
> [51970.260233] iwlwifi 0000:00:14.3: 0x000057F5 | IML/ROM data1
> [51970.260260] iwlwifi 0000:00:14.3: 0x00000080 | IML/ROM WFPM_AUTH_KEY_0
> [51970.260285] iwlwifi 0000:00:14.3: Fseq Registers:
> [51970.260305] iwlwifi 0000:00:14.3: 0x60000000 | FSEQ_ERROR_CODE
> [51970.260326] iwlwifi 0000:00:14.3: 0x80290033 | FSEQ_TOP_INIT_VERSION
> [51970.260347] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_CNVIO_INIT_VERSION
> [51970.260369] iwlwifi 0000:00:14.3: 0x0000A492 | FSEQ_OTP_VERSION
> [51970.260390] iwlwifi 0000:00:14.3: 0x00000003 | FSEQ_TOP_CONTENT_VERSION
> [51970.260411] iwlwifi 0000:00:14.3: 0x4552414E | FSEQ_ALIVE_TOKEN
> [51970.260432] iwlwifi 0000:00:14.3: 0x02000300 | FSEQ_CNVI_ID
> [51970.260453] iwlwifi 0000:00:14.3: 0x01300504 | FSEQ_CNVR_ID
> [51970.260458] iwlwifi 0000:00:14.3: 0x02000300 | CNVI_AUX_MISC_CHIP
> [51970.260480] iwlwifi 0000:00:14.3: 0x01300504 | CNVR_AUX_MISC_CHIP
> [51970.260502] iwlwifi 0000:00:14.3: 0x05B0905B | CNVR_SCU_SD_REGS_SD_REG_DIG_DCDC_VTRIM
> [51970.260523] iwlwifi 0000:00:14.3: 0x0000025B | CNVR_SCU_SD_REGS_SD_REG_ACTIVE_VDIG_MIRROR
> [51970.260543] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_PREV_CNVIO_INIT_VERSION
> [51970.260565] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_WIFI_FSEQ_VERSION
> [51970.260586] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_BT_FSEQ_VERSION
> [51970.260607] iwlwifi 0000:00:14.3: 0x00000136 | FSEQ_CLASS_TP_VERSION
> [51970.260619] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0x80473220
> [51970.260638] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xd0
> [51970.260703] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 4 fired (delay=0ms).
> [51970.662224] iwlwifi 0000:00:14.3: Device error - SW reset
> [51970.662424] ieee80211 phy0: Hardware restart was requested
> [51970.819102] iwlwifi 0000:00:14.3: Microcode SW error detected. Restarting 0x0.
> [51970.819173] iwlwifi 0000:00:14.3: Failed to start RT ucode: -5
> [51970.819183] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [51970.819202] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [51970.819205] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 6
> [51970.819209] iwlwifi 0000:00:14.3: Loaded firmware version: 77.6eaf654b.0 Qu-c0-hr-b0-77.ucode
> [51970.819213] iwlwifi 0000:00:14.3: 0x00000091 | ADVANCED_SYSASSERT          
> [51970.819217] iwlwifi 0000:00:14.3: 0x0000A2F0 | trm_hw_status0
> [51970.819220] iwlwifi 0000:00:14.3: 0x00000000 | trm_hw_status1
> [51970.819222] iwlwifi 0000:00:14.3: 0x004C9742 | branchlink2
> [51970.819225] iwlwifi 0000:00:14.3: 0x00015706 | interruptlink1
> [51970.819227] iwlwifi 0000:00:14.3: 0x00015706 | interruptlink2
> [51970.819230] iwlwifi 0000:00:14.3: 0x00013186 | data1
> [51970.819232] iwlwifi 0000:00:14.3: 0x00010000 | data2
> [51970.819235] iwlwifi 0000:00:14.3: 0x00000000 | data3
> [51970.819237] iwlwifi 0000:00:14.3: 0x00000000 | beacon time
> [51970.819240] iwlwifi 0000:00:14.3: 0x00000000 | tsf low
> [51970.819242] iwlwifi 0000:00:14.3: 0x00000000 | tsf hi
> [51970.819245] iwlwifi 0000:00:14.3: 0x00000000 | time gp1
> [51970.819247] iwlwifi 0000:00:14.3: 0x0001F354 | time gp2
> [51970.819250] iwlwifi 0000:00:14.3: 0x00000001 | uCode revision type
> [51970.819252] iwlwifi 0000:00:14.3: 0x0000004D | uCode version major
> [51970.819255] iwlwifi 0000:00:14.3: 0x6EAF654B | uCode version minor
> [51970.819258] iwlwifi 0000:00:14.3: 0x00000332 | hw version
> [51970.819260] iwlwifi 0000:00:14.3: 0x00C89002 | board version
> [51970.819263] iwlwifi 0000:00:14.3: 0x8017FD28 | hcmd
> [51970.819266] iwlwifi 0000:00:14.3: 0x62F29400 | isr0
> [51970.819268] iwlwifi 0000:00:14.3: 0x00000000 | isr1
> [51970.819270] iwlwifi 0000:00:14.3: 0x08F00002 | isr2
> [51970.819273] iwlwifi 0000:00:14.3: 0x04C0001C | isr3
> [51970.819275] iwlwifi 0000:00:14.3: 0x00000000 | isr4
> [51970.819278] iwlwifi 0000:00:14.3: 0x00000000 | last cmd Id
> [51970.819280] iwlwifi 0000:00:14.3: 0x00013186 | wait_event
> [51970.819283] iwlwifi 0000:00:14.3: 0x00000000 | l2p_control
> [51970.819286] iwlwifi 0000:00:14.3: 0x00000000 | l2p_duration
> [51970.819288] iwlwifi 0000:00:14.3: 0x00000000 | l2p_mhvalid
> [51970.819290] iwlwifi 0000:00:14.3: 0x00000000 | l2p_addr_match
> [51970.819293] iwlwifi 0000:00:14.3: 0x00000000 | lmpm_pmg_sel
> [51970.819295] iwlwifi 0000:00:14.3: 0x00000000 | timestamp
> [51970.819298] iwlwifi 0000:00:14.3: 0x00000020 | flow_handler
> [51970.819342] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [51970.819344] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 7
> [51970.819347] iwlwifi 0000:00:14.3: 0x20000070 | NMI_INTERRUPT_LMAC_FATAL
> [51970.819350] iwlwifi 0000:00:14.3: 0x00000000 | umac branchlink1
> [51970.819353] iwlwifi 0000:00:14.3: 0x804561EA | umac branchlink2
> [51970.819355] iwlwifi 0000:00:14.3: 0x80473712 | umac interruptlink1
> [51970.819358] iwlwifi 0000:00:14.3: 0x80473712 | umac interruptlink2
> [51970.819360] iwlwifi 0000:00:14.3: 0x00000400 | umac data1
> [51970.819363] iwlwifi 0000:00:14.3: 0x80473712 | umac data2
> [51970.819365] iwlwifi 0000:00:14.3: 0x00000000 | umac data3
> [51970.819368] iwlwifi 0000:00:14.3: 0x0000004D | umac major
> [51970.819370] iwlwifi 0000:00:14.3: 0x6EAF654B | umac minor
> [51970.819373] iwlwifi 0000:00:14.3: 0x0001F3ED | frame pointer
> [51970.819375] iwlwifi 0000:00:14.3: 0xC0886260 | stack pointer
> [51970.819378] iwlwifi 0000:00:14.3: 0x00010C00 | last host cmd
> [51970.819380] iwlwifi 0000:00:14.3: 0x00000000 | isr status reg
> [51970.819404] iwlwifi 0000:00:14.3: IML/ROM dump:
> [51970.819406] iwlwifi 0000:00:14.3: 0x00000003 | IML/ROM error/state
> [51970.819431] iwlwifi 0000:00:14.3: 0x0000588C | IML/ROM data1
> [51970.819458] iwlwifi 0000:00:14.3: 0x00000080 | IML/ROM WFPM_AUTH_KEY_0
> [51970.819482] iwlwifi 0000:00:14.3: Fseq Registers:
> [51970.819502] iwlwifi 0000:00:14.3: 0x60000000 | FSEQ_ERROR_CODE
> [51970.819507] iwlwifi 0000:00:14.3: 0x80290033 | FSEQ_TOP_INIT_VERSION
> [51970.819527] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_CNVIO_INIT_VERSION
> [51970.819532] iwlwifi 0000:00:14.3: 0x0000A492 | FSEQ_OTP_VERSION
> [51970.819552] iwlwifi 0000:00:14.3: 0x00000003 | FSEQ_TOP_CONTENT_VERSION
> [51970.819573] iwlwifi 0000:00:14.3: 0x4552414E | FSEQ_ALIVE_TOKEN
> [51970.819577] iwlwifi 0000:00:14.3: 0x02000300 | FSEQ_CNVI_ID
> [51970.819597] iwlwifi 0000:00:14.3: 0x01300504 | FSEQ_CNVR_ID
> [51970.819602] iwlwifi 0000:00:14.3: 0x02000300 | CNVI_AUX_MISC_CHIP
> [51970.819624] iwlwifi 0000:00:14.3: 0x01300504 | CNVR_AUX_MISC_CHIP
> [51970.819646] iwlwifi 0000:00:14.3: 0x05B0905B | CNVR_SCU_SD_REGS_SD_REG_DIG_DCDC_VTRIM
> [51970.819668] iwlwifi 0000:00:14.3: 0x0000025B | CNVR_SCU_SD_REGS_SD_REG_ACTIVE_VDIG_MIRROR
> [51970.819688] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_PREV_CNVIO_INIT_VERSION
> [51970.819709] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_WIFI_FSEQ_VERSION
> [51970.819714] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_BT_FSEQ_VERSION
> [51970.819733] iwlwifi 0000:00:14.3: 0x00000136 | FSEQ_CLASS_TP_VERSION
> [51970.819745] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0x80473220
> [51970.819764] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xd0
> [51971.424879] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 4 fired (delay=0ms).
> [51971.833736] ------------[ cut here ]------------
> [51971.833739] Hardware became unavailable during restart.
> [51971.833809] WARNING: CPU: 5 PID: 74953 at net/mac80211/util.c:1821 ieee80211_reconfig+0xe2/0x17b0 [mac80211]
> [51971.833875] Modules linked in: vhost_net vhost vhost_iotlb tap iptable_mangle xt_CHECKSUM xt_multiport iptable_nat nf_conntrack_netlink xt_nat veth xt_mark xt_MASQUERADE bridge stp llc xt_set ip_set nft_chain_nat nf_nat xfrm_user xfrm_algo ccm rfcomm cmac algif_hash algif_skcipher af_alg snd_seq_dummy snd_hrtimer snd_hda_codec_intelhdmi overlay bnep ip6t_REJECT nf_reject_ipv6 xt_hl zram ip6t_rt 842_decompress 842_compress ipt_REJECT lz4hc_compress nf_reject_ipv4 lz4_compress xt_LOG nf_log_syslog input_leds joydev nft_limit hid_multitouch xt_limit xt_addrtype xt_tcpudp xt_conntrack nf_conntrack nf_defrag_ipv6 nf_defrag_ipv4 nft_compat snd_hda_codec_alc269 snd_hda_scodec_component snd_hda_codec_realtek_lib snd_hda_codec_generic snd_hda_intel nf_tables snd_sof_pci_intel_icl snd_sof_pci_intel_cnl snd_sof_intel_hda_generic nfnetlink soundwire_intel snd_sof_intel_hda_sdw_bpt binfmt_misc snd_sof_intel_hda_common snd_soc_hdac_hda snd_sof_intel_hda_mlink snd_sof_intel_hda snd_hda_codec_hdmi soundwire_cadence snd_sof_pci
> [51971.833913]  snd_sof_xtensa_dsp snd_sof snd_sof_utils snd_soc_acpi_intel_match snd_soc_acpi_intel_sdca_quirks soundwire_generic_allocation snd_soc_acpi soundwire_bus snd_soc_sdca crc8 snd_soc_avs snd_soc_hda_codec snd_hda_ext_core snd_hda_codec hid_generic intel_uncore_frequency intel_uncore_frequency_common snd_hda_core mei_pxp mei_hdcp snd_intel_dspcfg surface_hid snd_intel_sdw_acpi ipts snd_hwdep surface_hid_core surface_platform_profile platform_profile hid intel_tcc_cooling surface_battery snd_soc_core surface_charger intel_rapl_msr snd_compress x86_pkg_temp_thermal ac97_bus snd_pcm_dmaengine intel_powerclamp snd_pcm coretemp snd_seq_midi iwlmvm snd_seq_midi_event nls_iso8859_1 snd_rawmidi gpio_keys kvm_intel surface_gpe processor_thermal_device_pci_legacy snd_seq btusb mac80211 processor_thermal_device kvm processor_thermal_wt_hint btrtl platform_temperature_control snd_seq_device btintel irqbypass processor_thermal_rfim libarc4 snd_timer btbcm btmtk processor_thermal_rapl rapl cmdlinepart iwlwifi spi_nor snd
> [51971.833954]  intel_cstate intel_rapl_common mei_me intel_wmi_thunderbolt bluetooth mtd 8250_dw intel_pmc_core soundcore mei pmt_telemetry processor_thermal_wt_req cfg80211 processor_thermal_power_floor pmt_discovery pmt_class processor_thermal_mbox int3403_thermal intel_soc_dts_iosf int340x_thermal_zone surfacepro3_button intel_pmc_ssram_telemetry mac_hid int3400_thermal surface_aggregator_registry acpi_pad soc_button_array surface_hotplug surface_acpi_notify intel_vsec acpi_tad dptf_power acpi_thermal_rel sch_fq_codel kyber_iosched msr parport_pc ppdev lp parport efi_pstore ip_tables x_tables autofs4 dm_crypt raid10 raid456 async_raid6_recov async_memcpy async_pq async_xor async_tx xor raid6_pq raid1 raid0 linear system76_io(OE) system76_acpi(OE) i915 nvme drm_buddy polyval_clmulni ttm ghash_clmulni_intel i2c_algo_bit nvme_core spi_intel_pci drm_display_helper nvme_keyring intel_lpss_pci spi_intel nvme_auth intel_lpss cec idma64 rc_core video surface_aggregator wmi crc_itu_t pinctrl_icelake aesni_intel
> [51971.834018] CPU: 5 UID: 0 PID: 74953 Comm: kworker/5:1 Tainted: G        W  OE       6.17.1-surface-2 #2 PREEMPT(voluntary) 
> [51971.834022] Tainted: [W]=WARN, [O]=OOT_MODULE, [E]=UNSIGNED_MODULE
> [51971.834024] Hardware name: Microsoft Corporation Surface Laptop 3/Surface Laptop 3, BIOS 19.101.140 04/11/2024
> [51971.834026] Workqueue: events_freezable ieee80211_restart_work [mac80211]
> [51971.834071] RIP: 0010:ieee80211_reconfig+0xe2/0x17b0 [mac80211]
> [51971.834125] Code: 0f 85 24 03 00 00 41 c6 84 24 ad 05 00 00 00 4c 89 e7 e8 b1 1e fb ff 41 89 c7 85 c0 74 66 48 c7 c7 d0 7c 1b c1 e8 6e e7 c8 ca <0f> 0b 4c 89 e7 31 c9 ba 04 00 00 00 be ff ff 00 00 e8 88 ef ff ff
> [51971.834128] RSP: 0018:ffffcf9f641cbd28 EFLAGS: 00010246
> [51971.834130] RAX: 0000000000000000 RBX: ffff8e3987399b08 RCX: 0000000000000000
> [51971.834131] RDX: 0000000000000000 RSI: 0000000000000000 RDI: 0000000000000000
> [51971.834132] RBP: ffffcf9f641cbe08 R08: 0000000000000000 R09: 0000000000000000
> [51971.834133] R10: 0000000000000000 R11: 0000000000000000 R12: ffff8e3987398940
> [51971.834133] R13: ffff8e3987399b08 R14: ffff8e3987398940 R15: 00000000fffffffb
> [51971.834135] FS:  0000000000000000(0000) GS:ffff8e3d4ca60000(0000) knlGS:0000000000000000
> [51971.834136] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
> [51971.834137] CR2: ffffe507405d1f30 CR3: 0000000204636005 CR4: 0000000000772ef0
> [51971.834138] PKRU: 55555554
> [51971.834139] Call Trace:
> [51971.834140]  <TASK>
> [51971.834143]  ? wq_worker_running+0xe/0x70
> [51971.834147]  ? synchronize_rcu_expedited+0x1af/0x1f0
> [51971.834150]  ? __pfx_autoremove_wake_function+0x10/0x10
> [51971.834153]  ? __pfx_wait_rcu_exp_gp+0x10/0x10
> [51971.834156]  ieee80211_restart_work+0xee/0x170 [mac80211]
> [51971.834194]  process_one_work+0x19c/0x3f0
> [51971.834198]  worker_thread+0x2ba/0x3d0
> [51971.834201]  kthread+0x104/0x220
> [51971.834203]  ? __pfx_worker_thread+0x10/0x10
> [51971.834205]  ? __pfx_kthread+0x10/0x10
> [51971.834207]  ret_from_fork+0x1ec/0x220
> [51971.834209]  ? __pfx_kthread+0x10/0x10
> [51971.834211]  ret_from_fork_asm+0x1a/0x30
> [51971.834214]  </TASK>
> [51971.834215] ---[ end trace 0000000000000000 ]---
> [51971.839034] iwlwifi 0000:00:14.3: Failed to synchronize multicast groups update
> [51971.839053] wlp0s20f3: deauthenticating from 88:9c:ad:04:e5:6e by local choice (Reason: 3=DEAUTH_LEAVING)
> [51971.839181] iwlwifi 0000:00:14.3: Failed to trigger RX queues sync (-5)
> [51971.839203] ------------[ cut here ]------------
> [51971.839204] Driver is not allowed to fail if the sta_state is transitioning down the list: -5
> [51971.839232] WARNING: CPU: 5 PID: 74953 at net/mac80211/sta_info.c:1467 _sta_info_move_state+0x208/0x5a0 [mac80211]
> [51971.839267] Modules linked in: vhost_net vhost vhost_iotlb tap iptable_mangle xt_CHECKSUM xt_multiport iptable_nat nf_conntrack_netlink xt_nat veth xt_mark xt_MASQUERADE bridge stp llc xt_set ip_set nft_chain_nat nf_nat xfrm_user xfrm_algo ccm rfcomm cmac algif_hash algif_skcipher af_alg snd_seq_dummy snd_hrtimer snd_hda_codec_intelhdmi overlay bnep ip6t_REJECT nf_reject_ipv6 xt_hl zram ip6t_rt 842_decompress 842_compress ipt_REJECT lz4hc_compress nf_reject_ipv4 lz4_compress xt_LOG nf_log_syslog input_leds joydev nft_limit hid_multitouch xt_limit xt_addrtype xt_tcpudp xt_conntrack nf_conntrack nf_defrag_ipv6 nf_defrag_ipv4 nft_compat snd_hda_codec_alc269 snd_hda_scodec_component snd_hda_codec_realtek_lib snd_hda_codec_generic snd_hda_intel nf_tables snd_sof_pci_intel_icl snd_sof_pci_intel_cnl snd_sof_intel_hda_generic nfnetlink soundwire_intel snd_sof_intel_hda_sdw_bpt binfmt_misc snd_sof_intel_hda_common snd_soc_hdac_hda snd_sof_intel_hda_mlink snd_sof_intel_hda snd_hda_codec_hdmi soundwire_cadence snd_sof_pci
> [51971.839303]  snd_sof_xtensa_dsp snd_sof snd_sof_utils snd_soc_acpi_intel_match snd_soc_acpi_intel_sdca_quirks soundwire_generic_allocation snd_soc_acpi soundwire_bus snd_soc_sdca crc8 snd_soc_avs snd_soc_hda_codec snd_hda_ext_core snd_hda_codec hid_generic intel_uncore_frequency intel_uncore_frequency_common snd_hda_core mei_pxp mei_hdcp snd_intel_dspcfg surface_hid snd_intel_sdw_acpi ipts snd_hwdep surface_hid_core surface_platform_profile platform_profile hid intel_tcc_cooling surface_battery snd_soc_core surface_charger intel_rapl_msr snd_compress x86_pkg_temp_thermal ac97_bus snd_pcm_dmaengine intel_powerclamp snd_pcm coretemp snd_seq_midi iwlmvm snd_seq_midi_event nls_iso8859_1 snd_rawmidi gpio_keys kvm_intel surface_gpe processor_thermal_device_pci_legacy snd_seq btusb mac80211 processor_thermal_device kvm processor_thermal_wt_hint btrtl platform_temperature_control snd_seq_device btintel irqbypass processor_thermal_rfim libarc4 snd_timer btbcm btmtk processor_thermal_rapl rapl cmdlinepart iwlwifi spi_nor snd
> [51971.839339]  intel_cstate intel_rapl_common mei_me intel_wmi_thunderbolt bluetooth mtd 8250_dw intel_pmc_core soundcore mei pmt_telemetry processor_thermal_wt_req cfg80211 processor_thermal_power_floor pmt_discovery pmt_class processor_thermal_mbox int3403_thermal intel_soc_dts_iosf int340x_thermal_zone surfacepro3_button intel_pmc_ssram_telemetry mac_hid int3400_thermal surface_aggregator_registry acpi_pad soc_button_array surface_hotplug surface_acpi_notify intel_vsec acpi_tad dptf_power acpi_thermal_rel sch_fq_codel kyber_iosched msr parport_pc ppdev lp parport efi_pstore ip_tables x_tables autofs4 dm_crypt raid10 raid456 async_raid6_recov async_memcpy async_pq async_xor async_tx xor raid6_pq raid1 raid0 linear system76_io(OE) system76_acpi(OE) i915 nvme drm_buddy polyval_clmulni ttm ghash_clmulni_intel i2c_algo_bit nvme_core spi_intel_pci drm_display_helper nvme_keyring intel_lpss_pci spi_intel nvme_auth intel_lpss cec idma64 rc_core video surface_aggregator wmi crc_itu_t pinctrl_icelake aesni_intel
> [51971.839380] CPU: 5 UID: 0 PID: 74953 Comm: kworker/5:1 Tainted: G        W  OE       6.17.1-surface-2 #2 PREEMPT(voluntary) 
> [51971.839383] Tainted: [W]=WARN, [O]=OOT_MODULE, [E]=UNSIGNED_MODULE
> [51971.839384] Hardware name: Microsoft Corporation Surface Laptop 3/Surface Laptop 3, BIOS 19.101.140 04/11/2024
> [51971.839385] Workqueue: events_freezable ieee80211_restart_work [mac80211]
> [51971.839411] RIP: 0010:_sta_info_move_state+0x208/0x5a0 [mac80211]
> [51971.839437] Code: 48 89 da e8 da b7 ff ff 85 c0 74 b8 80 3d 3b fe 20 00 00 75 af 89 c6 48 c7 c7 c8 5b 1b c1 c6 05 29 fe 20 00 01 e8 68 78 cd ca <0f> 0b eb 96 83 ea 02 83 e2 fd 0f 85 19 01 00 00 48 8b 43 50 4c 8d
> [51971.839438] RSP: 0018:ffffcf9f641cb7b0 EFLAGS: 00010246
> [51971.839440] RAX: 0000000000000000 RBX: ffff8e3a4ca32000 RCX: 0000000000000000
> [51971.839441] RDX: 0000000000000000 RSI: 0000000000000000 RDI: 0000000000000000
> [51971.839442] RBP: ffffcf9f641cb7d8 R08: 0000000000000000 R09: 0000000000000000
> [51971.839442] R10: 0000000000000000 R11: 0000000000000000 R12: 0000000000000003
> [51971.839443] R13: ffff8e39a1eb8a80 R14: ffff8e3987398940 R15: ffff8e3a4ca32ae0
> [51971.839444] FS:  0000000000000000(0000) GS:ffff8e3d4ca60000(0000) knlGS:0000000000000000
> [51971.839445] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
> [51971.839446] CR2: ffffe507405d1f30 CR3: 0000000204636005 CR4: 0000000000772ef0
> [51971.839447] PKRU: 55555554
> [51971.839448] Call Trace:
> [51971.839449]  <TASK>
> [51971.839451]  __sta_info_destroy_part2+0x1d3/0x1f0 [mac80211]
> [51971.839479]  __sta_info_flush+0x175/0x200 [mac80211]
> [51971.839507]  ieee80211_set_disassoc+0x79a/0x870 [mac80211]
> [51971.839550]  ieee80211_mgd_deauth+0x125/0x4c0 [mac80211]
> [51971.839590]  ieee80211_deauth+0x18/0x30 [mac80211]
> [51971.839628]  cfg80211_mlme_deauth+0xa5/0x1e0 [cfg80211]
> [51971.839675]  cfg80211_mlme_down+0x60/0x90 [cfg80211]
> [51971.839706]  cfg80211_disconnect+0x195/0x200 [cfg80211]
> [51971.839740]  cfg80211_leave+0x147/0x1c0 [cfg80211]
> [51971.839763]  cfg80211_netdev_notifier_call+0x13e/0x500 [cfg80211]
> [51971.839785]  ? psi_task_switch+0x10a/0x2a0
> [51971.839788]  ? raw_spin_rq_unlock+0x10/0x40
> [51971.839792]  ? __dev_printk+0x39/0xa0
> [51971.839795]  ? _dev_err+0x6b/0xa0
> [51971.839799]  ? __iwl_err+0x163/0x170 [iwlwifi]
> [51971.839813]  ? rtnl_is_locked+0x15/0x20
> [51971.839817]  ? inetdev_event+0x45/0x730
> [51971.839820]  ? packet_notifier+0x131/0x270
> [51971.839830]  notifier_call_chain+0x62/0xe0
> [51971.839833]  raw_notifier_call_chain+0x16/0x30
> [51971.839834]  call_netdevice_notifiers_info+0x50/0x90
> [51971.839837]  __dev_close_many+0x67/0x220
> [51971.839840]  netif_close_many+0x98/0x170
> [51971.839842]  netif_close+0x71/0x90
> [51971.839845]  dev_close+0x2a/0x90
> [51971.839847]  cfg80211_shutdown_all_interfaces+0x57/0x110 [cfg80211]
> [51971.839871]  ieee80211_restart_work+0x13c/0x170 [mac80211]
> [51971.839903]  process_one_work+0x19c/0x3f0
> [51971.839906]  worker_thread+0x2ba/0x3d0
> [51971.839909]  kthread+0x104/0x220
> [51971.839911]  ? __pfx_worker_thread+0x10/0x10
> [51971.839913]  ? __pfx_kthread+0x10/0x10
> [51971.839915]  ret_from_fork+0x1ec/0x220
> [51971.839916]  ? __pfx_kthread+0x10/0x10
> [51971.839918]  ret_from_fork_asm+0x1a/0x30
> [51971.839922]  </TASK>
> [51971.839924] ---[ end trace 0000000000000000 ]---
> [51971.839940] wlp0s20f3: failed to remove key (0, 88:9c:ad:04:e5:6e) from hardware (-5)
> [51971.839981] ------------[ cut here ]------------
> [51971.839982] WARNING: CPU: 5 PID: 74953 at net/mac80211/sta_info.c:1539 __sta_info_destroy_part2+0x1bb/0x1f0 [mac80211]
> [51971.840016] Modules linked in: vhost_net vhost vhost_iotlb tap iptable_mangle xt_CHECKSUM xt_multiport iptable_nat nf_conntrack_netlink xt_nat veth xt_mark xt_MASQUERADE bridge stp llc xt_set ip_set nft_chain_nat nf_nat xfrm_user xfrm_algo ccm rfcomm cmac algif_hash algif_skcipher af_alg snd_seq_dummy snd_hrtimer snd_hda_codec_intelhdmi overlay bnep ip6t_REJECT nf_reject_ipv6 xt_hl zram ip6t_rt 842_decompress 842_compress ipt_REJECT lz4hc_compress nf_reject_ipv4 lz4_compress xt_LOG nf_log_syslog input_leds joydev nft_limit hid_multitouch xt_limit xt_addrtype xt_tcpudp xt_conntrack nf_conntrack nf_defrag_ipv6 nf_defrag_ipv4 nft_compat snd_hda_codec_alc269 snd_hda_scodec_component snd_hda_codec_realtek_lib snd_hda_codec_generic snd_hda_intel nf_tables snd_sof_pci_intel_icl snd_sof_pci_intel_cnl snd_sof_intel_hda_generic nfnetlink soundwire_intel snd_sof_intel_hda_sdw_bpt binfmt_misc snd_sof_intel_hda_common snd_soc_hdac_hda snd_sof_intel_hda_mlink snd_sof_intel_hda snd_hda_codec_hdmi soundwire_cadence snd_sof_pci
> [51971.840047]  snd_sof_xtensa_dsp snd_sof snd_sof_utils snd_soc_acpi_intel_match snd_soc_acpi_intel_sdca_quirks soundwire_generic_allocation snd_soc_acpi soundwire_bus snd_soc_sdca crc8 snd_soc_avs snd_soc_hda_codec snd_hda_ext_core snd_hda_codec hid_generic intel_uncore_frequency intel_uncore_frequency_common snd_hda_core mei_pxp mei_hdcp snd_intel_dspcfg surface_hid snd_intel_sdw_acpi ipts snd_hwdep surface_hid_core surface_platform_profile platform_profile hid intel_tcc_cooling surface_battery snd_soc_core surface_charger intel_rapl_msr snd_compress x86_pkg_temp_thermal ac97_bus snd_pcm_dmaengine intel_powerclamp snd_pcm coretemp snd_seq_midi iwlmvm snd_seq_midi_event nls_iso8859_1 snd_rawmidi gpio_keys kvm_intel surface_gpe processor_thermal_device_pci_legacy snd_seq btusb mac80211 processor_thermal_device kvm processor_thermal_wt_hint btrtl platform_temperature_control snd_seq_device btintel irqbypass processor_thermal_rfim libarc4 snd_timer btbcm btmtk processor_thermal_rapl rapl cmdlinepart iwlwifi spi_nor snd
> [51971.840075]  intel_cstate intel_rapl_common mei_me intel_wmi_thunderbolt bluetooth mtd 8250_dw intel_pmc_core soundcore mei pmt_telemetry processor_thermal_wt_req cfg80211 processor_thermal_power_floor pmt_discovery pmt_class processor_thermal_mbox int3403_thermal intel_soc_dts_iosf int340x_thermal_zone surfacepro3_button intel_pmc_ssram_telemetry mac_hid int3400_thermal surface_aggregator_registry acpi_pad soc_button_array surface_hotplug surface_acpi_notify intel_vsec acpi_tad dptf_power acpi_thermal_rel sch_fq_codel kyber_iosched msr parport_pc ppdev lp parport efi_pstore ip_tables x_tables autofs4 dm_crypt raid10 raid456 async_raid6_recov async_memcpy async_pq async_xor async_tx xor raid6_pq raid1 raid0 linear system76_io(OE) system76_acpi(OE) i915 nvme drm_buddy polyval_clmulni ttm ghash_clmulni_intel i2c_algo_bit nvme_core spi_intel_pci drm_display_helper nvme_keyring intel_lpss_pci spi_intel nvme_auth intel_lpss cec idma64 rc_core video surface_aggregator wmi crc_itu_t pinctrl_icelake aesni_intel
> [51971.840110] CPU: 5 UID: 0 PID: 74953 Comm: kworker/5:1 Tainted: G        W  OE       6.17.1-surface-2 #2 PREEMPT(voluntary) 
> [51971.840113] Tainted: [W]=WARN, [O]=OOT_MODULE, [E]=UNSIGNED_MODULE
> [51971.840116] Hardware name: Microsoft Corporation Surface Laptop 3/Surface Laptop 3, BIOS 19.101.140 04/11/2024
> [51971.840119] Workqueue: events_freezable ieee80211_restart_work [mac80211]
> [51971.840146] RIP: 0010:__sta_info_destroy_part2+0x1bb/0x1f0 [mac80211]
> [51971.840172] Code: be d4 00 00 00 00 0f 84 07 ff ff ff 45 31 c0 b9 01 00 00 00 4c 89 f2 4c 89 ee 4c 89 e7 e8 3d 6c ff ff 85 c0 0f 84 e9 fe ff ff <0f> 0b e9 e2 fe ff ff 41 0f b6 d7 be 03 00 00 00 4c 89 f7 e8 5d b2
> [51971.840174] RSP: 0018:ffffcf9f641cb7e8 EFLAGS: 00010282
> [51971.840175] RAX: 00000000fffffffb RBX: 0000000000000000 RCX: 0000000000000000
> [51971.840176] RDX: 0000000000000000 RSI: 0000000000000000 RDI: 0000000000000000
> [51971.840177] RBP: ffffcf9f641cb810 R08: 0000000000000000 R09: 0000000000000000
> [51971.840178] R10: 0000000000000000 R11: 0000000000000000 R12: ffff8e3987398940
> [51971.840178] R13: ffff8e39a1eb8a80 R14: ffff8e3a4ca32000 R15: 0000000000000000
> [51971.840179] FS:  0000000000000000(0000) GS:ffff8e3d4ca60000(0000) knlGS:0000000000000000
> [51971.840180] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
> [51971.840181] CR2: ffffe507405d1f30 CR3: 0000000204636005 CR4: 0000000000772ef0
> [51971.840182] PKRU: 55555554
> [51971.840183] Call Trace:
> [51971.840184]  <TASK>
> [51971.840185]  __sta_info_flush+0x175/0x200 [mac80211]
> [51971.840212]  ieee80211_set_disassoc+0x79a/0x870 [mac80211]
> [51971.840255]  ieee80211_mgd_deauth+0x125/0x4c0 [mac80211]
> [51971.840295]  ieee80211_deauth+0x18/0x30 [mac80211]
> [51971.840331]  cfg80211_mlme_deauth+0xa5/0x1e0 [cfg80211]
> [51971.840364]  cfg80211_mlme_down+0x60/0x90 [cfg80211]
> [51971.840392]  cfg80211_disconnect+0x195/0x200 [cfg80211]
> [51971.840423]  cfg80211_leave+0x147/0x1c0 [cfg80211]
> [51971.840444]  cfg80211_netdev_notifier_call+0x13e/0x500 [cfg80211]
> [51971.840466]  ? psi_task_switch+0x10a/0x2a0
> [51971.840469]  ? raw_spin_rq_unlock+0x10/0x40
> [51971.840472]  ? __dev_printk+0x39/0xa0
> [51971.840474]  ? _dev_err+0x6b/0xa0
> [51971.840477]  ? __iwl_err+0x163/0x170 [iwlwifi]
> [51971.840490]  ? rtnl_is_locked+0x15/0x20
> [51971.840493]  ? inetdev_event+0x45/0x730
> [51971.840495]  ? packet_notifier+0x131/0x270
> [51971.840497]  notifier_call_chain+0x62/0xe0
> [51971.840499]  raw_notifier_call_chain+0x16/0x30
> [51971.840500]  call_netdevice_notifiers_info+0x50/0x90
> [51971.840503]  __dev_close_many+0x67/0x220
> [51971.840505]  netif_close_many+0x98/0x170
> [51971.840508]  netif_close+0x71/0x90
> [51971.840510]  dev_close+0x2a/0x90
> [51971.840512]  cfg80211_shutdown_all_interfaces+0x57/0x110 [cfg80211]
> [51971.840533]  ieee80211_restart_work+0x13c/0x170 [mac80211]
> [51971.840561]  process_one_work+0x19c/0x3f0
> [51971.840564]  worker_thread+0x2ba/0x3d0
> [51971.840567]  kthread+0x104/0x220
> [51971.840568]  ? __pfx_worker_thread+0x10/0x10
> [51971.840571]  ? __pfx_kthread+0x10/0x10
> [51971.840572]  ret_from_fork+0x1ec/0x220
> [51971.840574]  ? __pfx_kthread+0x10/0x10
> [51971.840575]  ret_from_fork_asm+0x1a/0x30
> [51971.840578]  </TASK>
> [51971.840579] ---[ end trace 0000000000000000 ]---
> [51971.840633] ------------[ cut here ]------------
> [51971.840634] WARNING: CPU: 5 PID: 74953 at net/mac80211/driver-ops.h:1038 ieee80211_del_chanctx+0x11c/0x130 [mac80211]
> [51971.840677] Modules linked in: vhost_net vhost vhost_iotlb tap iptable_mangle xt_CHECKSUM xt_multiport iptable_nat nf_conntrack_netlink xt_nat veth xt_mark xt_MASQUERADE bridge stp llc xt_set ip_set nft_chain_nat nf_nat xfrm_user xfrm_algo ccm rfcomm cmac algif_hash algif_skcipher af_alg snd_seq_dummy snd_hrtimer snd_hda_codec_intelhdmi overlay bnep ip6t_REJECT nf_reject_ipv6 xt_hl zram ip6t_rt 842_decompress 842_compress ipt_REJECT lz4hc_compress nf_reject_ipv4 lz4_compress xt_LOG nf_log_syslog input_leds joydev nft_limit hid_multitouch xt_limit xt_addrtype xt_tcpudp xt_conntrack nf_conntrack nf_defrag_ipv6 nf_defrag_ipv4 nft_compat snd_hda_codec_alc269 snd_hda_scodec_component snd_hda_codec_realtek_lib snd_hda_codec_generic snd_hda_intel nf_tables snd_sof_pci_intel_icl snd_sof_pci_intel_cnl snd_sof_intel_hda_generic nfnetlink soundwire_intel snd_sof_intel_hda_sdw_bpt binfmt_misc snd_sof_intel_hda_common snd_soc_hdac_hda snd_sof_intel_hda_mlink snd_sof_intel_hda snd_hda_codec_hdmi soundwire_cadence snd_sof_pci
> [51971.840706]  snd_sof_xtensa_dsp snd_sof snd_sof_utils snd_soc_acpi_intel_match snd_soc_acpi_intel_sdca_quirks soundwire_generic_allocation snd_soc_acpi soundwire_bus snd_soc_sdca crc8 snd_soc_avs snd_soc_hda_codec snd_hda_ext_core snd_hda_codec hid_generic intel_uncore_frequency intel_uncore_frequency_common snd_hda_core mei_pxp mei_hdcp snd_intel_dspcfg surface_hid snd_intel_sdw_acpi ipts snd_hwdep surface_hid_core surface_platform_profile platform_profile hid intel_tcc_cooling surface_battery snd_soc_core surface_charger intel_rapl_msr snd_compress x86_pkg_temp_thermal ac97_bus snd_pcm_dmaengine intel_powerclamp snd_pcm coretemp snd_seq_midi iwlmvm snd_seq_midi_event nls_iso8859_1 snd_rawmidi gpio_keys kvm_intel surface_gpe processor_thermal_device_pci_legacy snd_seq btusb mac80211 processor_thermal_device kvm processor_thermal_wt_hint btrtl platform_temperature_control snd_seq_device btintel irqbypass processor_thermal_rfim libarc4 snd_timer btbcm btmtk processor_thermal_rapl rapl cmdlinepart iwlwifi spi_nor snd
> [51971.840733]  intel_cstate intel_rapl_common mei_me intel_wmi_thunderbolt bluetooth mtd 8250_dw intel_pmc_core soundcore mei pmt_telemetry processor_thermal_wt_req cfg80211 processor_thermal_power_floor pmt_discovery pmt_class processor_thermal_mbox int3403_thermal intel_soc_dts_iosf int340x_thermal_zone surfacepro3_button intel_pmc_ssram_telemetry mac_hid int3400_thermal surface_aggregator_registry acpi_pad soc_button_array surface_hotplug surface_acpi_notify intel_vsec acpi_tad dptf_power acpi_thermal_rel sch_fq_codel kyber_iosched msr parport_pc ppdev lp parport efi_pstore ip_tables x_tables autofs4 dm_crypt raid10 raid456 async_raid6_recov async_memcpy async_pq async_xor async_tx xor raid6_pq raid1 raid0 linear system76_io(OE) system76_acpi(OE) i915 nvme drm_buddy polyval_clmulni ttm ghash_clmulni_intel i2c_algo_bit nvme_core spi_intel_pci drm_display_helper nvme_keyring intel_lpss_pci spi_intel nvme_auth intel_lpss cec idma64 rc_core video surface_aggregator wmi crc_itu_t pinctrl_icelake aesni_intel
> [51971.840766] CPU: 5 UID: 0 PID: 74953 Comm: kworker/5:1 Tainted: G        W  OE       6.17.1-surface-2 #2 PREEMPT(voluntary) 
> [51971.840768] Tainted: [W]=WARN, [O]=OOT_MODULE, [E]=UNSIGNED_MODULE
> [51971.840769] Hardware name: Microsoft Corporation Surface Laptop 3/Surface Laptop 3, BIOS 19.101.140 04/11/2024
> [51971.840770] Workqueue: events_freezable ieee80211_restart_work [mac80211]
> [51971.840793] RIP: 0010:ieee80211_del_chanctx+0x11c/0x130 [mac80211]
> [51971.840839] Code: ee e8 88 58 00 00 65 ff 0d 61 c6 fd cc 0f 85 2f ff ff ff 0f 1f 44 00 00 e9 25 ff ff ff 4c 89 ef e8 b9 6f fc ff e9 45 ff ff ff <0f> 0b e9 35 ff ff ff 66 66 2e 0f 1f 84 00 00 00 00 00 66 90 90 90
> [51971.840840] RSP: 0018:ffffcf9f641cb808 EFLAGS: 00010246
> [51971.840841] RAX: 0000000000000000 RBX: ffff8e399b449200 RCX: 0000000000000000
> [51971.840842] RDX: 0000000000000000 RSI: 0000000000000000 RDI: 0000000000000000
> [51971.840843] RBP: ffffcf9f641cb828 R08: ffff8e399b449230 R09: 0000000000000000
> [51971.840844] R10: ffff8e3987398940 R11: ffff8e399b449230 R12: ffff8e399b4492a0
> [51971.840845] R13: ffff8e3987398940 R14: 0000000000000000 R15: ffff8e399b4492a0
> [51971.840845] FS:  0000000000000000(0000) GS:ffff8e3d4ca60000(0000) knlGS:0000000000000000
> [51971.840847] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
> [51971.840847] CR2: ffffe507405d1f30 CR3: 0000000204636005 CR4: 0000000000772ef0
> [51971.840849] PKRU: 55555554
> [51971.840849] Call Trace:
> [51971.840850]  <TASK>
> [51971.840854]  ieee80211_free_chanctx+0x93/0xe0 [mac80211]
> [51971.840892]  __ieee80211_link_release_channel+0x119/0x150 [mac80211]
> [51971.840933]  ieee80211_link_release_channel+0x2f/0x50 [mac80211]
> [51971.840975]  ieee80211_set_disassoc+0x442/0x870 [mac80211]
> [51971.841021]  ieee80211_mgd_deauth+0x125/0x4c0 [mac80211]
> [51971.841059]  ieee80211_deauth+0x18/0x30 [mac80211]
> [51971.841094]  cfg80211_mlme_deauth+0xa5/0x1e0 [cfg80211]
> [51971.841127]  cfg80211_mlme_down+0x60/0x90 [cfg80211]
> [51971.841156]  cfg80211_disconnect+0x195/0x200 [cfg80211]
> [51971.841187]  cfg80211_leave+0x147/0x1c0 [cfg80211]
> [51971.841209]  cfg80211_netdev_notifier_call+0x13e/0x500 [cfg80211]
> [51971.841230]  ? psi_task_switch+0x10a/0x2a0
> [51971.841232]  ? raw_spin_rq_unlock+0x10/0x40
> [51971.841235]  ? __dev_printk+0x39/0xa0
> [51971.841237]  ? _dev_err+0x6b/0xa0
> [51971.841240]  ? __iwl_err+0x163/0x170 [iwlwifi]
> [51971.841252]  ? rtnl_is_locked+0x15/0x20
> [51971.841255]  ? inetdev_event+0x45/0x730
> [51971.841257]  ? packet_notifier+0x131/0x270
> [51971.841258]  notifier_call_chain+0x62/0xe0
> [51971.841260]  raw_notifier_call_chain+0x16/0x30
> [51971.841262]  call_netdevice_notifiers_info+0x50/0x90
> [51971.841264]  __dev_close_many+0x67/0x220
> [51971.841267]  netif_close_many+0x98/0x170
> [51971.841269]  netif_close+0x71/0x90
> [51971.841271]  dev_close+0x2a/0x90
> [51971.841273]  cfg80211_shutdown_all_interfaces+0x57/0x110 [cfg80211]
> [51971.841294]  ieee80211_restart_work+0x13c/0x170 [mac80211]
> [51971.841318]  process_one_work+0x19c/0x3f0
> [51971.841320]  worker_thread+0x2ba/0x3d0
> [51971.841323]  kthread+0x104/0x220
> [51971.841324]  ? __pfx_worker_thread+0x10/0x10
> [51971.841327]  ? __pfx_kthread+0x10/0x10
> [51971.841328]  ret_from_fork+0x1ec/0x220
> [51971.841329]  ? __pfx_kthread+0x10/0x10
> [51971.841331]  ret_from_fork_asm+0x1a/0x30
> [51971.841334]  </TASK>
> [51971.841334] ---[ end trace 0000000000000000 ]---
> [51971.841344] wlp0s20f3: failed to remove key (1, ff:ff:ff:ff:ff:ff) from hardware (-5)
> [51971.846906] ------------[ cut here ]------------
> [51971.846908] WARNING: CPU: 5 PID: 74953 at net/mac80211/driver-ops.c:41 drv_stop+0x10b/0x120 [mac80211]
> [51971.846942] Modules linked in: vhost_net vhost vhost_iotlb tap iptable_mangle xt_CHECKSUM xt_multiport iptable_nat nf_conntrack_netlink xt_nat veth xt_mark xt_MASQUERADE bridge stp llc xt_set ip_set nft_chain_nat nf_nat xfrm_user xfrm_algo ccm rfcomm cmac algif_hash algif_skcipher af_alg snd_seq_dummy snd_hrtimer snd_hda_codec_intelhdmi overlay bnep ip6t_REJECT nf_reject_ipv6 xt_hl zram ip6t_rt 842_decompress 842_compress ipt_REJECT lz4hc_compress nf_reject_ipv4 lz4_compress xt_LOG nf_log_syslog input_leds joydev nft_limit hid_multitouch xt_limit xt_addrtype xt_tcpudp xt_conntrack nf_conntrack nf_defrag_ipv6 nf_defrag_ipv4 nft_compat snd_hda_codec_alc269 snd_hda_scodec_component snd_hda_codec_realtek_lib snd_hda_codec_generic snd_hda_intel nf_tables snd_sof_pci_intel_icl snd_sof_pci_intel_cnl snd_sof_intel_hda_generic nfnetlink soundwire_intel snd_sof_intel_hda_sdw_bpt binfmt_misc snd_sof_intel_hda_common snd_soc_hdac_hda snd_sof_intel_hda_mlink snd_sof_intel_hda snd_hda_codec_hdmi soundwire_cadence snd_sof_pci
> [51971.846977]  snd_sof_xtensa_dsp snd_sof snd_sof_utils snd_soc_acpi_intel_match snd_soc_acpi_intel_sdca_quirks soundwire_generic_allocation snd_soc_acpi soundwire_bus snd_soc_sdca crc8 snd_soc_avs snd_soc_hda_codec snd_hda_ext_core snd_hda_codec hid_generic intel_uncore_frequency intel_uncore_frequency_common snd_hda_core mei_pxp mei_hdcp snd_intel_dspcfg surface_hid snd_intel_sdw_acpi ipts snd_hwdep surface_hid_core surface_platform_profile platform_profile hid intel_tcc_cooling surface_battery snd_soc_core surface_charger intel_rapl_msr snd_compress x86_pkg_temp_thermal ac97_bus snd_pcm_dmaengine intel_powerclamp snd_pcm coretemp snd_seq_midi iwlmvm snd_seq_midi_event nls_iso8859_1 snd_rawmidi gpio_keys kvm_intel surface_gpe processor_thermal_device_pci_legacy snd_seq btusb mac80211 processor_thermal_device kvm processor_thermal_wt_hint btrtl platform_temperature_control snd_seq_device btintel irqbypass processor_thermal_rfim libarc4 snd_timer btbcm btmtk processor_thermal_rapl rapl cmdlinepart iwlwifi spi_nor snd
> [51971.847009]  intel_cstate intel_rapl_common mei_me intel_wmi_thunderbolt bluetooth mtd 8250_dw intel_pmc_core soundcore mei pmt_telemetry processor_thermal_wt_req cfg80211 processor_thermal_power_floor pmt_discovery pmt_class processor_thermal_mbox int3403_thermal intel_soc_dts_iosf int340x_thermal_zone surfacepro3_button intel_pmc_ssram_telemetry mac_hid int3400_thermal surface_aggregator_registry acpi_pad soc_button_array surface_hotplug surface_acpi_notify intel_vsec acpi_tad dptf_power acpi_thermal_rel sch_fq_codel kyber_iosched msr parport_pc ppdev lp parport efi_pstore ip_tables x_tables autofs4 dm_crypt raid10 raid456 async_raid6_recov async_memcpy async_pq async_xor async_tx xor raid6_pq raid1 raid0 linear system76_io(OE) system76_acpi(OE) i915 nvme drm_buddy polyval_clmulni ttm ghash_clmulni_intel i2c_algo_bit nvme_core spi_intel_pci drm_display_helper nvme_keyring intel_lpss_pci spi_intel nvme_auth intel_lpss cec idma64 rc_core video surface_aggregator wmi crc_itu_t pinctrl_icelake aesni_intel
> [51971.847051] CPU: 5 UID: 0 PID: 74953 Comm: kworker/5:1 Tainted: G        W  OE       6.17.1-surface-2 #2 PREEMPT(voluntary) 
> [51971.847054] Tainted: [W]=WARN, [O]=OOT_MODULE, [E]=UNSIGNED_MODULE
> [51971.847055] Hardware name: Microsoft Corporation Surface Laptop 3/Surface Laptop 3, BIOS 19.101.140 04/11/2024
> [51971.847056] Workqueue: events_freezable ieee80211_restart_work [mac80211]
> [51971.847081] RIP: 0010:drv_stop+0x10b/0x120 [mac80211]
> [51971.847105] Code: 85 c0 74 0f 48 8b 78 08 44 89 e2 48 89 de e8 ec a1 05 00 65 ff 0d 85 2f 03 cd 0f 85 2c ff ff ff 0f 1f 44 00 00 e9 22 ff ff ff <0f> 0b 5b 41 5c 5d 31 c0 31 d2 31 f6 31 ff e9 52 d3 dc cb 66 90 90
> [51971.847106] RSP: 0018:ffffcf9f641cbbf0 EFLAGS: 00010246
> [51971.847108] RAX: 0000000000000000 RBX: ffff8e3987398940 RCX: 0000000000000000
> [51971.847109] RDX: 0000000000000000 RSI: 0000000000000000 RDI: 0000000000000000
> [51971.847109] RBP: ffffcf9f641cbc00 R08: 0000000000000000 R09: 0000000000000000
> [51971.847110] R10: 0000000000000000 R11: 0000000000000000 R12: 0000000000000000
> [51971.847111] R13: 0000000000000000 R14: ffff8e3987398940 R15: ffffcf9f641cbc60
> [51971.847112] FS:  0000000000000000(0000) GS:ffff8e3d4ca60000(0000) knlGS:0000000000000000
> [51971.847113] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
> [51971.847114] CR2: ffffe507405d1f30 CR3: 00000002aeab1006 CR4: 0000000000772ef0
> [51971.847115] PKRU: 55555554
> [51971.847115] Call Trace:
> [51971.847117]  <TASK>
> [51971.847119]  ieee80211_stop_device+0x81/0x90 [mac80211]
> [51971.847158]  ieee80211_do_stop+0x72f/0x900 [mac80211]
> [51971.847189]  ? packet_notifier+0x131/0x270
> [51971.847192]  ? _raw_spin_unlock_bh+0x1d/0x30
> [51971.847195]  ? dev_reset_queue+0x40/0xb0
> [51971.847198]  ieee80211_stop+0x6c/0x100 [mac80211]
> [51971.847230]  __dev_close_many+0x109/0x220
> [51971.847233]  netif_close_many+0x98/0x170
> [51971.847235]  netif_close+0x71/0x90
> [51971.847237]  dev_close+0x2a/0x90
> [51971.847240]  cfg80211_shutdown_all_interfaces+0x57/0x110 [cfg80211]
> [51971.847269]  ieee80211_restart_work+0x13c/0x170 [mac80211]
> [51971.847294]  process_one_work+0x19c/0x3f0
> [51971.847297]  worker_thread+0x2ba/0x3d0
> [51971.847300]  kthread+0x104/0x220
> [51971.847302]  ? __pfx_worker_thread+0x10/0x10
> [51971.847304]  ? __pfx_kthread+0x10/0x10
> [51971.847306]  ret_from_fork+0x1ec/0x220
> [51971.847307]  ? __pfx_kthread+0x10/0x10
> [51971.847309]  ret_from_fork_asm+0x1a/0x30
> [51971.847312]  </TASK>
> [51971.847313] ---[ end trace 0000000000000000 ]---
> [52007.339029] iwlwifi 0000:00:14.3: SecBoot CPU1 Status: 0x5803, CPU2 Status: 0x3
> [52007.339066] iwlwifi 0000:00:14.3: WFPM_LMAC1_PD_NOTIFICATION: 0x0
> [52007.339094] iwlwifi 0000:00:14.3: HPM_SECONDARY_DEVICE_STATE: 0x42
> [52007.339125] iwlwifi 0000:00:14.3: WFPM_MAC_OTP_CFG7_ADDR: 0x0
> [52007.339153] iwlwifi 0000:00:14.3: WFPM_MAC_OTP_CFG7_DATA: 0x0
> [52007.339158] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0xa05c18
> [52007.339164] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xa05c1c
> [52007.339170] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [52007.339275] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [52007.339279] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 6
> [52007.339282] iwlwifi 0000:00:14.3: Loaded firmware version: 77.6eaf654b.0 Qu-c0-hr-b0-77.ucode
> [52007.339286] iwlwifi 0000:00:14.3: 0x00000092 | ADVANCED_SYSASSERT          
> [52007.339298] iwlwifi 0000:00:14.3: 0x000022F0 | trm_hw_status0
> [52007.339302] iwlwifi 0000:00:14.3: 0x00000000 | trm_hw_status1
> [52007.339305] iwlwifi 0000:00:14.3: 0x004C9742 | branchlink2
> [52007.339307] iwlwifi 0000:00:14.3: 0x0001539C | interruptlink1
> [52007.339310] iwlwifi 0000:00:14.3: 0x0001539C | interruptlink2
> [52007.339313] iwlwifi 0000:00:14.3: 0x00014F4A | data1
> [52007.339315] iwlwifi 0000:00:14.3: 0x0BADCAFE | data2
> [52007.339318] iwlwifi 0000:00:14.3: 0x00000000 | data3
> [52007.339321] iwlwifi 0000:00:14.3: 0x00000000 | beacon time
> [52007.339324] iwlwifi 0000:00:14.3: 0x00000000 | tsf low
> [52007.339326] iwlwifi 0000:00:14.3: 0x00000000 | tsf hi
> [52007.339329] iwlwifi 0000:00:14.3: 0x00000000 | time gp1
> [52007.339331] iwlwifi 0000:00:14.3: 0x0003C3D8 | time gp2
> [52007.339334] iwlwifi 0000:00:14.3: 0x00000001 | uCode revision type
> [52007.339337] iwlwifi 0000:00:14.3: 0x0000004D | uCode version major
> [52007.339340] iwlwifi 0000:00:14.3: 0x6EAF654B | uCode version minor
> [52007.339343] iwlwifi 0000:00:14.3: 0x00000332 | hw version
> [52007.339346] iwlwifi 0000:00:14.3: 0x00C89002 | board version
> [52007.339349] iwlwifi 0000:00:14.3: 0x00000000 | hcmd
> [52007.339351] iwlwifi 0000:00:14.3: 0x00020000 | isr0
> [52007.339354] iwlwifi 0000:00:14.3: 0x00000000 | isr1
> [52007.339357] iwlwifi 0000:00:14.3: 0x08F00002 | isr2
> [52007.339359] iwlwifi 0000:00:14.3: 0x00C0001C | isr3
> [52007.339362] iwlwifi 0000:00:14.3: 0x00000000 | isr4
> [52007.339365] iwlwifi 0000:00:14.3: 0x00000000 | last cmd Id
> [52007.339367] iwlwifi 0000:00:14.3: 0x00014F4A | wait_event
> [52007.339370] iwlwifi 0000:00:14.3: 0x00000000 | l2p_control
> [52007.339373] iwlwifi 0000:00:14.3: 0x00000000 | l2p_duration
> [52007.339375] iwlwifi 0000:00:14.3: 0x00000000 | l2p_mhvalid
> [52007.339378] iwlwifi 0000:00:14.3: 0x00000000 | l2p_addr_match
> [52007.339381] iwlwifi 0000:00:14.3: 0x0000004B | lmpm_pmg_sel
> [52007.339383] iwlwifi 0000:00:14.3: 0x00000000 | timestamp
> [52007.339386] iwlwifi 0000:00:14.3: 0x0000F81C | flow_handler
> [52007.339431] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [52007.339434] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 7
> [52007.339437] iwlwifi 0000:00:14.3: 0x20000070 | NMI_INTERRUPT_LMAC_FATAL
> [52007.339440] iwlwifi 0000:00:14.3: 0x00000000 | umac branchlink1
> [52007.339443] iwlwifi 0000:00:14.3: 0x804561EA | umac branchlink2
> [52007.339446] iwlwifi 0000:00:14.3: 0x80473712 | umac interruptlink1
> [52007.339449] iwlwifi 0000:00:14.3: 0x8045639A | umac interruptlink2
> [52007.339451] iwlwifi 0000:00:14.3: 0x00000400 | umac data1
> [52007.339454] iwlwifi 0000:00:14.3: 0x8045639A | umac data2
> [52007.339457] iwlwifi 0000:00:14.3: 0x00000000 | umac data3
> [52007.339459] iwlwifi 0000:00:14.3: 0x0000004D | umac major
> [52007.339462] iwlwifi 0000:00:14.3: 0x6EAF654B | umac minor
> [52007.339465] iwlwifi 0000:00:14.3: 0x0003C44F | frame pointer
> [52007.339467] iwlwifi 0000:00:14.3: 0xC0887EE0 | stack pointer
> [52007.339470] iwlwifi 0000:00:14.3: 0x00000000 | last host cmd
> [52007.339472] iwlwifi 0000:00:14.3: 0x00200040 | isr status reg
> [52007.339492] iwlwifi 0000:00:14.3: IML/ROM dump:
> [52007.339495] iwlwifi 0000:00:14.3: 0x00000003 | IML/ROM error/state
> [52007.339520] iwlwifi 0000:00:14.3: 0x00005803 | IML/ROM data1
> [52007.339547] iwlwifi 0000:00:14.3: 0x00000080 | IML/ROM WFPM_AUTH_KEY_0
> [52007.339571] iwlwifi 0000:00:14.3: Fseq Registers:
> [52007.339590] iwlwifi 0000:00:14.3: 0x60000000 | FSEQ_ERROR_CODE
> [52007.339595] iwlwifi 0000:00:14.3: 0x80290033 | FSEQ_TOP_INIT_VERSION
> [52007.339614] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_CNVIO_INIT_VERSION
> [52007.339635] iwlwifi 0000:00:14.3: 0x0000A492 | FSEQ_OTP_VERSION
> [52007.339657] iwlwifi 0000:00:14.3: 0x00000003 | FSEQ_TOP_CONTENT_VERSION
> [52007.339678] iwlwifi 0000:00:14.3: 0x4552414E | FSEQ_ALIVE_TOKEN
> [52007.339683] iwlwifi 0000:00:14.3: 0x02000300 | FSEQ_CNVI_ID
> [52007.339703] iwlwifi 0000:00:14.3: 0x01300504 | FSEQ_CNVR_ID
> [52007.339708] iwlwifi 0000:00:14.3: 0x02000300 | CNVI_AUX_MISC_CHIP
> [52007.339729] iwlwifi 0000:00:14.3: 0x01300504 | CNVR_AUX_MISC_CHIP
> [52007.339751] iwlwifi 0000:00:14.3: 0x05B0905B | CNVR_SCU_SD_REGS_SD_REG_DIG_DCDC_VTRIM
> [52007.339772] iwlwifi 0000:00:14.3: 0x0000025B | CNVR_SCU_SD_REGS_SD_REG_ACTIVE_VDIG_MIRROR
> [52007.339792] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_PREV_CNVIO_INIT_VERSION
> [52007.339813] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_WIFI_FSEQ_VERSION
> [52007.339834] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_BT_FSEQ_VERSION
> [52007.339839] iwlwifi 0000:00:14.3: 0x00000136 | FSEQ_CLASS_TP_VERSION
> [52007.339865] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0x80473220
> [52007.339884] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xd0
> [52007.339891] iwlwifi 0000:00:14.3: Failed to start RT ucode: -110
> [52007.339897] iwlwifi 0000:00:14.3: Failed to start RT ucode: -110
> [52007.339913] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [52008.315027] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 4 fired (delay=0ms).
> [52008.341268] iwlwifi 0000:00:14.3: mac start retry 0
> [52010.410050] iwlwifi 0000:00:14.3: SecBoot CPU1 Status: 0x57e1, CPU2 Status: 0x3
> [52010.410082] iwlwifi 0000:00:14.3: WFPM_LMAC1_PD_NOTIFICATION: 0x0
> [52010.410109] iwlwifi 0000:00:14.3: HPM_SECONDARY_DEVICE_STATE: 0x42
> [52010.410137] iwlwifi 0000:00:14.3: WFPM_MAC_OTP_CFG7_ADDR: 0x0
> [52010.410188] iwlwifi 0000:00:14.3: WFPM_MAC_OTP_CFG7_DATA: 0x0
> [52010.410191] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0xa05c18
> [52010.410194] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xa05c1c
> [52010.410198] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [52010.410300] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [52010.410303] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 6
> [52010.410306] iwlwifi 0000:00:14.3: Loaded firmware version: 77.6eaf654b.0 Qu-c0-hr-b0-77.ucode
> [52010.410310] iwlwifi 0000:00:14.3: 0x00000092 | ADVANCED_SYSASSERT          
> [52010.410314] iwlwifi 0000:00:14.3: 0x000022F0 | trm_hw_status0
> [52010.410317] iwlwifi 0000:00:14.3: 0x00000000 | trm_hw_status1
> [52010.410320] iwlwifi 0000:00:14.3: 0x004C9742 | branchlink2
> [52010.410323] iwlwifi 0000:00:14.3: 0x0001539C | interruptlink1
> [52010.410326] iwlwifi 0000:00:14.3: 0x0001539C | interruptlink2
> [52010.410329] iwlwifi 0000:00:14.3: 0x00014F4A | data1
> [52010.410331] iwlwifi 0000:00:14.3: 0x0BADCAFE | data2
> [52010.410334] iwlwifi 0000:00:14.3: 0x00000000 | data3
> [52010.410337] iwlwifi 0000:00:14.3: 0x00000000 | beacon time
> [52010.410340] iwlwifi 0000:00:14.3: 0x00000000 | tsf low
> [52010.410342] iwlwifi 0000:00:14.3: 0x00000000 | tsf hi
> [52010.410345] iwlwifi 0000:00:14.3: 0x00000000 | time gp1
> [52010.410348] iwlwifi 0000:00:14.3: 0x0003C323 | time gp2
> [52010.410350] iwlwifi 0000:00:14.3: 0x00000001 | uCode revision type
> [52010.410353] iwlwifi 0000:00:14.3: 0x0000004D | uCode version major
> [52010.410356] iwlwifi 0000:00:14.3: 0x6EAF654B | uCode version minor
> [52010.410359] iwlwifi 0000:00:14.3: 0x00000332 | hw version
> [52010.410362] iwlwifi 0000:00:14.3: 0x00C89002 | board version
> [52010.410365] iwlwifi 0000:00:14.3: 0x00000000 | hcmd
> [52010.410367] iwlwifi 0000:00:14.3: 0x00020000 | isr0
> [52010.410370] iwlwifi 0000:00:14.3: 0x00000000 | isr1
> [52010.410373] iwlwifi 0000:00:14.3: 0x08F00002 | isr2
> [52010.410375] iwlwifi 0000:00:14.3: 0x00C0001C | isr3
> [52010.410378] iwlwifi 0000:00:14.3: 0x00000000 | isr4
> [52010.410381] iwlwifi 0000:00:14.3: 0x00000000 | last cmd Id
> [52010.410383] iwlwifi 0000:00:14.3: 0x00014F4A | wait_event
> [52010.410386] iwlwifi 0000:00:14.3: 0x00000000 | l2p_control
> [52010.410389] iwlwifi 0000:00:14.3: 0x00000000 | l2p_duration
> [52010.410391] iwlwifi 0000:00:14.3: 0x00000000 | l2p_mhvalid
> [52010.410394] iwlwifi 0000:00:14.3: 0x00000000 | l2p_addr_match
> [52010.410397] iwlwifi 0000:00:14.3: 0x0000004B | lmpm_pmg_sel
> [52010.410399] iwlwifi 0000:00:14.3: 0x00000000 | timestamp
> [52010.410402] iwlwifi 0000:00:14.3: 0x0000F81C | flow_handler
> [52010.410446] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [52010.410449] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 7
> [52010.410452] iwlwifi 0000:00:14.3: 0x20000070 | NMI_INTERRUPT_LMAC_FATAL
> [52010.410455] iwlwifi 0000:00:14.3: 0x00000000 | umac branchlink1
> [52010.410458] iwlwifi 0000:00:14.3: 0x804561EA | umac branchlink2
> [52010.410461] iwlwifi 0000:00:14.3: 0x80473712 | umac interruptlink1
> [52010.410464] iwlwifi 0000:00:14.3: 0x8045639A | umac interruptlink2
> [52010.410467] iwlwifi 0000:00:14.3: 0x00000400 | umac data1
> [52010.410469] iwlwifi 0000:00:14.3: 0x8045639A | umac data2
> [52010.410472] iwlwifi 0000:00:14.3: 0x00000000 | umac data3
> [52010.410475] iwlwifi 0000:00:14.3: 0x0000004D | umac major
> [52010.410477] iwlwifi 0000:00:14.3: 0x6EAF654B | umac minor
> [52010.410480] iwlwifi 0000:00:14.3: 0x0003C39B | frame pointer
> [52010.410483] iwlwifi 0000:00:14.3: 0xC0887EE0 | stack pointer
> [52010.410485] iwlwifi 0000:00:14.3: 0x00000000 | last host cmd
> [52010.410488] iwlwifi 0000:00:14.3: 0x00200040 | isr status reg
> [52010.410511] iwlwifi 0000:00:14.3: IML/ROM dump:
> [52010.410514] iwlwifi 0000:00:14.3: 0x00000003 | IML/ROM error/state
> [52010.410538] iwlwifi 0000:00:14.3: 0x000057E1 | IML/ROM data1
> [52010.410565] iwlwifi 0000:00:14.3: 0x00000080 | IML/ROM WFPM_AUTH_KEY_0
> [52010.410589] iwlwifi 0000:00:14.3: Fseq Registers:
> [52010.410608] iwlwifi 0000:00:14.3: 0x60000000 | FSEQ_ERROR_CODE
> [52010.410629] iwlwifi 0000:00:14.3: 0x80290033 | FSEQ_TOP_INIT_VERSION
> [52010.410650] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_CNVIO_INIT_VERSION
> [52010.410671] iwlwifi 0000:00:14.3: 0x0000A492 | FSEQ_OTP_VERSION
> [52010.410692] iwlwifi 0000:00:14.3: 0x00000003 | FSEQ_TOP_CONTENT_VERSION
> [52010.410713] iwlwifi 0000:00:14.3: 0x4552414E | FSEQ_ALIVE_TOKEN
> [52010.410734] iwlwifi 0000:00:14.3: 0x02000300 | FSEQ_CNVI_ID
> [52010.410739] iwlwifi 0000:00:14.3: 0x01300504 | FSEQ_CNVR_ID
> [52010.410759] iwlwifi 0000:00:14.3: 0x02000300 | CNVI_AUX_MISC_CHIP
> [52010.410766] iwlwifi 0000:00:14.3: 0x01300504 | CNVR_AUX_MISC_CHIP
> [52010.410787] iwlwifi 0000:00:14.3: 0x05B0905B | CNVR_SCU_SD_REGS_SD_REG_DIG_DCDC_VTRIM
> [52010.410809] iwlwifi 0000:00:14.3: 0x0000025B | CNVR_SCU_SD_REGS_SD_REG_ACTIVE_VDIG_MIRROR
> [52010.410829] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_PREV_CNVIO_INIT_VERSION
> [52010.410850] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_WIFI_FSEQ_VERSION
> [52010.410871] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_BT_FSEQ_VERSION
> [52010.410876] iwlwifi 0000:00:14.3: 0x00000136 | FSEQ_CLASS_TP_VERSION
> [52010.410903] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0x80473220
> [52010.410945] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xd0
> [52010.410974] iwlwifi 0000:00:14.3: Failed to start RT ucode: -110
> [52010.410980] iwlwifi 0000:00:14.3: Failed to start RT ucode: -110
> [52010.410985] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [52011.373535] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 4 fired (delay=0ms).
> [52011.400161] iwlwifi 0000:00:14.3: mac start retry 0
> [52064.795186] iwlwifi 0000:00:14.3: Microcode SW error detected. Restarting 0x0.
> [52064.795274] iwlwifi 0000:00:14.3: Failed to start RT ucode: -5
> [52064.795285] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [52064.795311] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [52064.795315] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 6
> [52064.795319] iwlwifi 0000:00:14.3: Loaded firmware version: 77.6eaf654b.0 Qu-c0-hr-b0-77.ucode
> [52064.795323] iwlwifi 0000:00:14.3: 0x00000091 | ADVANCED_SYSASSERT          
> [52064.795327] iwlwifi 0000:00:14.3: 0x0000A2F0 | trm_hw_status0
> [52064.795339] iwlwifi 0000:00:14.3: 0x00000000 | trm_hw_status1
> [52064.795342] iwlwifi 0000:00:14.3: 0x004C9742 | branchlink2
> [52064.795345] iwlwifi 0000:00:14.3: 0x004C5220 | interruptlink1
> [52064.795348] iwlwifi 0000:00:14.3: 0x004C5220 | interruptlink2
> [52064.795350] iwlwifi 0000:00:14.3: 0x00013186 | data1
> [52064.795353] iwlwifi 0000:00:14.3: 0x00010000 | data2
> [52064.795356] iwlwifi 0000:00:14.3: 0x00000000 | data3
> [52064.795358] iwlwifi 0000:00:14.3: 0x00000000 | beacon time
> [52064.795361] iwlwifi 0000:00:14.3: 0x00000000 | tsf low
> [52064.795364] iwlwifi 0000:00:14.3: 0x00000000 | tsf hi
> [52064.795366] iwlwifi 0000:00:14.3: 0x00000000 | time gp1
> [52064.795369] iwlwifi 0000:00:14.3: 0x0001AE4F | time gp2
> [52064.795371] iwlwifi 0000:00:14.3: 0x00000001 | uCode revision type
> [52064.795374] iwlwifi 0000:00:14.3: 0x0000004D | uCode version major
> [52064.795377] iwlwifi 0000:00:14.3: 0x6EAF654B | uCode version minor
> [52064.795380] iwlwifi 0000:00:14.3: 0x00000332 | hw version
> [52064.795383] iwlwifi 0000:00:14.3: 0x00C89002 | board version
> [52064.795386] iwlwifi 0000:00:14.3: 0x8014FD28 | hcmd
> [52064.795388] iwlwifi 0000:00:14.3: 0xE2920000 | isr0
> [52064.795391] iwlwifi 0000:00:14.3: 0x00000000 | isr1
> [52064.795394] iwlwifi 0000:00:14.3: 0x08F00002 | isr2
> [52064.795396] iwlwifi 0000:00:14.3: 0x00C0000C | isr3
> [52064.795399] iwlwifi 0000:00:14.3: 0x00000000 | isr4
> [52064.795402] iwlwifi 0000:00:14.3: 0x00000000 | last cmd Id
> [52064.795404] iwlwifi 0000:00:14.3: 0x00013186 | wait_event
> [52064.795407] iwlwifi 0000:00:14.3: 0x00000000 | l2p_control
> [52064.795410] iwlwifi 0000:00:14.3: 0x00000000 | l2p_duration
> [52064.795412] iwlwifi 0000:00:14.3: 0x00000000 | l2p_mhvalid
> [52064.795415] iwlwifi 0000:00:14.3: 0x00000000 | l2p_addr_match
> [52064.795417] iwlwifi 0000:00:14.3: 0x00000000 | lmpm_pmg_sel
> [52064.795420] iwlwifi 0000:00:14.3: 0x00000000 | timestamp
> [52064.795423] iwlwifi 0000:00:14.3: 0x00000020 | flow_handler
> [52064.795466] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [52064.795469] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 7
> [52064.795472] iwlwifi 0000:00:14.3: 0x20000070 | NMI_INTERRUPT_LMAC_FATAL
> [52064.795476] iwlwifi 0000:00:14.3: 0x00000000 | umac branchlink1
> [52064.795478] iwlwifi 0000:00:14.3: 0x804561EA | umac branchlink2
> [52064.795481] iwlwifi 0000:00:14.3: 0x80473712 | umac interruptlink1
> [52064.795484] iwlwifi 0000:00:14.3: 0x80473712 | umac interruptlink2
> [52064.795487] iwlwifi 0000:00:14.3: 0x00000400 | umac data1
> [52064.795489] iwlwifi 0000:00:14.3: 0x80473712 | umac data2
> [52064.795492] iwlwifi 0000:00:14.3: 0x00000000 | umac data3
> [52064.795495] iwlwifi 0000:00:14.3: 0x0000004D | umac major
> [52064.795497] iwlwifi 0000:00:14.3: 0x6EAF654B | umac minor
> [52064.795500] iwlwifi 0000:00:14.3: 0x0001AEE8 | frame pointer
> [52064.795503] iwlwifi 0000:00:14.3: 0xC0886260 | stack pointer
> [52064.795505] iwlwifi 0000:00:14.3: 0x00010C00 | last host cmd
> [52064.795508] iwlwifi 0000:00:14.3: 0x00000000 | isr status reg
> [52064.795531] iwlwifi 0000:00:14.3: IML/ROM dump:
> [52064.795533] iwlwifi 0000:00:14.3: 0x00000003 | IML/ROM error/state
> [52064.795558] iwlwifi 0000:00:14.3: 0x00005841 | IML/ROM data1
> [52064.795585] iwlwifi 0000:00:14.3: 0x00000080 | IML/ROM WFPM_AUTH_KEY_0
> [52064.795609] iwlwifi 0000:00:14.3: Fseq Registers:
> [52064.795629] iwlwifi 0000:00:14.3: 0x60000000 | FSEQ_ERROR_CODE
> [52064.795650] iwlwifi 0000:00:14.3: 0x80290033 | FSEQ_TOP_INIT_VERSION
> [52064.795655] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_CNVIO_INIT_VERSION
> [52064.795675] iwlwifi 0000:00:14.3: 0x0000A492 | FSEQ_OTP_VERSION
> [52064.795696] iwlwifi 0000:00:14.3: 0x00000003 | FSEQ_TOP_CONTENT_VERSION
> [52064.795722] iwlwifi 0000:00:14.3: 0x4552414E | FSEQ_ALIVE_TOKEN
> [52064.795743] iwlwifi 0000:00:14.3: 0x02000300 | FSEQ_CNVI_ID
> [52064.795747] iwlwifi 0000:00:14.3: 0x01300504 | FSEQ_CNVR_ID
> [52064.795767] iwlwifi 0000:00:14.3: 0x02000300 | CNVI_AUX_MISC_CHIP
> [52064.795774] iwlwifi 0000:00:14.3: 0x01300504 | CNVR_AUX_MISC_CHIP
> [52064.795796] iwlwifi 0000:00:14.3: 0x05B0905B | CNVR_SCU_SD_REGS_SD_REG_DIG_DCDC_VTRIM
> [52064.795817] iwlwifi 0000:00:14.3: 0x0000025B | CNVR_SCU_SD_REGS_SD_REG_ACTIVE_VDIG_MIRROR
> [52064.795837] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_PREV_CNVIO_INIT_VERSION
> [52064.795858] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_WIFI_FSEQ_VERSION
> [52064.795879] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_BT_FSEQ_VERSION
> [52064.795901] iwlwifi 0000:00:14.3: 0x00000136 | FSEQ_CLASS_TP_VERSION
> [52064.795929] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0x80473220
> [52064.795948] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xd0
> [52065.416091] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 4 fired (delay=0ms).
> [52066.166808] iwlwifi 0000:00:14.3: Microcode SW error detected. Restarting 0x0.
> [52066.166856] iwlwifi 0000:00:14.3: Failed to start RT ucode: -5
> [52066.166867] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [52066.166909] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [52066.166914] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 6
> [52066.166919] iwlwifi 0000:00:14.3: Loaded firmware version: 77.6eaf654b.0 Qu-c0-hr-b0-77.ucode
> [52066.166923] iwlwifi 0000:00:14.3: 0x00000090 | ADVANCED_SYSASSERT          
> [52066.166929] iwlwifi 0000:00:14.3: 0x0000A2F0 | trm_hw_status0
> [52066.166932] iwlwifi 0000:00:14.3: 0x00000000 | trm_hw_status1
> [52066.166936] iwlwifi 0000:00:14.3: 0x004C9742 | branchlink2
> [52066.166940] iwlwifi 0000:00:14.3: 0x004C4394 | interruptlink1
> [52066.166944] iwlwifi 0000:00:14.3: 0x004C4394 | interruptlink2
> [52066.166947] iwlwifi 0000:00:14.3: 0x00013186 | data1
> [52066.166951] iwlwifi 0000:00:14.3: 0x00000000 | data2
> [52066.166954] iwlwifi 0000:00:14.3: 0x00000000 | data3
> [52066.166957] iwlwifi 0000:00:14.3: 0x00000000 | beacon time
> [52066.166961] iwlwifi 0000:00:14.3: 0x00000000 | tsf low
> [52066.166964] iwlwifi 0000:00:14.3: 0x00000000 | tsf hi
> [52066.166968] iwlwifi 0000:00:14.3: 0x00000000 | time gp1
> [52066.166971] iwlwifi 0000:00:14.3: 0x000503B3 | time gp2
> [52066.166975] iwlwifi 0000:00:14.3: 0x00000001 | uCode revision type
> [52066.166978] iwlwifi 0000:00:14.3: 0x0000004D | uCode version major
> [52066.166982] iwlwifi 0000:00:14.3: 0x6EAF654B | uCode version minor
> [52066.166986] iwlwifi 0000:00:14.3: 0x00000332 | hw version
> [52066.166989] iwlwifi 0000:00:14.3: 0x00C89002 | board version
> [52066.166993] iwlwifi 0000:00:14.3: 0x8017FD28 | hcmd
> [52066.167005] iwlwifi 0000:00:14.3: 0x20028000 | isr0
> [52066.167008] iwlwifi 0000:00:14.3: 0x00000000 | isr1
> [52066.167012] iwlwifi 0000:00:14.3: 0x08F00002 | isr2
> [52066.167015] iwlwifi 0000:00:14.3: 0x04C0001C | isr3
> [52066.167019] iwlwifi 0000:00:14.3: 0x00000000 | isr4
> [52066.167036] iwlwifi 0000:00:14.3: 0x00000000 | last cmd Id
> [52066.167040] iwlwifi 0000:00:14.3: 0x00013186 | wait_event
> [52066.167043] iwlwifi 0000:00:14.3: 0x00000000 | l2p_control
> [52066.167047] iwlwifi 0000:00:14.3: 0x00000000 | l2p_duration
> [52066.167050] iwlwifi 0000:00:14.3: 0x00000000 | l2p_mhvalid
> [52066.167054] iwlwifi 0000:00:14.3: 0x00000000 | l2p_addr_match
> [52066.167057] iwlwifi 0000:00:14.3: 0x00000009 | lmpm_pmg_sel
> [52066.167061] iwlwifi 0000:00:14.3: 0x00000000 | timestamp
> [52066.167064] iwlwifi 0000:00:14.3: 0x00000020 | flow_handler
> [52066.167127] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [52066.167131] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 7
> [52066.167135] iwlwifi 0000:00:14.3: 0x20000070 | NMI_INTERRUPT_LMAC_FATAL
> [52066.167140] iwlwifi 0000:00:14.3: 0x00000000 | umac branchlink1
> [52066.167144] iwlwifi 0000:00:14.3: 0x804561EA | umac branchlink2
> [52066.167147] iwlwifi 0000:00:14.3: 0x80473712 | umac interruptlink1
> [52066.167151] iwlwifi 0000:00:14.3: 0x80473712 | umac interruptlink2
> [52066.167155] iwlwifi 0000:00:14.3: 0x00000400 | umac data1
> [52066.167158] iwlwifi 0000:00:14.3: 0x80473712 | umac data2
> [52066.167162] iwlwifi 0000:00:14.3: 0x00000000 | umac data3
> [52066.167165] iwlwifi 0000:00:14.3: 0x0000004D | umac major
> [52066.167169] iwlwifi 0000:00:14.3: 0x6EAF654B | umac minor
> [52066.167172] iwlwifi 0000:00:14.3: 0x00050426 | frame pointer
> [52066.167176] iwlwifi 0000:00:14.3: 0xC0886260 | stack pointer
> [52066.167179] iwlwifi 0000:00:14.3: 0x00010C00 | last host cmd
> [52066.167183] iwlwifi 0000:00:14.3: 0x00000000 | isr status reg
> [52066.167207] iwlwifi 0000:00:14.3: IML/ROM dump:
> [52066.167210] iwlwifi 0000:00:14.3: 0x00000003 | IML/ROM error/state
> [52066.167235] iwlwifi 0000:00:14.3: 0x00005827 | IML/ROM data1
> [52066.167262] iwlwifi 0000:00:14.3: 0x00000080 | IML/ROM WFPM_AUTH_KEY_0
> [52066.167286] iwlwifi 0000:00:14.3: Fseq Registers:
> [52066.167306] iwlwifi 0000:00:14.3: 0x60000000 | FSEQ_ERROR_CODE
> [52066.167327] iwlwifi 0000:00:14.3: 0x80290033 | FSEQ_TOP_INIT_VERSION
> [52066.167348] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_CNVIO_INIT_VERSION
> [52066.167370] iwlwifi 0000:00:14.3: 0x0000A492 | FSEQ_OTP_VERSION
> [52066.167391] iwlwifi 0000:00:14.3: 0x00000003 | FSEQ_TOP_CONTENT_VERSION
> [52066.167412] iwlwifi 0000:00:14.3: 0x4552414E | FSEQ_ALIVE_TOKEN
> [52066.167434] iwlwifi 0000:00:14.3: 0x02000300 | FSEQ_CNVI_ID
> [52066.167456] iwlwifi 0000:00:14.3: 0x01300504 | FSEQ_CNVR_ID
> [52066.167477] iwlwifi 0000:00:14.3: 0x02000300 | CNVI_AUX_MISC_CHIP
> [52066.167501] iwlwifi 0000:00:14.3: 0x01300504 | CNVR_AUX_MISC_CHIP
> [52066.167522] iwlwifi 0000:00:14.3: 0x05B0905B | CNVR_SCU_SD_REGS_SD_REG_DIG_DCDC_VTRIM
> [52066.167544] iwlwifi 0000:00:14.3: 0x0000025B | CNVR_SCU_SD_REGS_SD_REG_ACTIVE_VDIG_MIRROR
> [52066.167564] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_PREV_CNVIO_INIT_VERSION
> [52066.167585] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_WIFI_FSEQ_VERSION
> [52066.167606] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_BT_FSEQ_VERSION
> [52066.167628] iwlwifi 0000:00:14.3: 0x00000136 | FSEQ_CLASS_TP_VERSION
> [52066.167656] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0x80473220
> [52066.167675] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xd0
> [52066.777261] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 4 fired (delay=0ms).
> [52070.058145] iwlwifi 0000:00:14.3: SecBoot CPU1 Status: 0x57f5, CPU2 Status: 0x3
> [52070.058182] iwlwifi 0000:00:14.3: WFPM_LMAC1_PD_NOTIFICATION: 0x0
> [52070.058209] iwlwifi 0000:00:14.3: HPM_SECONDARY_DEVICE_STATE: 0x42
> [52070.058237] iwlwifi 0000:00:14.3: WFPM_MAC_OTP_CFG7_ADDR: 0x0
> [52070.058265] iwlwifi 0000:00:14.3: WFPM_MAC_OTP_CFG7_DATA: 0x0
> [52070.058270] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0xa05c18
> [52070.058276] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xa05c1c
> [52070.058282] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [52070.058389] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [52070.058393] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 6
> [52070.058399] iwlwifi 0000:00:14.3: Loaded firmware version: 77.6eaf654b.0 Qu-c0-hr-b0-77.ucode
> [52070.058404] iwlwifi 0000:00:14.3: 0x00000090 | ADVANCED_SYSASSERT          
> [52070.058410] iwlwifi 0000:00:14.3: 0x000022F0 | trm_hw_status0
> [52070.058415] iwlwifi 0000:00:14.3: 0x00000000 | trm_hw_status1
> [52070.058420] iwlwifi 0000:00:14.3: 0x004C9742 | branchlink2
> [52070.058426] iwlwifi 0000:00:14.3: 0x0001A2AA | interruptlink1
> [52070.058431] iwlwifi 0000:00:14.3: 0x0001A2AA | interruptlink2
> [52070.058436] iwlwifi 0000:00:14.3: 0x00014F4A | data1
> [52070.058441] iwlwifi 0000:00:14.3: 0x00000000 | data2
> [52070.058446] iwlwifi 0000:00:14.3: 0x00000000 | data3
> [52070.058450] iwlwifi 0000:00:14.3: 0x00000000 | beacon time
> [52070.058455] iwlwifi 0000:00:14.3: 0x00000000 | tsf low
> [52070.058459] iwlwifi 0000:00:14.3: 0x00000000 | tsf hi
> [52070.058463] iwlwifi 0000:00:14.3: 0x00000000 | time gp1
> [52070.058467] iwlwifi 0000:00:14.3: 0x0003C389 | time gp2
> [52070.058471] iwlwifi 0000:00:14.3: 0x00000001 | uCode revision type
> [52070.058476] iwlwifi 0000:00:14.3: 0x0000004D | uCode version major
> [52070.058481] iwlwifi 0000:00:14.3: 0x6EAF654B | uCode version minor
> [52070.058486] iwlwifi 0000:00:14.3: 0x00000332 | hw version
> [52070.058491] iwlwifi 0000:00:14.3: 0x00C89002 | board version
> [52070.058496] iwlwifi 0000:00:14.3: 0x00000000 | hcmd
> [52070.058501] iwlwifi 0000:00:14.3: 0x00020000 | isr0
> [52070.058506] iwlwifi 0000:00:14.3: 0x00080000 | isr1
> [52070.058510] iwlwifi 0000:00:14.3: 0x08F00002 | isr2
> [52070.058515] iwlwifi 0000:00:14.3: 0x00C0001C | isr3
> [52070.058520] iwlwifi 0000:00:14.3: 0x00000001 | isr4
> [52070.058525] iwlwifi 0000:00:14.3: 0x00000000 | last cmd Id
> [52070.058529] iwlwifi 0000:00:14.3: 0x00014F4A | wait_event
> [52070.058534] iwlwifi 0000:00:14.3: 0x00000000 | l2p_control
> [52070.058539] iwlwifi 0000:00:14.3: 0x00000000 | l2p_duration
> [52070.058544] iwlwifi 0000:00:14.3: 0x00000000 | l2p_mhvalid
> [52070.058549] iwlwifi 0000:00:14.3: 0x00000000 | l2p_addr_match
> [52070.058554] iwlwifi 0000:00:14.3: 0x0000000B | lmpm_pmg_sel
> [52070.058559] iwlwifi 0000:00:14.3: 0x00000000 | timestamp
> [52070.058562] iwlwifi 0000:00:14.3: 0x0000F81C | flow_handler
> [52070.058610] iwlwifi 0000:00:14.3: Start IWL Error Log Dump:
> [52070.058615] iwlwifi 0000:00:14.3: Transport status: 0x00000242, valid: 7
> [52070.058620] iwlwifi 0000:00:14.3: 0x20000070 | NMI_INTERRUPT_LMAC_FATAL
> [52070.058627] iwlwifi 0000:00:14.3: 0x00000000 | umac branchlink1
> [52070.058631] iwlwifi 0000:00:14.3: 0x804561EA | umac branchlink2
> [52070.058635] iwlwifi 0000:00:14.3: 0x80473712 | umac interruptlink1
> [52070.058640] iwlwifi 0000:00:14.3: 0x80456398 | umac interruptlink2
> [52070.058644] iwlwifi 0000:00:14.3: 0x00000400 | umac data1
> [52070.058649] iwlwifi 0000:00:14.3: 0x80456398 | umac data2
> [52070.058653] iwlwifi 0000:00:14.3: 0x00000000 | umac data3
> [52070.058658] iwlwifi 0000:00:14.3: 0x0000004D | umac major
> [52070.058662] iwlwifi 0000:00:14.3: 0x6EAF654B | umac minor
> [52070.058666] iwlwifi 0000:00:14.3: 0x0003C3F8 | frame pointer
> [52070.058671] iwlwifi 0000:00:14.3: 0xC0887EE4 | stack pointer
> [52070.058675] iwlwifi 0000:00:14.3: 0x00000000 | last host cmd
> [52070.058679] iwlwifi 0000:00:14.3: 0x00200040 | isr status reg
> [52070.058707] iwlwifi 0000:00:14.3: IML/ROM dump:
> [52070.058709] iwlwifi 0000:00:14.3: 0x00000003 | IML/ROM error/state
> [52070.058733] iwlwifi 0000:00:14.3: 0x000057F5 | IML/ROM data1
> [52070.058760] iwlwifi 0000:00:14.3: 0x00000080 | IML/ROM WFPM_AUTH_KEY_0
> [52070.058784] iwlwifi 0000:00:14.3: Fseq Registers:
> [52070.058803] iwlwifi 0000:00:14.3: 0x60000000 | FSEQ_ERROR_CODE
> [52070.058808] iwlwifi 0000:00:14.3: 0x80290033 | FSEQ_TOP_INIT_VERSION
> [52070.058828] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_CNVIO_INIT_VERSION
> [52070.058849] iwlwifi 0000:00:14.3: 0x0000A492 | FSEQ_OTP_VERSION
> [52070.058854] iwlwifi 0000:00:14.3: 0x00000003 | FSEQ_TOP_CONTENT_VERSION
> [52070.058874] iwlwifi 0000:00:14.3: 0x4552414E | FSEQ_ALIVE_TOKEN
> [52070.058878] iwlwifi 0000:00:14.3: 0x02000300 | FSEQ_CNVI_ID
> [52070.058898] iwlwifi 0000:00:14.3: 0x01300504 | FSEQ_CNVR_ID
> [52070.058902] iwlwifi 0000:00:14.3: 0x02000300 | CNVI_AUX_MISC_CHIP
> [52070.058924] iwlwifi 0000:00:14.3: 0x01300504 | CNVR_AUX_MISC_CHIP
> [52070.058946] iwlwifi 0000:00:14.3: 0x05B0905B | CNVR_SCU_SD_REGS_SD_REG_DIG_DCDC_VTRIM
> [52070.058967] iwlwifi 0000:00:14.3: 0x0000025B | CNVR_SCU_SD_REGS_SD_REG_ACTIVE_VDIG_MIRROR
> [52070.058986] iwlwifi 0000:00:14.3: 0x00090006 | FSEQ_PREV_CNVIO_INIT_VERSION
> [52070.059008] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_WIFI_FSEQ_VERSION
> [52070.059012] iwlwifi 0000:00:14.3: 0x00290033 | FSEQ_BT_FSEQ_VERSION
> [52070.059052] iwlwifi 0000:00:14.3: 0x00000136 | FSEQ_CLASS_TP_VERSION
> [52070.059096] iwlwifi 0000:00:14.3: UMAC CURRENT PC: 0x80473220
> [52070.059116] iwlwifi 0000:00:14.3: LMAC1 CURRENT PC: 0xd0
> [52070.059123] iwlwifi 0000:00:14.3: Failed to start RT ucode: -110
> [52070.059127] iwlwifi 0000:00:14.3: Failed to start RT ucode: -110
> [52070.059130] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 13 fired (delay=0ms).
> [52071.033725] iwlwifi 0000:00:14.3: WRT: Collecting data: ini trigger 4 fired (delay=0ms).
> [52071.439139] iwlwifi 0000:00:14.3: mac start retry 0
> [52159.495059] ------------[ cut here ]------------
> [52159.495065] WARNING: CPU: 5 PID: 760 at drivers/net/wireless/intel/iwlwifi/mvm/mac-ctxt.c:274 iwl_mvm_mac_ctxt_init+0x217/0x230 [iwlmvm]
> [52159.495124] Modules linked in: vhost_net vhost vhost_iotlb tap iptable_mangle xt_CHECKSUM xt_multiport iptable_nat nf_conntrack_netlink xt_nat veth xt_mark xt_MASQUERADE bridge stp llc xt_set ip_set nft_chain_nat nf_nat xfrm_user xfrm_algo ccm rfcomm cmac algif_hash algif_skcipher af_alg snd_seq_dummy snd_hrtimer snd_hda_codec_intelhdmi overlay bnep ip6t_REJECT nf_reject_ipv6 xt_hl zram ip6t_rt 842_decompress 842_compress ipt_REJECT lz4hc_compress nf_reject_ipv4 lz4_compress xt_LOG nf_log_syslog input_leds joydev nft_limit hid_multitouch xt_limit xt_addrtype xt_tcpudp xt_conntrack nf_conntrack nf_defrag_ipv6 nf_defrag_ipv4 nft_compat snd_hda_codec_alc269 snd_hda_scodec_component snd_hda_codec_realtek_lib snd_hda_codec_generic snd_hda_intel nf_tables snd_sof_pci_intel_icl snd_sof_pci_intel_cnl snd_sof_intel_hda_generic nfnetlink soundwire_intel snd_sof_intel_hda_sdw_bpt binfmt_misc snd_sof_intel_hda_common snd_soc_hdac_hda snd_sof_intel_hda_mlink snd_sof_intel_hda snd_hda_codec_hdmi soundwire_cadence snd_sof_pci
> [52159.495207]  snd_sof_xtensa_dsp snd_sof snd_sof_utils snd_soc_acpi_intel_match snd_soc_acpi_intel_sdca_quirks soundwire_generic_allocation snd_soc_acpi soundwire_bus snd_soc_sdca crc8 snd_soc_avs snd_soc_hda_codec snd_hda_ext_core snd_hda_codec hid_generic intel_uncore_frequency intel_uncore_frequency_common snd_hda_core mei_pxp mei_hdcp snd_intel_dspcfg surface_hid snd_intel_sdw_acpi ipts snd_hwdep surface_hid_core surface_platform_profile platform_profile hid intel_tcc_cooling surface_battery snd_soc_core surface_charger intel_rapl_msr snd_compress x86_pkg_temp_thermal ac97_bus snd_pcm_dmaengine intel_powerclamp snd_pcm coretemp snd_seq_midi iwlmvm snd_seq_midi_event nls_iso8859_1 snd_rawmidi gpio_keys kvm_intel surface_gpe processor_thermal_device_pci_legacy snd_seq btusb mac80211 processor_thermal_device kvm processor_thermal_wt_hint btrtl platform_temperature_control snd_seq_device btintel irqbypass processor_thermal_rfim libarc4 snd_timer btbcm btmtk processor_thermal_rapl rapl cmdlinepart iwlwifi spi_nor snd
> [52159.495312]  intel_cstate intel_rapl_common mei_me intel_wmi_thunderbolt bluetooth mtd 8250_dw intel_pmc_core soundcore mei pmt_telemetry processor_thermal_wt_req cfg80211 processor_thermal_power_floor pmt_discovery pmt_class processor_thermal_mbox int3403_thermal intel_soc_dts_iosf int340x_thermal_zone surfacepro3_button intel_pmc_ssram_telemetry mac_hid int3400_thermal surface_aggregator_registry acpi_pad soc_button_array surface_hotplug surface_acpi_notify intel_vsec acpi_tad dptf_power acpi_thermal_rel sch_fq_codel kyber_iosched msr parport_pc ppdev lp parport efi_pstore ip_tables x_tables autofs4 dm_crypt raid10 raid456 async_raid6_recov async_memcpy async_pq async_xor async_tx xor raid6_pq raid1 raid0 linear system76_io(OE) system76_acpi(OE) i915 nvme drm_buddy polyval_clmulni ttm ghash_clmulni_intel i2c_algo_bit nvme_core spi_intel_pci drm_display_helper nvme_keyring intel_lpss_pci spi_intel nvme_auth intel_lpss cec idma64 rc_core video surface_aggregator wmi crc_itu_t pinctrl_icelake aesni_intel
> [52159.495406] CPU: 5 UID: 0 PID: 760 Comm: NetworkManager Tainted: G        W  OE       6.17.1-surface-2 #2 PREEMPT(voluntary) 
> [52159.495413] Tainted: [W]=WARN, [O]=OOT_MODULE, [E]=UNSIGNED_MODULE
> [52159.495415] Hardware name: Microsoft Corporation Surface Laptop 3/Surface Laptop 3, BIOS 19.101.140 04/11/2024
> [52159.495418] RIP: 0010:iwl_mvm_mac_ctxt_init+0x217/0x230 [iwlmvm]
> [52159.495461] Code: 24 48 c7 c2 10 37 18 c1 31 f6 e8 54 b6 7c ff e9 08 ff ff ff f3 48 0f bc c0 89 83 58 07 00 00 83 f8 04 0f 85 4f ff ff ff eb d3 <0f> 0b b8 f0 ff ff ff e9 6d fe ff ff e8 b8 76 cb cb 0f 1f 84 00 00
> [52159.495464] RSP: 0018:ffffcf9f42d9f1d8 EFLAGS: 00010202
> [52159.495468] RAX: 0000000000000050 RBX: ffff8e39a1eb9f08 RCX: 0000000000000000
> [52159.495471] RDX: 0000000000000000 RSI: 0000000000000000 RDI: 0000000000000000
> [52159.495473] RBP: ffffcf9f42d9f218 R08: 0000000000000000 R09: 0000000000000000
> [52159.495475] R10: 0000000000000000 R11: 0000000000000000 R12: ffff8e398739a048
> [52159.495477] R13: ffff8e39a1eb9f08 R14: ffff8e398739a078 R15: ffff8e39a1eba3b0
> [52159.495512] FS:  00007d87606454c0(0000) GS:ffff8e3d4ca60000(0000) knlGS:0000000000000000
> [52159.495515] CS:  0010 DS: 0000 ES: 0000 CR0: 0000000080050033
> [52159.495518] CR2: ffffe5074426dc20 CR3: 00000001102b3006 CR4: 0000000000772ef0
> [52159.495521] PKRU: 55555554
> [52159.495522] Call Trace:
> [52159.495525]  <TASK>
> [52159.495530]  iwl_mvm_mld_mac_add_interface+0x90/0x310 [iwlmvm]
> [52159.495572]  drv_add_interface+0x4f/0x270 [mac80211]
> [52159.495652]  ieee80211_do_open+0x582/0x7e0 [mac80211]
> [52159.495745]  ieee80211_open+0x6e/0xa0 [mac80211]
> [52159.495833]  __dev_open+0x109/0x2a0
> [52159.495841]  __dev_change_flags+0x1b1/0x220
> [52159.495847]  netif_change_flags+0x26/0x80
> [52159.495852]  do_setlink.constprop.0+0x3b1/0x12b0
> [52159.495858]  ? intel_iommu_map_pages+0x35e/0x710
> [52159.495865]  ? __nla_validate_parse+0x59/0xe90
> [52159.495871]  ? sched_balance_newidle+0x2bc/0x420
> [52159.495880]  ? security_capable+0x7e/0x1f0
> [52159.495886]  ? ns_capable+0x2d/0x70
> [52159.495891]  ? netlink_create+0x1d0/0x280
> [52159.495900]  rtnl_newlink+0x900/0xd60
> [52159.495905]  ? iommu_map+0x3e/0xa0
> [52159.495911]  ? __iommu_dma_map+0xa0/0x190
> [52159.495919]  ? security_capable+0x7e/0x1f0
> [52159.495924]  ? __pfx_rtnl_newlink+0x10/0x10
> [52159.495929]  rtnetlink_rcv_msg+0x364/0x410
> [52159.495933]  ? bdev_getblk+0x31/0x90
> [52159.495941]  ? ext4_inode_csum+0xee/0x120
> [52159.495947]  ? __pfx_rtnetlink_rcv_msg+0x10/0x10
> [52159.495951]  netlink_rcv_skb+0x58/0x110
> [52159.495957]  rtnetlink_rcv+0x15/0x30
> [52159.495960]  netlink_unicast+0x28b/0x3b0
> [52159.495965]  netlink_sendmsg+0x1f3/0x440
> [52159.495970]  ____sys_sendmsg+0x39c/0x3d0
> [52159.495975]  ___sys_sendmsg+0x87/0xe0
> [52159.495982]  ? __wake_up_sync+0x45/0x70
> [52159.495989]  ? ep_poll_callback+0x2a4/0x320
> [52159.495995]  ? __wake_up_common+0x7b/0xb0
> [52159.496003]  ? __wake_up_sync_key+0x49/0x80
> [52159.496010]  __sys_sendmsg+0x73/0xe0
> [52159.496017]  __x64_sys_sendmsg+0x1d/0x30
> [52159.496022]  x64_sys_call+0x21c5/0x2740
> [52159.496028]  do_syscall_64+0x7f/0x1080
> [52159.496035]  ? ___sys_sendmsg+0x94/0xe0
> [52159.496040]  ? ksys_write+0xd3/0xf0
> [52159.496045]  ? refill_obj_stock+0x14d/0x340
> [52159.496052]  ? __memcg_slab_free_hook+0x103/0x160
> [52159.496059]  ? __fput+0x1ae/0x2f0
> [52159.496062]  ? kmem_cache_free+0x34c/0x460
> [52159.496069]  ? __fput+0x1ae/0x2f0
> [52159.496073]  ? fput_close_sync+0x40/0xa0
> [52159.496077]  ? __x64_sys_close+0x3e/0x80
> [52159.496083]  ? x64_sys_call+0x1c34/0x2740
> [52159.496087]  ? do_syscall_64+0xb8/0x1080
> [52159.496092]  ? __x64_sys_sendmsg+0x1d/0x30
> [52159.496097]  ? x64_sys_call+0x21c5/0x2740
> [52159.496100]  ? do_syscall_64+0xb8/0x1080
> [52159.496105]  ? file_check_and_advance_wb_err+0x2b/0xd0
> [52159.496111]  ? __rseq_handle_notify_resume+0xab/0x4c0
> [52159.496117]  ? ext4_sync_file+0x1cc/0x390
> [52159.496124]  ? do_fcntl+0x74b/0x7d0
> [52159.496128]  ? restore_fpregs_from_fpstate+0x3d/0xc0
> [52159.496136]  ? __x64_sys_fcntl+0xaa/0x130
> [52159.496139]  ? __task_pid_nr_ns+0xad/0xd0
> [52159.496145]  ? __do_sys_getpid+0x1d/0x30
> [52159.496149]  ? x64_sys_call+0x8cf/0x2740
> [52159.496153]  ? do_syscall_64+0xb8/0x1080
> [52159.496158]  ? clear_bhb_loop+0x30/0x80
> [52159.496162]  ? clear_bhb_loop+0x30/0x80
> [52159.496167]  entry_SYSCALL_64_after_hwframe+0x76/0x7e
> [52159.496170] RIP: 0033:0x7d8761127a0d
> [52159.496181] Code: 28 89 54 24 1c 48 89 74 24 10 89 7c 24 08 e8 fa 8f f6 ff 8b 54 24 1c 48 8b 74 24 10 41 89 c0 8b 7c 24 08 b8 2e 00 00 00 0f 05 <48> 3d 00 f0 ff ff 77 33 44 89 c7 48 89 44 24 08 e8 3e 90 f6 ff 48
> [52159.496184] RSP: 002b:00007ffc5ef7e1e0 EFLAGS: 00000293 ORIG_RAX: 000000000000002e
> [52159.496188] RAX: ffffffffffffffda RBX: 0000000000000099 RCX: 00007d8761127a0d
> [52159.496191] RDX: 0000000000000000 RSI: 00007ffc5ef7e220 RDI: 000000000000000d
> [52159.496193] RBP: 00005d0f4dec2030 R08: 0000000000000000 R09: 0000000000000000
> [52159.496195] R10: 0000000000000000 R11: 0000000000000293 R12: 0000000000000000
> [52159.496197] R13: 00007ffc5ef7e370 R14: 00007ffc5ef7e36c R15: 0000000000000000
> [52159.496203]  </TASK>
> [52159.496204] ---[ end trace 0000000000000000 ]---
> [52159.703856] debugfs: 'netdev:wlp0s20f3' already exists in 'iwlmvm'
> [52159.703863] debugfs: 'iwlmvm' already exists in 'netdev:wlp0s20f3'
> [52159.703865] iwlwifi 0000:00:14.3: Failed to create debugfs directory under netdev:wlp0s20f3
> [52159.719729] debugfs: 'netdev:p2p-dev-wlp0s20' already exists in 'iwlmvm'
> [52162.721682] wlp0s20f3: authenticate with 88:9c:ad:04:e5:6e (local address=c8:34:8e:0b:fe:b2)
> [52162.722716] wlp0s20f3: send auth to 88:9c:ad:04:e5:6e (try 1/3)
> [52162.760174] wlp0s20f3: authenticated
> [52162.762260] wlp0s20f3: associate with 88:9c:ad:04:e5:6e (try 1/3)
> [52162.765663] wlp0s20f3: RX AssocResp from 88:9c:ad:04:e5:6e (capab=0x1111 status=0 aid=7)
> [52162.777362] wlp0s20f3: associated
> [52162.794377] wlp0s20f3: Limiting TX power to 23 (23 - 0) dBm as advertised by 88:9c:ad:04:e5:6e
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


[Surface Laptop 3 · linux-surface/linux-surface Wiki · GitHub](https://github.com/linux-surface/linux-surface/wiki/Surface-Laptop-3#iwlwifi-direct-firmware-load-for-iwlwifi-quqnj-b0-hr-b0-50ucode-failed-with-error--2)
```
git clone https://chromium.googlesource.com/chromiumos/third_party/linux-firmware chromiumos-linux-firmware
cd chromiumos-linux-firmware
sudo cp -v -R /lib/firmware /lib/firmware.old 
sudo cp -v iwlwifi-* /lib/firmware/
cd /lib/firmware
sudo ln -s iwlwifi-Qu-c0-hr-b0-50.ucode iwlwifi-Qu-b0-hr-b0-50.ucode
```

Hvit, gammel wifi-usb-stick
Ralink RT2770, rt2800usb, 'rt2870.bin'
```
[   58.273844] usb 3-2: new high-speed USB device number 3 using xhci_hcd
[   58.418016] usb 3-2: New USB device found, idVendor=148f, idProduct=2770, bcdDevice= 1.01
[   58.418021] usb 3-2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[   58.418022] usb 3-2: Product: 802.11 n WLAN
[   58.418023] usb 3-2: Manufacturer: Ralink
[   58.418024] usb 3-2: SerialNumber: 1.0
[   58.551070] usb 3-2: reset high-speed USB device number 3 using xhci_hcd
[   58.687792] ieee80211 phy1: rt2x00_set_rt: Info - RT chipset 2872, rev 0202 detected
[   58.742081] ieee80211 phy1: rt2x00_set_rf: Info - RF chipset 0003 detected
[   58.742248] ieee80211 phy1: Selected rate control algorithm 'minstrel_ht'
[   58.742872] usbcore: registered new interface driver rt2800usb
[   58.751270] rt2800usb 3-2:1.0 wlx342109091e60: renamed from wlan0
[   58.759711] ieee80211 phy1: rt2x00lib_request_firmware: Info - Loading firmware file 'rt2870.bin'
[   58.760945] ieee80211 phy1: rt2x00lib_request_firmware: Info - Firmware detected - version: 0.36
```


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