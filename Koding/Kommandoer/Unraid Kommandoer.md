`curl upload.lolbraa.no -T your_file.txt`

[Reddit - Dive into anything](https://www.reddit.com/r/unRAID/comments/f2cy93/tmp_vs_devshm/)
# Generelle
## Keyboard layout
[Option to change Boot Keyboard Language - Feature Requests - Unraid](https://forums.unraid.net/topic/46325-option-to-change-boot-keyboard-language/?do=findComment&comment=663043)
```
loadkeys no-latin1
```
``/boot/config/go``
## Shutdown/Reboot
[To cleanly Stop the array from the command line](https://docs.unraid.net/legacy/FAQ/console/#to-cleanly-stop-the-array-from-the-command-line)
```
/sbin/<command>
```
**Available commands:** ==reboot== ==poweroff== ==shutdown==
Note
> `poweroff` If you get an unclean shutdown when issuing this command you need to adjust your timeout settings, see [https://forums.unraid.net/topic/69868-dealing-with-unclean-shutdowns](https://forums.unraid.net/topic/69868-dealing-with-unclean-shutdowns)

## [Powertop](https://forums.unraid.net/topic/98070-reduce-power-consumption-with-powertop/)
```
powertop
powertop --auto-tune &>/dev/null
```

## Permissions
[Notat hentet fra Reddit](https://www.reddit.com/r/unRAID/comments/1b7ks0p/i_just_wanted_to_say_i_love_unraid/)
>Containers and owners is somewhat a mess, untill you can properly wrap your head around it.
>Docker itself runs at root `0:0`, but many containers use functions to run the actual applications as a regular user; some hardcoded and some defined by (usually) env vars. This user will own files inside the container, reflected in the linked folder on the host.
>It seems unraid has users starting at `1000:100`, though terminal runs as root `0:0`, and there is a dedicated `99:100` user to be used for containers.
>If a container is run alone, with nothing else interacting with the files, owner of the files doesn’t really matter.
>If multiple containers share directories, the UID:GID of the user run inside the containers have to be the same (again reflected on the files on the host), be that `99:100`, `1000:1000` or `107:107`.
>Many containers have PUID:PGID env vars to specify user, some can be forced by adding —user `99:100` - though depending on the internals of the container, it might not work anyways.

To see what `user:group` owns the files in a directory, simply type from the terminal
```
ls -l /mnt/user/data/media/movies`
```

```
chown -cR 99:100 <DIRECTORY/FILE>
```
[Chown Command in Linux: How to Change File Ownership](https://phoenixnap.com/kb/linux-chown-command-with-examples)

## Run diagnostics
```
diagnostics
```

## Restart nettverk
[Command to restart network? - General Support (V5 and Older) - Unraid](https://forums.unraid.net/topic/2048-command-to-restart-network/)
```
/etc/rc.d/rc.inet1  restart
```
Fungerer når den av en eller annen grunn glitcher og mister total kobling til nettverket.

## Restart PHP/nginx/Docker/VMs
[info](https://www.reddit.com/r/unRAID/comments/1753w5w/unraid_dashboard_not_accessible_however_running/)
```
nginx
/etc/rc.d/rc.nginx restart 
/etc/rc.d/rc.nginx reload 

PHP:
/etc/rc.d/rc.php-fpm restart 
/etc/rc.d/rc.php-fpm reload

Docker:
/etc/rc.d/rc.docker start|stop|restart|status

VMs:
virsh start | reboot | shutdown | destroy --graceful


SSHD
/etc/rc.d/rc.sshd restart
```

## Tail the syslog
```
tail -f /var/log/syslog
```

## Look at the parameters in the config file
```
nano /boot/syslinux.cfg-
```

## Create a backup image of your usb and store it on disk1
```
dd if=/dev/sda of=/mnt/disk1/unraid.img
```

## Check power on hours for all drives
```
for drive in $(ls -la /dev | grep -Ev 'sda|sd[a-z][0-9]' | grep sd[a-z] | awk '{print $10}'); do hours=$(smartctl --all /dev/${drive} | grep Power_On_Hours | awk '{print $10}'); echo "Power on Hours for ${drive}: ${hours}"; echo ''; done
```


# Mover
## Stopp mover
```
mover stop
```

## Filter
Bruker [[Plugin] Mover Tuning](https://forums.unraid.net/topic/70783-plugin-mover-tuning/) sin filter-funksjon. Filter er skrevet i filen:
/mnt/user/appdata/moverfilter.txt
```
/mnt/diverse/appdata/moverfilter.txt
/mnt/cache/Lolbraa\ Bilder/Immich/encoded-video/*
/mnt/cache/Lolbraa\ Bilder/Immich/thumbs/
```
[Script for å la cache være dynamisk](https://forums.unraid.net/topic/154106-guide-how-to-keep-cache-drive-full-of-media/)
[**How to ignore a SINGLE file**, **How to ignore Muliple files.**  og **How to Ignore a directory**](https://forums.unraid.net/topic/70783-plugin-mover-tuning/page/34/#comment-1185036)
Verifisere
```
find "/mnt/cache/Lolbraa\ Bilder" -depth | grep -vFf '/mnt/user/appdata/moverfilter.txt'
```

# Macros
Lagt til i /boot/config/go etter instrukser her [Console | Unraid Docs](https://docs.unraid.net/legacy/FAQ/console/#to-cleanly-stop-the-array-from-the-command-line).
Laget egne for Immich-logs og cd /mnt/user
```sh
# Docker logs for Immich
echo "alias immichlogs='cd /mnt/user/appdata/docker_compose_projects/Immich;docker compose logs -f -n 1000'">>/etc/profile
# Logs for NCGNAS/Offsite-Admin-backup ()
echo "alias backuplogs='tail /mnt/user/appdata/borgmatic-ncgoffsite-admin/logs/ncgnasoffsite-admin.log -f -n 100'">>/etc/profile
# Kjapt til cd /mnt/user
echo "alias cduser='cd /mnt/user'">>/etc/profile
```
Lage for 
- cd til .logs og .locks og appdata
- tail -f /var/log/syslog

```sh
tail /mnt/user/appdata/borgmatic-ncgoffsite-admin/logs/ncgnasoffsite-admin.log -f -n 100
cd /mnt/user/appdata/docker_compose_projects/Immich;docker compose logs -f
```

# Rclone-config
```
[gdrive]
type = drive
client_id = 4533917761-gsb7gi8ph0q9b1okjp5569c7rdndt920.apps.googleusercontent.com
client_secret = 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
scope = drive
token = {"access_token":"ya29.a0Ad52N3_9UXBLnJusMe86wGjevklM7B3TXZ7XiFbhjkSbi8ofuvjs5ZGf4-34UNnlR1gxmWijs0W15IYT3AJqh10yEABjHGvCnaCB65AiQnETLhqqYb7vdG6H9fb1-L9ie0So2Vbtuk4MOFr88gJyEV5bPc7NBtixojrIREoaCgYKAW8SARASFQHGX2MiWf-eh_XP5vDHy0wF7-ZYyA0174","token_type":"Bearer","refresh_token":"1//0ccwZQ840NKQxCgYIARAAGAwSNwF-L9Irt7Rkzv-01GaJCZ0bbcZsyi4n483Eq3qriejcgUqnWejGEPmk88UvqHBm4XauAnX9y14","expiry":"2024-04-11T17:00:00.891418471+02:00"}
team_drive = 

[telia]
type = jottacloud
configVersion = 1
client_id = desktop
tokenURL = https://sky-auth.telia.no/auth/realms/get/protocol/openid-connect/token
token = {"access_token":"eyJhbGciOiJSUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICJNa3hiU2ZCcHJOekNOOUg4b0FhMkdLNEp4S25XNXQtWkgwa05FV01wQ19zIn0.eyJqdGkiOiJiNjhkNDRlNy0yYmFiLTRkZWItODI0YS1mMTA4OTMwMjQ0ZWEiLCJleHAiOjE3MTI4MjAxNzgsIm5iZiI6MCwiaWF0IjoxNzEyODE2NTc4LCJpc3MiOiJodHRwczovL3NreS1hdXRoLnRlbGlhLm5vL2F1dGgvcmVhbG1zL2dldCIsInN1YiI6ImY6ZTM4N2ZmMWEtZGM4My00NzY1LWIwYmYtZmYwMzAxNzcwNWJkOmdldC0xMDA5NzgwMDAiLCJ0eXAiOiJCZWFyZXIiLCJhenAiOiJkZXNrdG9wIiwibm9uY2UiOiI4YjQwOWRjZi1hYzM1LTRmMmYtYTBiZC0wMDk0OWEzMjA5ZjUiLCJhdXRoX3RpbWUiOjE3MDA4NTM5MzEsInNlc3Npb25fc3RhdGUiOiI2N2M3YWQ4Mi01ODRkLTQ4OGItOTlmZC1lYzM1YmNhYzY2NzgiLCJhY3IiOiIxIiwiYWxsb3dlZC1vcmlnaW5zIjpbImh0dHBzOi8vc2t5LnRlbGlhLm5vIl0sInJlYWxtX2FjY2VzcyI6eyJyb2xlcyI6WyJvZmZsaW5lX2FjY2VzcyJdfSwic2NvcGUiOiJvcGVuaWQgb2ZmbGluZV9hY2Nlc3Mgam90dGEtZGVmYXVsdCIsImV4dF9pZCI6IjNjZGY5YzMzLWEzMzItNDc4MC1iNWMzLWYxOGZmODU4ZTE1YyIsInJlYWxtIjoiZ2V0IiwidXNlcm5hbWUiOiJnZXQtMTAwOTc4MDAwIn0.UC9VJPPqP_d0SzQYXOhUwrzls3oSSWdljs4kmtbtuDne1s1JxPpY6VinRUOEUy39wD9CEZUF-VCG0CESZNycAzyrQAI-qWx3et4IMxjbQRfZo_CMLhOJk9lvA3wemvCJILWRjLQ-EHtjjsmw5ZUgDvCMMhPZVoY2ngLkVNaYBYeXHF_20Y6n2rwkvNJMaHK_zlB2QJA31NOtl7oFt4U7hlx0_oOapD6ykyY3UhMpekYtPoRZA0IQfNqowKnhzR3QlgIjlk7UhT0JBsBH8-008_f49S3Sry5gvjBTGmkG5geam9Gf4IkCSzgnU88pkKaB7J15LfS3QfyICzoaGyFjVQ","token_type":"bearer","refresh_token":"eyJhbGciOiJIUzI1NiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICI4ZTlhYjdhNy05NTQ4LTRiY2QtOGQwNy1jMmU4OTYxYWUwNmQifQ.eyJqdGkiOiJkZjZhN2YyMC0yNzNjLTQyNDctOWExNy1jZTc1ZjkxNzA4ZjQiLCJleHAiOjAsIm5iZiI6MCwiaWF0IjoxNzEyODE2NTc4LCJpc3MiOiJodHRwczovL3NreS1hdXRoLnRlbGlhLm5vL2F1dGgvcmVhbG1zL2dldCIsImF1ZCI6Imh0dHBzOi8vc2t5LWF1dGgudGVsaWEubm8vYXV0aC9yZWFsbXMvZ2V0Iiwic3ViIjoiZjplMzg3ZmYxYS1kYzgzLTQ3NjUtYjBiZi1mZjAzMDE3NzA1YmQ6Z2V0LTEwMDk3ODAwMCIsInR5cCI6Ik9mZmxpbmUiLCJhenAiOiJkZXNrdG9wIiwibm9uY2UiOiI4YjQwOWRjZi1hYzM1LTRmMmYtYTBiZC0wMDk0OWEzMjA5ZjUiLCJhdXRoX3RpbWUiOjAsInNlc3Npb25fc3RhdGUiOiI2N2M3YWQ4Mi01ODRkLTQ4OGItOTlmZC1lYzM1YmNhYzY2NzgiLCJyZWFsbV9hY2Nlc3MiOnsicm9sZXMiOlsib2ZmbGluZV9hY2Nlc3MiXX0sInNjb3BlIjoib3BlbmlkIG9mZmxpbmVfYWNjZXNzIGpvdHRhLWRlZmF1bHQifQ.LNx0AxgeCVfaUhcLeL4M0yzm6zK4CeElaq46aWVoRBU","expiry":"2024-04-11T09:22:58.73805054+02:00"}
device = 
mountpoint = 

[BraaNAS]
type = smb
host = 192.168.1.65
user = admin
pass = gNaW5nh5IoW1Xjc1bgIU487XD-tnBgPm

[local]
type = local

[googlephotos]
type = google photos
token = {"access_token":"ya29.a0Ad52N3-L7lEV2t6iH3L6SvG8VaP7XRDcDDtUTz1p4FLrqCXNgjODhWFTt_NSc7bwRcxl8mEB97NSaME7MZh0HxbI5fzbre6zdyoS0_FVIGSsngF0zq3Mi6QvPKnl4H079-4XxAIINl2cQXDXvrWcyIF2hpXpPJg0ry9GKREaCgYKATcSARASFQHGX2Mi3V7sK_WrKhDT25kwfk3EnA0174","token_type":"Bearer","refresh_token":"1//0cBeNnHd1kAx_CgYIARAAGAwSNwF-L9IrUU40LTKVI2mNAWG5CvV2g_8wybGIsze0qV8qYdRW2g7KGHNlaqOFo4V4wkdADTCc8kQ","expiry":"2024-04-10T22:00:00.812744814+02:00"}


```


# ssh github
~/.ssh/config
```
Host github.com
IdentityFile ~/.ssh/id_git_ssh
IdentitiesOnly yes
```
Kopiert inn private nøkkelen fra 1pass


# Docker-folder-ikon
[GitHub - hernandito/unRAID-Docker-Folder-Animated-Icons---Alternate-Colors](https://github.com/hernandito/unRAID-Docker-Folder-Animated-Icons---Alternate-Colors)
Git-repo klonet til /mnt/user/system/icons.
For å få et ikon på en mappe, finn navnet til filen man ønsker på GitHuben og så bruk path:
```
/mnt/user/system/icons/unRAID-Docker-Folder-Animated-Icons---Alternate-Colors-master/Pale-Collection/pale-database.svg
```