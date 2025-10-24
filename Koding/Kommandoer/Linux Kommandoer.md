`curl upload.lolbraa.no -T your_file.txt`

# Førstehjelp
## Generelle kommandoer
[shortcut keys - What is the equivalent of 'Control-Alt-Delete'? - Ask Ubuntu](https://askubuntu.com/questions/95192/what-is-the-equivalent-of-control-alt-delete)
- ctrl+alt+backspace combination (disabled on default on 11.10) that can restart the GUI.
- ctrl+alt+F2 to F6, that will display a console from which you could login and then eventually kill the stucked application. Once you killed it you can return to the GUI by pressing alt-f7. Killing an application by name can be done by using this command:
```
sudo killall <name-of-the-application>
```
- If this doesn't work, use the `-9` flag to kill it with überforce.
```
sudo killall -9 <name-of-the-application>
```
- IN CASE OF EMERGENCY : use the [Magic SysReq Key](http://en.wikipedia.org/wiki/Magic_SysRq_key) to directly "speak" to the kernel.
- for hjelp på POP se [[programmer#Stuck GUI]]
## REISUB - low level key
Forsøk først CTRL ALT DELETE.
Kan også forsøke kun RE.

Holding down Alt and SysRq (which is the Print Screen key) while slowly typing REISUB will get you safely restarted (1 sek mellom hver?). 
REISUO will do a shutdown rather than a restart.
- R: Switch the keyboard from raw mode to XLATE mode
- E: Send the SIGTERM signal to all processes except init
- I: Send the SIGKILL signal to all processes except init
- S: Sync all mounted filesystems
- U: Remount all mounted filesystems in read-only mode
- B: Immediately reboot the system, without unmounting partitions or syn
[REISUB - the gentle Linux restart | Andrew Kember](https://blog.kember.net/posts/2008-04-reisub-the-gentle-linux-restart/)
[\[HowTo\] reboot / turn off your frozen computer: REISUB/REISUO - Tutorials - Manjaro Linux Forum](https://forum.manjaro.org/t/howto-reboot-turn-off-your-frozen-computer-reisub-reisuo/3855)

## Andre tips
[SystemRescue - System Rescue Homepage](https://www.system-rescue.org/) 

## US Keyboard
[British and American keyboards - Wikipedia](https://en.wikipedia.org/wiki/British_and_American_keyboards#/media/File:KB_United_States-NoAltGr.svg)
![[Linux Kommandoer-20240827093622214.jpg]]



# Mange kule kommandoer
[weywot/guides/commands.md at main · spxak1/weywot · GitHub](https://github.com/spxak1/weywot/blob/main/guides/commands.md)
[[Ubuntu.Server.CLI.pro.tips.19.04.22.pdf|Ubuntu Server Tips Cheatsheet]]
[Sjekke innloggede brukere/aktive SSH-økter](https://www.golinuxcloud.com/list-check-active-ssh-connections-linux/)
[Mange (gode?) Linux-artikler](https://www.baeldung.com/linux/)
1. redo last command but as root
```
sudo !!
```
2. open an editor to run a command
```
ctrl+x+e
```


# Oppdatere
```
sudo apt update && sudo apt upgrade
```


# Resource monitoring
## Generelt
htop
[btop](https://github.com/aristocratos/btop)
top
## Nettverk
[iftop](https://www.geeksforgeeks.org/iftop-command-in-linux-with-examples/)
```sh
iftop -i eth0
```
darkstat
## Disk
[iotop](https://github.com/Tomas-M/iotop)
## Power
powertop
```sh
powertop auto-tune ???
```
## Klokkehastighet
```sh
watch grep \"cpu MHz\" /proc/cpuinfo
```



# VIM
https://www.freecodecamp.org/news/vim-beginners-guide/
quit
```
:q
```



# Permissions
Tutorial: [Learning permissions | Linux Journey](https://linuxjourney.com/lesson/file-permissions)
Sjekke permissions
```
ls -l
```
Endre permissions
```
+ eXecutive rights for User on file hello.sh
chmod u+x ./hello.sh
```
SSH-nøkler (["permissions are too open"](https://stackoverflow.com/questions/9270734/ssh-permissions-are-too-open))
```
chmod 600 ~/.ssh/id_rsa
```

https://192.168.0.10:1443/Tools/NewPerms
Hvordan New Permissions gjør det
```
Processing: /mnt/user/public
... chmod -R u-x,go-rwx,go+u,ugo+X /mnt/user/public
... chown -R nobody:users /mnt/user/public
... sync
```



# Filsystem
[How to understand the (Ubuntu) filesystem](https://askubuntu.com/questions/138547/how-to-understand-the-ubuntu-file-system-layout)https://askubuntu.com/questions/138547/how-to-understand-the-ubuntu-file-system-layout
![[hN4lt.jpg]]
[Ulike FS](https://www.baeldung.com/linux/filesystems)
## Størrelse på directories
[rclone ncdu](https://rclone.org/commands/rclone_ncdu/)
[Ncdu](https://dev.yorhel.nl/ncdu/man)

### du
[du command in Linux](https://www.geeksforgeeks.org/du-command-linux-examples/)
[eksempel](https://serverfault.com/questions/136373/what-is-a-good-tool-to-scan-a-ftp-directory-and-show-disk-usage-visually-ala-kdi)
[du and the options you should be using](https://www.redhat.com/sysadmin/du-command-options)
[du simple stackexchange](https://unix.stackexchange.com/questions/185764/how-do-i-get-the-size-of-a-directory-on-the-command-line)
```sh
du -kc --human-readable * | sort -n
du --human-readable --all --total  *
du --human-readable --all --total  * | sort -h | tee filetree.txt
du --human-readable --all --total --max-depth=4  . | sort -h | tee filetree.txt # Finner alle filer og directories til en dybde på 4 mapper. Gir ut størrelsen på hver, sortert på størrelsen og lagret i en fil. 
du -sh file_path
du -sch
```

### find
Run the following command to find all files with the size larger than 20 MB and modified for the last 24 hours:
```
find / -mtime 0 -type f -size +20M -exec du -h {} + 2>/dev/null | sort -r -h
```

To find all files larger than 200 MB:
```
find / -type f -size +200M -exec du -h {} + 2>/dev/null | sort -r -h
```
[How to find directories/files that take up the most disk space on a Plesk for Linux server – Plesk](https://support.plesk.com/hc/en-us/articles/12377119104663--How-to-find-directories-files-that-take-up-the-most-disk-space-on-a-Plesk-for-Linux-server)

### Disk Free
[5 Linux commands to check free disk space | Opensource.com](https://opensource.com/article/18/7/how-check-free-disk-space-linux)
```
df -h
```

## Fjerne filer
To remove non-empty directories and all the files within them recursively, use the `-r` (recursive) option:

```
rm -r dirname
```
[Rm Command in Linux | Linuxize](https://linuxize.com/post/rm-command-in-linux/)

## Midnight commander
[Midnight Commander keyboard shortcuts ‒ DefKey](https://defkey.com/gnu-midnight-commander-shortcuts#)
i tmux, ctrl + t for å selecte

## Søke med find
[Find Command in Linux (Find Files and Directories) | Linuxize](https://linuxize.com/post/how-to-find-files-in-linux-using-the-command-line/)
```
find /home/linuxize -type f -name document.pdf
```


## Kopiere filer
Lage rsync-kommandoer [Rsync Command Generator by Snipline](https://www.rsyncinator.app/web)

Forklaring av forandring-logg [backup - What does f+++++++++ mean in rsync logs? - Stack Overflow](https://stackoverflow.com/questions/4493525/what-does-f-mean-in-rsync-logs)
### Overføre filer fra lokal disk til LolbraaNAS
OBS: Trailing slash bestemmer om selve mappen eller kun filene inni skal sendes.
Satt sammen her [Rsync Command Generator by Snipline](https://www.rsyncinator.app/web)
```sh
rsync --archive --compress --progress --partial --verbose --human-readable "/home/kriss/Pictures/Digikam/2025.01.13 Photoshoot Lillebror" lolbraanas:"/mnt/user/Lolbraa Bilder/Lolbraa fotogenitet"
```
```sh
rsync -avhP "/media/kriss/ekstrassd/Digikam/2025.01 Lillebror blir født/" lolbraanas:"/mnt/user/Lolbraa Bilder/Lolbraa fotogenitet/2
025.01 Lillebror blir født"
```


## Mount SMB-share
[# Mount an SMB Share in Linux](https://www.linode.com/docs/guides/linux-mount-smb-share/)
Manuell mount
```sh
sudo mount -t cifs //192.168.0.10/Lolbraa\ Bilder /mnt/lolbraanas_bilder -o credentials=/root/.servercred
```
Credentials
```/root/.servercred
username=lolandbraa
password=pass
```
~~Automatisk fstab~~
```fstab
# custom
//192.168.0.10/Lolbraa\ Bilder /mnt/lolbraanas_bilder cifs sec=ntlmv2,credentials=/root/.servercred,iocharset=utf8,file_mode=0777,dir_mode=0777 0
```
Sjekk manuell mount
```
mount -t cifs
```
Unmounte manuell mount
```
umount -t cifs /mnt/lolbraanas
```


# Shell operators

Overview

|   |   |
|---|---|
|Symbol / Operator|Description|
|&|This operator allows you to run commands in the background of your terminal.|
|&&|This operator allows you to combine multiple commands together in one line of your terminal.|
|>|This operator is a redirector - meaning that we can take the output from a command (such as using cat to output a file) and direct it elsewhere.|
|>>|This operator does the same function of the `>` operator but appends the output rather than replacing (meaning nothing is overwritten).|

Let's cover these in a bit more detail.

## Pipes
### Telle linjer
Pipe the result to [`wc`](http://en.wikipedia.org/wiki/Wc_%28Unix%29) using the `-l` (_line count_) switch:
```sh
wc -l
```
[Ref](https://stackoverflow.com/questions/12457457/count-number-of-lines-in-terminal-output)
### Sortere/filtrere output
[sort](https://linuxhandbook.com/sort-command/)
[grep](https://linuxize.com/post/how-to-use-grep-command-to-search-files-in-linux/) (Global Regular Expression Print) 
```
docker compose logs -n 10000 -f | grep -A 3 error
```
- Flagg ``-A <antall linjer>`` for å se kontekst etter. 
- Flagg ``-B <antall linjer>`` for å se kontekst før. 
### Skrive til fil
[Skrive kommando output til fil](https://askubuntu.com/questions/420981/how-do-i-save-terminal-output-to-a-file)
```sh
> redirects stdout.
2> redirects stderr.
&> redirects both.
you can do: cmd > outfile 2>&1
```



# Bash-terminal
## Søke gjennom bash history
[unix - How can I search the bash history and rerun a command? - Super User](https://superuser.com/questions/7414/how-can-i-search-the-bash-history-and-rerun-a-command)
Type Ctrl R at the command line and start typing the previous command. Once a result appears keep hitting Ctrl R to see other matches. When the command you want appears, simply press Enter
## Flere kommandoer på en gang og FOR-loops
[9 Examples of for Loops in Linux Bash Scripts](https://www.howtogeek.com/815778/bash-for-loops-examples/)
```sh
for i in 1 2 3 4 5; do echo $i; done
# kommando brukt for å kun finne checksum av noen filer
for i in 4 5 6 7 8 10 11 12; do sha256sum *$i.zip; done
```

[Run Multiple Linux Commands at Once \[3 Ways\]](https://itsfoss.com/run-multiple-commands-linux/)

| Operator | Example                | Explanation                                      |
| -------- | ---------------------- | ------------------------------------------------ |
| ;        | Command 1 ; Command 2  | Run command 1 first and then command 2           |
| &&       | Command 1 && Command 2 | Run command 2 only if command 1 ends sucessfully |
| \|       | Command 1 \| Command 2 | Run command 2 only if command 1 fails            |



# Arkivering (zip, gz, osv.)
https://linuxize.com/post/how-to-zip-files-and-directories-in-linux/

## [gzip](https://linuxize.com/post/gzip-command-in-linux/)
Keep the original file
```sh
gzip -k filename
gzip -c filename > filename.gz
```
>Another option to keep the original file is to use the `-c` option, which tells `gzip` to write on standard output and redirect the output to a file:

## Verifisering av
### .zip
[software rec - How can I test all zip files in a folder to verify if they are corrupted or not? - Super User](https://superuser.com/questions/526275/how-can-i-test-all-zip-files-in-a-folder-to-verify-if-they-are-corrupted-or-not)
```sh
unzip -tq '*.[Zz][Ii][Pp]'
```
### .rar
[macos - How do I find out which RAR file is corrupt? - Super User](https://superuser.com/questions/318032/how-do-i-find-out-which-rar-file-is-corrupt)
```sh
unrar t file.rar
```
nstalleres med nerdtools på Unraid
### .7z
[archiving - Testing archive with 7-zip - Super User](https://superuser.com/questions/193290/testing-archive-with-7-zip)
```sh
7z t <archive-name>
```
Installeres med nerdtools på Unraid, [GitHub - p7zip-project/p7zip: A new p7zip fork with additional codecs and improvements (forked from https://sourceforge.net/projects/sevenzip/ AND https://sourceforge.net/projects/p7zip/).](https://github.com/p7zip-project/p7zip)
### .tar.


# Kontinuerlig lese siste linjer av en log
```sh
tail -f /location/of/thefile | grep -i -E "foo|bar"
```
[Kilde](https://unix.stackexchange.com/questions/10834/reading-from-a-continuously-changing-logfile) - denne leser kun hvis output er foo eller bar.
https://www.howtogeek.com/481766/how-to-use-the-tail-command-on-linux/



# AFK-verktøy
Ignorere inputs til en kommando
[Eksempler](https://phoenixnap.com/kb/linux-nohup)
```
nohup [command] [argument] &
```

## Tmux
[Getting started with Tmux](https://linuxize.com/post/getting-started-with-tmux/)
[Tmux CheatSheet](https://tmuxcheatsheet.com/)
```
tmux new -s session_name
```
> You can detach from the Tmux session and return to your normal shell by typing:
> `Ctrl+b` `d`

```
tmux ls

tmux attach-session -t session_name/-number
```
> Kill windows (you are curently in) with `ctrl+b` `&`

[Scrolle](https://superuser.com/questions/209437/how-do-i-scroll-in-tmux)

```
Ctrl-b then [ then you can use your normal navigation keys to scroll around (eg. Up Arrow or PgDn). Press q to quit scroll mode.

Function                     vi              emacs
--------                     --              -----
Half page down               C-d             M-Down
Half page up                 C-u             M-Up
Next page                    C-f             Page down
Previous page                C-b             Page up
Scroll down                  C-Down or C-e   C-Down
Scroll up                    C-Up or C-y     C-Up
Search again                 n               n
Search again in reverse      N               N
Search backward              ?               C-r
Search forward               /               C-s
```



# Nettverk

[5 Linux network troubleshooting commands | Enable Sysadmin](https://www.redhat.com/sysadmin/five-network-commands)
[A beginner's guide to network troubleshooting in Linux | Enable Sysadmin](https://www.redhat.com/sysadmin/beginners-guide-network-troubleshooting-linux)
[Sette en IP-addresse](https://askubuntu.com/questions/758441/ifconfig-does-not-show-my-ip)
[Sjekke om man har en link](https://serverfault.com/questions/59862/cant-get-an-ip-address)

## SSH tunneling
[Using SSH Tunneling as a VPN Alternative \| Severalnines](https://severalnines.com/blog/using-ssh-tunneling-vpn-alternative/)
So, if you run the following command in your local machine:
```
$ ssh -L 8888:192.168.100.120:3306 remote@35.166.37.12 -p 20022 -N
```
This will open the port 8888 in your local machine, which will access the remote database node, port 3306, via the SSH Server, port 20022, using the “remote” user.
So, to make it more clear, after running this command, you can access the remote database node, running this in your local machine:

```SH
ssh -L 8888:192.168.1.11:80 ncgadmin@syspi
```

# Time-kommando
[Which Checksum Tool on Linux is Faster? - SysTutorials](https://www.systutorials.com/which-checksum-tool-on-linux-is-faster/)
```
$ time sha1sum wiki.txt 
251dcb5c08c6a2fabd258f2c8a9b95e15c0cc098  wiki.txt

real    1m21.143s
user    0m21.647s
sys 0m4.668s
```



![[Linux Kommandoer-2025.04.02 13.16.57.png|550]]