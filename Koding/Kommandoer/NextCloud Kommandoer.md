[Using the occ command — Nextcloud latest Administration Manual latest documentation](https://docs.nextcloud.com/server/stable/admin_manual/configuration_server/occ_command.html)

# OCC
[GitHub - nextcloud/all-in-one: How to run `occ` commands?](https://github.com/nextcloud/all-in-one?tab=readme-ov-file#how-to-run-occ-commands)
```
sudo docker exec --user www-data -it nextcloud-aio-nextcloud php occ files:scan --all
```
Kommandoer
```
files:scan --all
```


# Webdav
URL: `https://cloud.lolandbraa.no/remote.php/dav/files/kristoffer/<mappe med space>`
> Sjekk ut "innstillinger" i Files nederst til venstre og Webdav.

Brukernavn og app-passord. App-passord fra profil-innstillinger.


# Client på linux

```sh
sudo add-apt-repository ppa:nextcloud-devs/client
sudo apt update
# For integrasjon med nemo-file explorer
sudo apt install nemo-nextcloud
```