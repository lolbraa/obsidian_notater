# Informasjon
## Informasjon om ulike kabler
[Crossover or "Null Modem" vs. Straight Through Serial Cable - Decisive Tactics, Inc.](https://www.decisivetactics.com/support/view?article=crossover-or-null-modem-vs-straight-through-serial-cable)
![[Serial-20240901185433208.jpg|749]]

## Pinout
[DB-9 Connector Pinout - Decisive Tactics, Inc.](https://www.decisivetactics.com/support/view?article=db-9-connector-pinout) 
![[Serial-20240901185511749.jpg|399]][RJ-45 Console Connector Pinout - Decisive Tactics, Inc.](https://www.decisivetactics.com/support/view?article=rj45-connector-pinout)
![[Serial-20240901185734952.jpg|482]]

## Overgang RJ45 til Serial 
https://wiki.mikrotik.com/wiki/File:Rj45-pinout.gif.png
![[Serial-20240901185747622.jpg|394]]


## Terminal-programmer
### GNU Screen
https://wiki.archlinux.org/title/GNU_Screen

---
# Enheter
For bruk i Tabby, se [[Programmer#Serial]]
## LolbraaSense
- Null-modem cable
- apu boards *115200,8n1.*

[PC Engines GmbH - FAQ, HowTo, etc. ...](http://pcengines.ch/howto.php#serialconsole)
- The loop-back test: put a paper clip in the female DB9 connector which would go on the alix/apu board at pins 2 and 3, then you should receive typed characters in your terminal emulation program. This tests the terminal emulation program, the USB-RS232 and the serial cable and this test MUST work before blaming any board attached to it. But this test does not prove whether or not a null-modem cable is used.
- The most common mistake people make is not using a null-modem cable: If you have a multimeter, check that the pins 2 and 3 are crossed. Do NOT use gender changers!
- The default baud rate for alix boards is 38400,8n1 and for apu boards 115200,8n1.
- The recommended terminal emulation program for any platform is [PuTTY](http://www.chiark.greenend.org.uk/%7Esgtatham/putty/download.html)
- Pressing the button S1 while powering up, temporarily enables a previously in the BIOS disabled serial console.
- To test if an apu board boots up, even if there is no serial console, boot it with TinyCore and a beep should be heard after about 30s-40s.

  
The output of the BIOS redirected to the serial port can be disabled, this can be useful when the port is needed for a controlling device.  
  
**"May the Null modem cable be with you!"**

## LolbraaNAS (manual)
![[Serial-20240901185336123.jpg|479]]

## LolbraaKVM
Port 6, se [[LolbraaKVM#Oversikt]]
	**Serial console port** (default: /dev/ttyAMA0, RS232 input, outputs +6V/-6V, for the Raspberry Pi or server console access, use the [Cisco/Mikrotik-style](https://wiki.mikrotik.com/wiki/File:Rj45-pinout.gif.png) cable).

- En guide: [Adding USB Serial to pikvm for remote server access](https://www.reddit.com/r/pikvm/comments/papgzj/adding_usb_serial_to_pikvm_for_remote_server/)

### Serial til LolbraaSense
#### Oppsett
0. [FAQ & Troubleshooting - PiKVM Handbook](https://docs.pikvm.org/faq/#common-questions)
		How can I use the serial console to gain access to other devices?
		You need to stop the service which listens on the `/dev/ttyAMA0`:
```
rw 
systemctl stop serial-getty@ttyAMA0.service
```
		If you want this change permanent (not starting again after reboot), you can disable this service, ('enable' to reverse this decision):
```
systemctl disable serial-getty@ttyAMA0.service
```
	- Only USB OR the RJ-45 serial connector will work, you can't use them together!
	- If you disable the service permanently, you can't recover your device via serial console if you need this.
	- There are some reports, that you need to remove `ttyAMA0` from /boot/cmdline.txt, but this is not needed on new installations.
1. [access_the_serial_port_with_the_v3_hat](https://www.reddit.com/r/pikvm/comments/rt5l5l/access_the_serial_port_with_the_v3_hat/)
```
stty < /dev/ttyAMA0
```
	- "Active client", må bruke null modem cable.
	- Bruker blå, flat RJ45-DB9-kabel
1. [Serial-over-USB - PiKVM Handbook](https://docs.pikvm.org/usb_serial/)
	1. Gjort steg 1 og rebootet
2. [ubuntu - Cannot make directory '/var/run/screen': Permission denied - Super User](https://superuser.com/questions/1195962/cannot-make-directory-var-run-screen-permission-denied)
	1. Fikk error, så gjorde som i linken over
	So to work around it, you can create a directory, such as `~/.screen`:
```
mkdir ~/.screen && chmod 700 ~/.screen
```
	and export the `SCREENDIR` to point to that directory:
```
export SCREENDIR=$HOME/.screen
```
#### Connect
*OBS, pga. noe jeg har gjort feil (?) må man stoppe en annen service som bruker serial-interfacet på KVM til noe USB-greier. Får det ikke til å ikke starte på boot*
```sh
systemctl stop serial-getty@ttyAMA0.service
minicom lolbraasense
```

eller
```sh
screen /dev/ttyAMA0 115200
```