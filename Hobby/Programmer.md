 # [Eddy Installation Error: Child Process Exited with Code 100](https://stackoverflow.com/questions/76805857/eddy-installation-error-child-process-exited-with-code-100)
```
sudo apt clean
sudo apt update
sudo dpkg --configure -a
sudo apt install -f
sudo apt full-upgrade
sudo apt autoremove --purge
```


# diverse
[KRename - KDE Applications](https://apps.kde.org/krename/)
- [Reddit - Dive into anything](https://www.reddit.com/r/pop_os/comments/1gpdsov/will_pop_os_or_anyone_for_that_matter_ever_make/?share_id=QobXnfW7qPGkKgjYbCocv&utm_content=1&utm_medium=android_app&utm_name=androidcss&utm_source=share&utm_term=2)

# Diagnostikk
Mye bra software!
[Home of Gibson Research Corporation](https://www.grc.com)
## Logwatch
[How to install and configure Logwatch - Ubuntu Server documentation](https://documentation.ubuntu.com/server/how-to/observability/install-logwatch/)

## Validering av USB drive
ValiDrive
[GRC | ValiDrive](https://www.grc.com/validrive.htm)

## Validering av HDD
- [GRC | Hard drive data recovery software](https://www.grc.com/sr/spinrite.htm) - dyrt, og flere mener det er "snake oil" og kun bruker SMART data
- [hard drive - Equivalent of badblocks on Windows or DOS - Super User](https://superuser.com/questions/338067/equivalent-of-badblocks-on-windows-or-dos)
- [Windows based preclear  - General Support - Unraid](https://forums.unraid.net/topic/48145-windows-based-preclear/?do=findComment&comment=486136): WD's Data Lifeguard;  Seagate's SeaTools;  HGST's Drive Fitness Test

# Recovery
- [GRC | Hard drive data recovery software](https://www.grc.com/sr/spinrite.htm)


---

# Firefox
Default search engine
[About SearXNG — SearXNG Documentation (2024.10.7+f1f0dfd23)](https://docs.searxng.org/user/about.html#how-do-i-set-it-as-the-default-search-engine)

# Vivaldi
[Add SearXNG with Autocompletion to Vivaldi](https://ae3.ch/searxng-vivaldi-autocomplete/)

---
# Visual Studio Code
## Innstillinger
[visual studio code - How can I export settings? - Stack Overflow](https://stackoverflow.com/questions/35368889/how-can-i-export-settings):
With the current version of Visual Studio Code as of this writing (1.22.1), [you can find your settings in](https://code.visualstudio.com/docs/getstarted/settings#_settings-file-locations):
- `~/.config/Code/User` on Linux
- `%APPDATA%\Code\User` (`C:\Users\username\AppData\Roaming\Code\User`) on Windows
- `~/Library/Application Support/Code/User/` on Mac OS X
The files are `settings.json` and `keybindings.json`. Simply copy them to the target machine.

[Your extensions are in](https://code.visualstudio.com/docs/editor/extension-marketplace#_where-are-extensions-installed):
- `~/.vscode/extensions` on Linux and Mac OS X
- `%USERPROFILE%\.vscode\extensions` (`C:\Users\username\.vscode\extensions`) on Windows (i.e., essentially the same place as on Linux and Mac OS X)


---

# Terminal
## fish
[fish shell](https://fishshell.com/)
## Oh My Posh
[Linux | Oh My Posh](https://ohmyposh.dev/docs/installation/linux)
## nano
[Cheatsheet for GNU nano](https://www.nano-editor.org/dist/latest/cheatsheet.html)

> [!PICTURE]- shortcuts
> ![[Programmer-20240911085656947.jpg|500]]

## Tabby
### Tips
Lim inn: ``ctrl + shift + v``
Se [[Generelle Kommandoer#Tmux]]
Ikoner [Find Icons with the Perfect Look & Feel | Font Awesome](https://fontawesome.com/icons)
Sette default [How to setup Tabby as default terminal in Linux? · Eugeny/tabby · Discussion #6266 · GitHub](https://github.com/Eugeny/tabby/discussions/6266)

### Sync
- [GitHub - niceit/tabby-cloud-sync-settings: Tabby plugin for syncing settings across device platforms. https://github.com/Eugeny/tabby](https://github.com/niceit/tabby-cloud-sync-settings) plugin 
	- [Gist](https://gist.github.com/lolbraa/57b8f80c9dfb72e3158cc920cc57a8ca)(GitHub) id og token i 1pass
	- Fungerer også med en annen sync-plugin i samme gist???
	- ~~Webdav~~
		- ~~Se [[NextCloud Kommandoer#Webdav]] for oppsett~~
		- ~~Innstillinger: Se [[Programmer-20240904203311558.jpg]]~~
```
https://cloud.lolandbraa.no/remote.php
kristoffer
app-passord i 1pass: https://start.1password.com/open/i?a=HJGS6TLOPVBJPGBAN5CYJKE2B4&v=gpaffwudef2dfdrqfmuj2u5ulm&i=77jneg47n3225xsjv3u2doapou&h=my.1password.eu
ingen port
/dav/files/kristoffer/07 Verktøy/00 Terminal/TabbyCloudSyncWebdav
```

### Tabby Web
- Guthub OAuth
	- Client ID: ed192624173ca2cea813
	- Client secret: 1pass


### 1password agent på Linux
Problem [1Password integration · Eugeny/tabby · Discussion #5939 · GitHub](https://github.com/Eugeny/tabby/discussions/5939)
#### Løsning 1
> Run the following snippet to create a login script in `/etc/profile.d/`:  
> `echo "export SSH_AUTH_SOCK=~/.1password/agent.sock" | sudo tee /etc/profile.d/1password-ssh-auth-sock.sh`  
> If your system launches the GNOME keyring SSH agent automatically, you can disable that by running the following command:
```
mkdir -p ~/.config/autostart \
  && cp /etc/xdg/autostart/gnome-keyring-ssh.desktop ~/.config/autostart/gnome-keyring-ssh.desktop \
  && echo "Hidden=true" >> ~/.config/autostart/gnome-keyring-ssh.desktop
```
> If you choose not to do this, the GNOME setting `(/run/user/1000/keyring/ssh)` may take precedence over the 1Password setting, depending on your operating system.
#### Løsning 2
1. Følg instruksene her [SSH client compatibility | 1Password Developer](https://developer.1password.com/docs/ssh/agent/compatibility/#ssh-auth-sock)
```sh
echo "export SSH_AUTH_SOCK=~/.1password/agent.sock" | sudo tee /etc/profile.d/1password-ssh-auth-sock.sh
```
2. Eventuelt må du gjøre dette (vet ikke helt om det var nødvendig)
```sh
SSH_AUTH_SOCK=~/.1password/agent.sock ssh-add -l
```
3. Restart Tabby, evt. også maskina


### Serial
[Error: Permission denied, cannot open /dev/ttyUSB0 · Issue #8511 · Eugeny/tabby · GitHub](https://github.com/Eugeny/tabby/issues/8511)
```sh
sudo usermod -a -G tty $USER
sudo usermod -a -G dialout $USER
```

### Sudo-error
[sudo not working on Linux · Issue #960 · Eugeny/tabby · GitHub](https://github.com/Eugeny/tabby/issues/960#issuecomment-998700199)
When exiting Tabby the below processes still run in the background.
```shell
$ ps -eaf|grep tabby
user    7570    3731  0 Dec20 ?        00:00:00 /opt/Tabby/tabby --type=zygote --no-zygote-sandbox --no-sandbox
user    7571    3731  0 Dec20 ?        00:00:00 /opt/Tabby/tabby --type=zygote --no-sandbox
```
After killing these I'm able to use `sudo`
```shell
pkill tabby
```

# 1password
## Legge til SSH-nøkkel
Har laget ny nøkkel for alle lolbraa-enheter, "Lolbraa Systemnokkel".
```sh
echo "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIFAt/YS69Bf9tMLsI6P5DL9fO+M50o4Wva/gxhaf+KDa" >> ~/.ssh/authorized_keys
```
[Lolbraa Systemnokkel](https://start.1password.com/open/i?a=HJGS6TLOPVBJPGBAN5CYJKE2B4&v=gpaffwudef2dfdrqfmuj2u5ulm&i=d2r3gkmumjlv7vk3w2jqflj63y&h=my.1password.eu)
## Authentication-error; for mange forsøk
[NorwayCraftGroupAS/dokumentasjon/1password.md#agenttoml](https://github.com/NorwayCraftGroupAS/dokumentasjon/blob/main/1password.md#agenttoml)
For mange nøkler i 1pass-vault som forsøkes. Endre agent.toml (høyreklikk en SSH-nøkkel i 1pass) og legg inn feks:

```toml
Lolbraa Enheter
[[ssh-keys]]
item = "Lolbraa Systemnokkel"
vault = "Private"

Braa Enheter
[[ssh-keys]]
item = "Braa Systemnokkel"
vault = "Felles: Braa"

NCGNAS/SSH U: root
[[ssh-keys]]
item = "NCGNAS/SSH U: root"
vault = "Felles: NCG-sensitivt"

NCG/SSH Systemnokkel
[[ssh-keys]]
item = "NCG/SSH Systemnokkel"
vault = "Felles: NCG-sensitivt"

Plesk/SSH U: root
[[ssh-keys]]
item = "Plesk/SSH U: root"
vault = "Felles: NCG-sensitivt"

TBGx/SSH
[[ssh-keys]]
item = "TBGx/SSH"
vault = "Felles: NCG-sensitivt"

Vaults
[[ssh-keys]]
vault = "Felles: NCG-sensitivt"
[[ssh-keys]]
vault = "Private"
```
[Docs for problemstilling](https://developer.1password.com/docs/ssh/agent/advanced/#create-an-ssh-agent-config-file) og [docs for agent.toml](https://developer.1password.com/docs/ssh/agent/config/).
> De elementene som står først i agent.toml er også de som først prøves, ref: `ssh-add -l`.
> 
> %LOCALAPPDATA%/1Password/config/ssh/agent.toml



# Remote desktop: [Rustdesk](https://rustdesk.com/)
Funnet i [Best Remote Desktop Software?](https://www.reddit.com/r/sysadmin/comments/1168sye/best_remote_desktop_software/).
Open source, selfhosted og mange muligheter gratis.

## Relay
Kjører en relay og ID-server (?) på LolbraaNAS ([RustDeskServer-AiO](https://hub.docker.com/r/ich777/rustdesk-server-aio)).
[Client Configuration :: Documentation for RustDesk](https://rustdesk.com/docs/en/self-host/client-configuration/#2-manual-config)

IDer og passorder til kjente klienter ligger i 1pass.

### Export Server Settings:
for enkel importering i settings
```
=0nI9QjVwYkNrp1V1RFWJ1GVyp0bjJlejlTd3kXVzlGcIBXTMhjQNVlYxJEVtxkI6ISeltmIsIiI6ISawFmIsIiI6ISehxWZyJCLi8mbuEWYyJGZuFGbvxmLuBndiojI0N3boJye
```

### Manuell innstilonger
Key: 
```
LmTBqbUMB8LMpHpisUy7u9czRcoJrTmIXTuWZk6F0V4=
```
ID-server: 
```
vpn.lolandbraa.no
```



# WinSCP
Konfigurasjonsfil på tvers av enheter i ``...\Nextcloud\07 Verktøy\WinSCP\WinSCP.ini``.
Settes i Innstillinger > Lagring > Egendefinert INI-fil.


# Cloudflare
## DNS-challenge for Let's Encrypt
Bruker Nginx Proxy Manager og lager \*.lolandbraa.no-sertifikat.
Lager en API-token på https://dash.cloudflare.com/. ([ref](https://www.nodinrogers.com/post/2022-03-10-certbot-cloudflare-docker/))
Lagret i 1pass.
## Pages
https://www.lolandbraa.no/
https://lolandbraa-no.pages.dev/
https://github.com/lolbraa/lolandbraa.no

# Troubleshooting
Se [[Linux Kommandoer#Førstehjelp]]

# Tips og triks
* [awesome-selfhosted/awesome-selfhosted: A list of Free Software network services and web applications which can be hosted on your own servers](https://github.com/awesome-selfhosted/awesome-selfhosted)
* [hashicorp/vault - Docker Image | Docker Hub](https://hub.docker.com/r/hashicorp/vault)
* [qarmin/czkawka: Multi functional app to find duplicates, empty folders, similar images etc.](https://github.com/qarmin/czkawka)
- [Unmanic/unmanic: Unmanic - Library Optimiser](https://github.com/Unmanic/unmanic)
- [Serve and Funnel | Tailscale Explained - YouTube](https://www.youtube.com/watch?v=MpxmfpCl20c&feature=youtu.be)
- [caronc/apprise: Apprise - Push Notifications that work with just about every platform!](https://github.com/caronc/apprise?tab=readme-ov-file#email-notifications)
- [YoRyan/mailrise: An SMTP gateway for Apprise notifications.](https://github.com/YoRyan/mailrise)
- [vogler/free-games-claimer: Automatically claims free games on the Epic Games Store, Amazon Prime Gaming and GOG.](https://github.com/vogler/free-games-claimer?tab=readme-ov-file)



# Pop-OS
[Apps for GNOME – Discover the best Apps for GNOME](https://apps.gnome.org/en/)

## Sikkerhet
[GitHub - iAnonymous3000/popos-hardening-guide: A step-by-step guide to securing Pop!\_OS Linux desktops. Covering system updates, user security, network hardening, disk encryption, and more, this guide is tailored for users looking to enhance their Pop!\_OS security posture.](https://github.com/iAnonymous3000/popos-hardening-guide?tab=readme-ov-file)

## Files: Kopiere path fra Nautilus(?)
ctrl+L and ctrl+c.
[Reddit - Dive into anything](https://www.reddit.com/r/gnome/comments/uk27xt/how_to_copy_directory_path_in_files/)
## Files: SCP-tilgang til LolbraaNAS
```
ssh://root@lolbraanas
```
## Lyd til flere utganger
[sound - How to achieve (automated) simultaneous outputs with Pipewire? - Ask Ubuntu](https://askubuntu.com/questions/1379376/how-to-achieve-automated-simultaneous-outputs-with-pipewire)
`$XDG_CONFIG_HOME/pipewire/pipewire.conf.d/add-combined-sink.conf`
```python
context.exec = [
    { path = "pactl" args = "load-module module-combine-sink" }
]
```

## Fonts
[How to Install Google and Microsoft Fonts on Linux](https://www.howtogeek.com/769894/how-to-install-google-and-microsoft-fonts-on-linux/)
```sh
sudo apt install ttf-mscorefonts-installer
fc-match TimesNewRoman
```

## Stoppe Flatpacks fra å oppdatere (?)
[software updates - How do I pin a Flatpak application to a specific version to prevent it from being updated? - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/673741/how-do-i-pin-a-flatpak-application-to-a-specific-version-to-prevent-it-from-bein)

## Stuck GUI
[Black Screen or Login Issues (Pop!\_OS 22.04 LTS) - System76 Support](https://support.system76.com/articles/login-loop-pop/#switch-to-a-terminal)
Go to commandline: `ctrl + alt + F3,F4 eller F5.
Note that you can always return to the graphical login screen by pressing Ctrl+Alt+F1, or by typing `sudo systemctl restart gdm`.

## AppImages
[GitHub - TheAssassin/AppImageLauncher: Helper application for Linux distributions serving as a kind of "entry point" for running and integrating AppImages](https://github.com/TheAssassin/AppImageLauncher)

## Sekunder
https://askubuntu.com/questions/39412/how-to-show-seconds-on-the-clock-in-gnome-3
```
gsettings set org.gnome.desktop.interface clock-show-seconds true
```

## Random crashes, gaming?
```log
Aug  6 17:01:36 krisstasjonerpop /usr/libexec/gdm-x-session[1070]: (WW) AMDGPU(0): flip queue failed: Invalid argument
Aug  6 17:01:36 krisstasjonerpop /usr/libexec/gdm-x-session[1070]: (WW) AMDGPU(0): Page flip failed: Invalid argument
Aug  6 17:01:36 krisstasjonerpop /usr/libexec/gdm-x-session[1070]: (EE) AMDGPU(0): present flip failed
```
- https://www.reddit.com/r/AMDHelp/comments/17yn72h/page_flip_fails_error22game_crash/
```
Section "OutputClass"
	Identifier "AMDgpu"
	MatchDriver "amdgpu"
	Driver "amdgpu"
	Option "EnablePageFlip" "off"
	Option "TearFree" "false"
EndSection
```
- Skru ned refresh rate

## Screenshots, flameshot
Keybinding [Key Bindings \| Flameshot](https://flameshot.org/docs/guide/key-bindings/#on-ubuntu-and-other-gnome-based-distros)
Tips: Test først i CLI i tilfelle errors
```
flameshot gui --clipboard --path /home/kristoffer/Pictures/
```


## Backup 
[Guide to Backup and Restore Linux Systems with Timeshift](https://itsfoss.com/backup-restore-linux-timeshift/)