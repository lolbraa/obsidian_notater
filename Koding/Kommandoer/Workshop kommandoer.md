# Ekstern, offline HDD-backup
## Backup av Fotogenitet
Overføre fra LolbraaNAS:/Lolbraa Fotogenitet til Fugl:/Lolbraa Fotogenitet ("gammel" ekstern harddisk koblet til NASen over USB)
```
rsync -avh "/mnt/user/Lolbraa\ Bilder/Lolbraa\ fotogenitet/" "/mnt/disks/Lolbraa_fotogenitet/"
```
Etter å ha dry-runnet neste kommando og sjekket at filene kan slettes, kjørt for å slette filer som er slettet/endret lokasjon/navn/osv.:
```
rsync -avh --checksum --delete /mnt/user/Lolbraa\ Bilder/Lolbraa\ fotogenitet/ /mnt/disks/Lolbraa_fotogenite
t/
```


## Backup av Immich
```
rsync -avh "/mnt/user/Lolbraa\ Bilder/Lolbraa\ fotogenitet/" "/mnt/disks/Lolbraa_fotogenitet/"
```
/mnt/user/immich/library
til 
/mnt/disks/Backup/Immich

# Slette snapshot fra Duplicacy-repo
Tok backup av noen filer med uhell. 
Fordi jeg visste dato sjekket jeg loggene for å finne revision-id for den aktuelle snapshot-id.
 dup.lolbraa.no lagde jeg en manuell jobb for å fjerne de aktuelle revisione. Jeg kjørte en backup, så den manuelle jobben, så hoved check/prune. 
 ![[Workshop kommandoer-20241018201921420.jpg|500]]
```
-id public -r 288-289 -exclusive
```
[Duplicacy Issue: How do I remove files backed up by mistake, or the entire backup id containing them?](https://duplicacy.com/issue?id=5653425186406400)
[Prune command details - How-to - Duplicacy Forum](https://forum.duplicacy.com/t/prune-command-details/1005)

# Migrere ny eksterndisk
Jeg flyttet NC Borg-repoet (samt 
Duplicacy Main Job) fra Data-disk (NTFS) til ny eksterndisk (ZFS kryptert). NC AIO støtter ikke at man endrer backup-path etter første initialisering (noe som er sykt dritt), og derfor måtte jeg sørge for at borg-repoet hadde samme path `/mnt/disks/Data/NC` (det endte meg at jeg måtte restore fra backup, så da fikk jeg ordnet dette)
Obs: Jeg endret også Duplicacy-docker-path og Telia-sky-skriptet.
1. Kopierte: Mens NC kjørte, kopierte jeg over borg-repoet med rsync (se kommandoer). Etter at repoet var kopiert over, kjørte jeg en backup. Det burde jeg ikke gjort.
*Kopierte ([linux - Copy entire file system hierarchy from one drive to another - Super User](https://superuser.com/questions/307541/copy-entire-file-system-hierarchy-from-one-drive-to-another))*
```sh
rsync -axHAWXS --numeric-ids --info=progress2 --exclude "Lolands" /mnt/disks/Data/ /mnt/disks/eksterndisk | tee /mnt/disks/eksterndisk/migration.txt
```
```migration.txt
9,760,877,527,000 100%   64.91MB/s   39:50:15 (xfr#1560624, to-chk=0/1563794)
```
*Verifiserte:*
```sh
rsync -ncaxHAWXS --numeric-ids --info=progress2 --exclude "Lolands" /mnt/disks/Data/ /mnt/disks/eksterndisk --log-file /mnt/disks/eksterndisk/migration.verify.txt
```
2. Rename: Etter backupen unmounted jeg både Data og eksterndisk, og så byttet jeg navn til Data->DataOld og eksterndisk->Data. 
3. Sjekk: Når den nye disken hadde riktig navn, mounted jeg og sjekket at alt fungerte som det skulle med NC AIO Borg-løsningen. Det fungerte delvis, men det var ett problem: Siden jeg hadde tatt en backup til den gamle disken ETTER jeg hadde kopiert, var det noen filer som manglet på den nye disken. Borg merket at registeret i cache inneholdt nyere informasjon enn registeret i repoen. Jeg forsøkte selvfølgelig å kopiere de oppdaterte filene.
*KopierBorgOppdatert*
```sh
rsync -axHAWXS --numeric-ids --info=progress2 /mnt/disks/DataOld/NC/ /mnt/disks/Data/NC --log-file /mnt/disks/eksterndisk/migration.BorgOppdatert.2.txt
```
4. Repair: Jeg forsøkte å reparere det med en verify, verify-repair og så backup (husker ikke nøyaktig forløpet). Men uansett hva jeg gjorde av verify og backups senere, fikk jeg ikke "Completely healed previously damaged file!" til å gå vekk. Var redd for at backup-repoet ikke var fullstendig lenger; kanskje korrupt. Derfor valgte jeg å restore hele NC AIO tilbake til den siste, fullstendige snapshoten jeg hadde på gamle harddisken.
5. Restore: Kopierte over gamle borg-repoet DataOld til Data. Endret navn fra Data til eksterndisk (bedre navn). Prunet/fjernet alle NC images og volumes ifølge denne guiden (obs: fjerner også dockers fra WebUI som ikke er startet). Rebootet og startet NC AIO Mastercontainer. Skrev ned det nye passordet og restored fra sist backup til en ny data-path (endret navn på den gamle til data.old. Det tok 5t40m.
6. Verify: Lot NC Desktop laste opp filer av nyere versjon fra laptop, stasjonær, osv. Og kjørte en verify for å se hvilke filer som ikke er like fra data.old til data (restored). Jeg fikk en del "sata crc error count" fra Cache SSD 3 (Kingston).
*Verify borg restore til ny nextcloud data* 
```sh
rsync -ncaxHAWXS --numeric-ids --dry-run --info=progress2 /mnt/user/nextcloud/data.old/ /mnt/user/nextcloud/data/ --log-file /mnt/disks/eksterndisk/nc.restore.verify.txt
```





# Sjekke Lolands-kopi-integritet
Før sletting av Lolands-filene kopiert til 12TB Data i Tbg.
```sh
rsync -niaHc /mnt/disks/Data/Lolands/ /mnt/user/nextcloud/data/roar/files/Backup | tee /mnt/user/nextcloud/data/roar/files/Backup/migration.verify.txtigration.verify.txt
```
> [!NOTE]- Resultat
> ```
> .d..t.og... ./
> .d..t...... Backup mai 2019/
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'07_03_28_01/DCIM/101MSDCF/
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'07_03_28_01/DCIM/101MSDCF/DSC02260.JPG
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'07_12_31_01/DCIM/101MSDCF/
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'07_12_31_01/DCIM/101MSDCF/DSC02544.JPG
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'07_12_31_01/DCIM/101MSDCF/DSC02670.JPG
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'08_04_06_03/DCIM/101MSDCF/
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'08_04_06_03/DCIM/101MSDCF/DSC02841.JPG
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'08_04_27_01/DCIM/101MSDCF/
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'08_04_27_01/DCIM/101MSDCF/DSC02906.JPG
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'08_04_27_01/DCIM/101MSDCF/DSC02914.JPG
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'08_08_25_01/DCIM/101MSDCF/
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'08_08_25_01/DCIM/101MSDCF/DSC03332.JPG
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'08_11_02_01/DCIM/101MSDCF/
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'08_11_02_01/DCIM/101MSDCF/DSC03457.JPG
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'09_01_17_01/DCIM/101MSDCF/
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'09_01_17_01/DCIM/101MSDCF/DSC03673.JPG
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'09_03_09_01/DCIM/101MSDCF/
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'09_03_09_01/DCIM/101MSDCF/DSC03707.JPG
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'09_04_24_01/DCIM/101MSDCF/
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'09_04_24_01/DCIM/101MSDCF/DSC03823.JPG
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'09_04_24_01/DCIM/101MSDCF/DSC03841.JPG
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'09_04_24_01/DCIM/101MSDCF/DSC03867.JPG
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'09_04_24_01/DCIM/101MSDCF/DSC03952.JPG
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'09_06_01_01/DCIM/101MSDCF/
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'09_06_01_01/DCIM/101MSDCF/DSC04108.JPG
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'09_07_31_01/DCIM/101MSDCF/
> .d..t...... Backup mai 2019/Alle bilder i kataloger/'09_12_18_01/DCIM/101MSDCF/
> >f+++++++++ Backup mai 2019/Alle bilder i kataloger/'09_12_18_01/DCIM/101MSDCF/DSC04587.JPG
> .d..t...... Backup mai 2019/Ellen Marie Mobil/Bilder fra nyeste mobil/
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 8") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 9") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00186.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00187.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00188.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00189.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00190.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00191.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00193.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00194.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00195.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00196.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00197.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00198.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00199.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00200.MPG") failed: Input/output error (5)
> rsync: [sender] readlink_stat("/mnt/disks/Data/Lolands/Backup mai 2019/Video/DVD 7/M2U00201.MPG") failed: Input/output error (5)
> .d..t...... Backup mai 2019/Fra VHS/
> .d..t...... Backup mai 2019/Video/DVD 7/
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00171.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00172.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00173.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00174.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00175.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00176.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00177.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00178.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00179.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00180.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00181.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00182.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00183.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00184.MPG
> >f+++++++++ Backup mai 2019/Video/DVD 7/M2U00185.MPG
> .f...pog... Denne er kjøpt 2019/Instruction Manual for Safety and Comfort.pdf
> .f...pog... Denne er kjøpt 2019/TOSHIBA CANVIO BASICS.pdf
> .d..t...... Midlertidig backup 08.12.2021/
> .d..t...... Midlertidig backup 08.12.2021/Ferdig film/
> rsync error: some files/attrs were not transferred (see previous errors) (code 23) at main.c(1336) [sender=3.2.7]
> ```


[ubuntu - Verifying a large directory after copy from one hard drive to another - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/313089/verifying-a-large-directory-after-copy-from-one-hard-drive-to-another)
> [!NOTE]- Original post
> [rsync](http://manpages.ubuntu.com/manpages/precise/en/man1/rsync.1.html) is often used to copy files instead of `gcp`, but it can also be used to verify a copy, however it was made. Simply do
> 
> ```
> rsync -niaHc /origfolder/ /copyfolder
> ```
> 
> Be careful to end the first folder name (the source) with a `/`. The options are
> 
> - `-n` do not copy (make no changes)
> - `-i` itemise the differences
> - `-a` preserve (i.e. compare since we have `-n`) permissions, ownerships, symbolic links, etc. and recurse down directories
> - `-H` preserve hard links
> - `-c` compare checksums
> 
> The output shows a code detailing the differences for each file or directory that differs. There is no output if they are the same. The code has columns `YXcstpoguax` where each character is a dot `.` if that aspect of the comparison is ok, or a letter:
> 
> ```
> Y is type of update: 
>    < sent (not appropriate in this case)
>    > need to copy 
>    c missing file or directory
>    h is hard link
>    . no update
>    * and rest of line is a message, eg *deleting
> X file type: f file  d dir  L symlink  D device S special file
> c checksum differs. + new item  " " same
> s size differs
> t timestamp differs
> p permissions differ
> o owner differ
> g group differ
> u (not used)
> a acl differ
> x extended attributes differ
> ```
> 
> For example,
> 
> ```
> .d..t...... a/b/                    directory timestamp differs
> cL+++++++++ a/b/d -> /nosuch2       symbolic link missing
> cS+++++++++ a/b/f                   special file missing (a/b/f is a fifo)
> >f..t...... a/b/ff                  file timestamp differs
> hf          a/b/xx1 => a/b/xx       files should be a hard linked
> cLc.t...... a/b/z -> /tmp/hi2       symbolic link to different name
> cd+++++++++ a/c/                    directory missing
> >f+++++++++ a/c/i.10                missing file needs to be copied
> ```



# rmlint: Finne og slette duplikater fra FamBraaNAS
Forsøkt Digikam og Czkawka, men finner det vanskelig å prioritere riktig: At av de filene som finnes både i recovery OG i vanlig struktur, der skal den vanlige strukturen prioriteres.

[Gentle Guide to rmlint — rmlint (2.10.1 Ludicrous Lemur) documentation](https://rmlint.readthedocs.io/en/latest/tutorial.html)
- Installert docker med ``/mnt/user/Lolbraa Backup/BraaNAS/``
- ``/mnt/user/Lolbraa Backup/BraaNAS/Fam_Braa/Fotobank``
- endret Recovery...  navn til ``!recovery``
- Kan [Original selection](https://rmlint.readthedocs.io/en/latest/tutorial.html#original-detection-selection)
	1. bruke regex for å IKKE prioritere paths matcher **recovery**, 
	2. eller flagge det som backup-direktiv med //. 
	   Sammen med "d - keep path with lowest depth"?

Forslag 1:
```
rmlint -S 'R<.*(Recovery).*>m' /mnt/user/Lolbraa Backup/BraaNAS/
```

Forslag 2:
Søker ``/Fotobank`` etter duplikater og vil prioritere å beholde alle utenom ``/!recovery``. Hvis den finner duplikater, prioriterer den filen med kortest path
```
cd "/mnt/user/Lolbraa Backup/BraaNAS/Fam_Braa/Fotobank"

rmlint -g -o pretty:stdout -o summary:stdout --keep-all-untagged -S d "/mnt/user/Lolbraa Backup/BraaNAS/Fam_Braa/Fotobank/" // "/mnt/user/Lolbraa Backup/BraaNAS/Fam_Braa/Fotobank/!recovery"
```

Output
```
==> Note: Please use the saved script below for removal, not the above output.
==> In total 1064387 files, whereof 298727 are duplicates in 117104 groups.
==> This equals 1368.67 GB of duplicates which could be removed.
==> 2 other suspicious item(s) found, which may vary in size.
==> Scanning took in total 19h 49m 8.375s.

Wrote a json file to: /mnt/user/Lolbraa Backup/BraaNAS/rmlint.json
Wrote a sh file to: /mnt/user/Lolbraa Backup/BraaNAS/rmlint.sh
```

# Zippe mange mapper fra gammel disk
```
zip -rv \
"/mnt/user/Lolbraa Backup/Diverse/HDD fra KrissStasjoner (pre 2023)/arkiv.zip" \
./Animation/ \
./M
ikkebrukt
```

# Overføre NCGNAS -> LolbraaNAS
Takeouts med rsync
Tenkte først taildrop, men den støtter ikke overføringer mellom eksterne brukere
```
rsync -avP -e ssh /mnt/user/public/firefoxdownloads/Nphotos/* root@100.104.43.35:"/mnt/user/Lolbraa Backup/Takeouts/Nora Google Takeout Photos 13.05.2024/"

rsync -avP -e ssh /mnt/user/public/firefoxdownloads/*.zip root@100.104.43.35:"/mnt/user/Lolbraa Backup/Takeouts/Google Photo Takeout 14.05.2024/"
```

# Følge NCGNAS Borg-logs
```sh
tail /mnt/user/appdata/borgmatic/logs/ncgnasoffsite.log -f -n 25
```

# Synkronisere FamBraaNAS/Fam_Braa <-> LolbraaNAS
Brukt for å deduplisere identiske filer lokalt (med Czkawka) og synkronisere endringer til FamBraaNAS.
```bash
rclone sync \
local:"/mnt/user/Lolbraa Backup/FRA BraaNAS/Fam_Braa/Fotobank" \
BraaNAS:"/Fam_Braa/Fotobank" \
-P --transfers 4 \
--dry-run \
--combined "/mnt/user/public/rclone_sync_fam_braa.log"
```

# Følge Immich Compose-logs
https://docs.docker.com/reference/cli/docker/compose/logs/
```
cd /mnt/user/appdata/docker_compose_projects/Immich;docker compose logs -f

Telle linjer
https://stackoverflow.com/questions/12457457/count-number-of-lines-in-terminal-output
cd /mnt/user/appdata/docker_compose_projects/Immich;docker compose logs | grep "Successfully generated" | wc -l
```

# Checksum av Norwaycraft-flytting
```
rsync -Pahn --checksum --log-file=/var/log/rsync-fambraanas-ncgnas-06.02.2024.log --exclude Martin/ --exclude Karoline/ --exclude "Fulle Backuper/" -e 'ssh -oHostKeyAlgorithms=+ssh-dss -p 22' sshd@192.168.1.65:/shares/Backup/* root@100.69.121.73:/mnt/user/backup/norwaycraft

Fra FamBraaNAS
rsync --checksum --dry-run --out-format="%C" /shares/Backup/!Nettverkskart.txt /dev/null

./rclone hashsum md5 braanas:/Backup/ --exclude "Fulle Backuper/**" --exclude "Karoline/**" --exclude "Martin/**" --output-file fambraahash.txt --download


Endte med å bruke https://fsumfe.sourceforge.net/
Lage Annet.md5 (for /Annet) med fsumfe (hos Martin). 

Sjekke på NCGNAS:
md5sum -c Annet.md5 2>&1 | tee Annet.md5.output
cat Annet.md5.output | grep FAILED

md5sum * 2>&1 | tee Annet.md5.output

Generere for filer som jeg endre navn
md5sum 3-Kitpvp.zip 4-Hub.zip  \
"NCv8 18.02.2021.zip" \
"NCv9 Bedwars Backup 11.12.2021.zip" \
"NCv9 Bedwars Backup v2 11.12.2021.zip" \
"NCv9 Byggeserver 20.08.2021 backup.zip" \
"NCv9 Floating Henge 07.10.2021.zip" \
"NCv9 lobby10Backup.24.09.21.zip" \
"NCv9 lobby1027.09.zip" \
"NCv9 proxy 20.03.2021.zip" \
"NCv9 Survival Backup 13.03.2021.zip" \
NCv9Survival.20.03.2021.zip \
2>&1 | tee endretnavn.md5


```

# Signal lage gruppe
```bash
curl -X 'POST' \
  'http://192.168.0.10:9922/v1/groups/%2B4748361836' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "description": "Gruppe for varsel. Lagd med REST API hostet på LolbraaNAS",
  "group_link": "disabled",
  "members": [
    "+4748361836",
    "+4746747614"
  ],
  "name": "NCG Varsel",
  "permissions": {
    "add_members": "only-admins",
    "edit_group": "only-admins"
  }
}'

Respons:
{"id":"group.UUtMa3hRQ0ZCRVJaWFY4MmdXUU5VVFdMWWNoeGZ6dlJhVUt3UW1pUXY0VT0="}
```

# Unmount-errors
https://forums.unraid.net/topic/12941-solved-how-to-mount-a-drive-that-unraid-wont-mount/
https://stackoverflow.com/questions/624154/linux-which-process-is-causing-device-busy-when-doing-umount
https://forums.unraid.net/topic/91696-solved-cannot-unmount-mntcache-to-stop-array/
https://github.com/BinsonBuzz/unraid_rclone_mount/issues/28
https://www.reddit.com/r/unRAID/comments/78xhpr/cant_stop_array_stuck_on_retry_unmounting_user/
Open Files-plugin fra CA (under tools)
Stop Shell-plugin fra CA
```
/usr/local/emhttp/webGui/event/unmounting_disks/stop_shell

#!/bin/bash
# read cache pools or fallback to legacy /mnt/cache
if [[ -d /boot/config/pools ]]; then
  cache=$(ls /boot/config/pools|sed 's:.cfg$::;s:^:/mnt/:')
else
  cache=/mnt/cache
fi
# stop any open shell which prevents unmounting of array
for PID in $(lsof /mnt/disk[0-9]* $cache /mnt/user /mnt/user0 2>/dev/null|awk '/^(bash|sh|mc) /{print $2}'); do
  kill $PID 1>/dev/null 2>&1
done
```

Etter mye lsof, htop og annet, kjørte jeg denne som fungerte ([ref](https://stackoverflow.com/questions/7878707/how-to-unmount-a-busy-device))
```
pkill sh
```