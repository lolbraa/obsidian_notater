# Følge Immich Compose-logs
https://docs.docker.com/reference/cli/docker/compose/logs/
```
cd /mnt/user/appdata/docker_compose_projects/Immich;docker compose logs -f
```

# Hardwaretranscoding
Se [[Hardwaretranscoding#Immich]]

# Immich bruker-IDer
Mamma 8a6e3d1d-d632-4417-9494-f6dbceac4d76
Pappa cc4f5ed5-c223-441d-97df-c5e4419241fb
Nora 3cd0aea0-362a-4c81-a355-6329261f4981
Kristoffer 6fcec7fc-6bb7-4930-8b9a-c8483b7864f8

## OAuth
Se [[Nettverkssikkerhet#Access - OAuth]] for hvordan Login-systemet fungerer med Cloudflare Access for OAuth-identifisering.


# Backup
Immich autobackup

# External libraries
OBS: Per 1.124 må assets importeres som nye hvis man flytter/endrer noe på pathen! Altså gamle blir lagt i trash, så blir nye importert og må genereres nye thumbnails.
## Braa Fotobank
Bildene lever på BraaNAS:/felles/Fotobank, men synkroniseres med rsync (se userscript).
Per 14.01.2025 er det 543,540 assets. 
Det tok lang tid å legge inn i Immich. 
La det til en egen bruker for å ikke surre alle bildene inn i eksisterende bruker.
De fleste previewsa ble generert med WebP 720p for å spare plass og gjøre det så raskt som mulig. Vanlig 1080p jpg.

Valgte å fjerne Recovery-mappa, og da gikk det ned til 169,446 assets. Stikkprøver viste at det kun var små bilder (thumbnails fra annet program?) med dårlig oppløsning, og av alle bilder med dårlig oppløsning fantes det ett original i en vanlig mappestruktur.



# Rydding
## Fjerne problem-/untracked-files
### Manuelt alternativ
https://github.com/immich-app/immich/discussions/4592

```
#1. Eksporter untracked files http://immich/admin/repair til "/mnt/user/immich/untracked 29.07.2024.txt"
#2. Endre txt-filene til å bruke host-filsystem-paths. /usr/src/app/upload/ til /mnt/user/immich/library/.
#3. Kjør move-script
#4. Importer med Immich CLI eller dra over i nettleseren

#Mamma 8a6e3d1d-d632-4417-9494-f6dbceac4d76
#Pappa cc4f5ed5-c223-441d-97df-c5e4419241fb
#Nora 3cd0aea0-362a-4c81-a355-6329261f4981
#Kristoffer 6fcec7fc-6bb7-4930-8b9a-c8483b7864f8

  
# Kopiere filer fra en backup-restore
for file in $(cat "/mnt/user/immich/untracked 29.07.2024.txt" | grep 8a6e3d1d-d632-4417-9494-f6dbceac4d76); do cp "$file" /mnt/user/immich/untracked/mamma/; done

for file in $(cat "/mnt/user/immich/untracked 29.07.2024.txt" | grep cc4f5ed5-c223-441d-97df-c5e4419241fb); do cp "$file" /mnt/user/immich/untracked/pappa/; done

for file in $(cat "/mnt/user/immich/untracked 29.07.2024.txt" | grep 3cd0aea0-362a-4c81-a355-6329261f4981); do cp "$file" /mnt/user/immich/untracked/nora/; done

for file in $(cat "/mnt/user/immich/untracked 29.07.2024.txt" | grep 6fcec7fc-6bb7-4930-8b9a-c8483b7864f8); do cp "$file" /mnt/user/immich/untracked/kristoffer/; done


# Slette untracked files fra Immich
for file in $(cat "/mnt/user/immich/untracked 29.07.2024.txt"); do mv "$file" /mnt/user/immich/untracked/slett/; done
```
### Immich-tools
1. [GitHub - Thoroslives/immich\_remove\_offline\_files: A simple way to remove orphaned offline assets from Immich's database.](https://github.com/Thoroslives/immich_remove_offline_files)
2. [GitHub - clumsyCoder00/Immich-Tools: A couple of tools to fill in the gaps of published tools to manage offline and untracked files in Immich.](https://github.com/clumsyCoder00/Immich-Tools)
#### 01.08.2024
Kjørte en gjennomgang av 6587 "untracked assets" med ``root@LolbraaNAS:/mnt/user/immich# sh move_untracke_files.sh ``.
- Slettet encoded_videos og thumbs.
- Mappe ``/upload``: Gikk gjennom mange filer, spesielt Nora og Kristoffer sine. Alle jeg fant var korrupte (utenom et par laaange filmer som var lastet opp med uhell). Noen kunne jeg salvage med [Repair corrupt, unreadable MP4 MOV video files online](https://fix.video), men de fleste viste ingen ting. 
  Konklusjon: Dette er filer som ble avbrutt under opplastning, og har derfor blitt etterlatt/ikke slettet av Immich_Server. Filene skal ha blitt lastet opp riktig i etterkant (forhåpentligvis).
- Mappe ``/library``: Disse filene eksisterer også allerede i Immich (under ``...+1``). Aner ikke hvorfor de var lost.

Kjørte `immich_remove_offline_files.py` for Kriss, Nora og Inger.
```sh
python3 immich_remove_offline_files.py --admin_apikey "1pass" --user_apikey "1pass" --immichaddress "http://192.168.0.10:2283"
```
Resulterte i kun offline paths for for thumbs (person). [[Overgang fra Google til Self Hosted-20240801210531668.jpg]]

## Sjekke database
[pgAdmin 4](http://192.168.0.10:15432/browser/)
Video-transcoding-progresjon
```sql
SELECT * 
FROM public.assets 
WHERE "originalPath" LIKE '/usr/src/app/external/lolandfotobank/Backup/Backup mai 2019/Fra VHS/%'
ORDER BY id ASC LIMIT 100
```
```sql
SELECT * 
FROM public.assets 
WHERE "type" = 'VIDEO' AND "encodedVideoPath" = '';
```
```sql
SELECT * 
FROM public.assets 
WHERE id = '5b873525-5372-4a95-b80f-0d2730da9fa6';
```

### Duplikater
Finne alle objekter som har samme originalnavn mellom to brukere, og kun vise en linje per originale navn.
```sql
SELECT "originalFileName"
FROM public.assets
WHERE "ownerId" = '3cd0aea0-362a-4c81-a355-6329261f4981' OR "ownerId" = '6fcec7fc-6bb7-4930-8b9a-c8483b7864f8'
GROUP BY "originalFileName"
HAVING COUNT(DISTINCT "ownerId") > 1
```

Liste alle assets/duplikater med deres respektive eier.
```sql
SELECT "originalFileName", "ownerId"
FROM public.assets
WHERE "ownerId" IN ('3cd0aea0-362a-4c81-a355-6329261f4981', '6fcec7fc-6bb7-4930-8b9a-c8483b7864f8')
  AND "fileCreatedAt" < '2018-01-01'
  AND "originalFileName" IN (
    SELECT "originalFileName"
    FROM public.assets
    WHERE "ownerId" IN ('3cd0aea0-362a-4c81-a355-6329261f4981', '6fcec7fc-6bb7-4930-8b9a-c8483b7864f8')
      AND "fileCreatedAt" < '2018-01-01'
    GROUP BY "originalFileName"
    HAVING COUNT(DISTINCT "ownerId") > 1
)
ORDER BY "originalFileName", "ownerId";
```

Også sjekke om de er favorittmerket eller allerede slettet
```sql
SELECT *
FROM public.assets
WHERE "ownerId" = '3cd0aea0-362a-4c81-a355-6329261f4981'
  AND "isFavorite" = false
  AND "deletedAt" IS NULL
  AND "originalFileName" IN (
    SELECT "originalFileName"
    FROM public.assets
    WHERE "ownerId" IN ('3cd0aea0-362a-4c81-a355-6329261f4981', '6fcec7fc-6bb7-4930-8b9a-c8483b7864f8')
      AND "fileCreatedAt" < '2018-01-01'
    GROUP BY "originalFileName"
    HAVING COUNT(DISTINCT "ownerId") > 1
    LIMIT 1
);
```

"slette" en fil
```sql
UPDATE public.assets
SET "deletedAt" = NOW()
WHERE id = '38a74b06-0672-42fc-81fa-f7c25296f9fc'
```

Hva jeg endte med å kjøre
```sql
UPDATE public.assets
SET "deletedAt" = NOW()
WHERE "ownerId" = '3cd0aea0-362a-4c81-a355-6329261f4981'
  AND "isFavorite" = false
  AND "deletedAt" IS NULL
  AND "checksum" IN (
    SELECT "checksum"
    FROM public.assets
    WHERE "ownerId" IN ('3cd0aea0-362a-4c81-a355-6329261f4981', '6fcec7fc-6bb7-4930-8b9a-c8483b7864f8')
      AND "fileCreatedAt" < '2018-01-01'
    GROUP BY "checksum"
    HAVING COUNT(DISTINCT "ownerId") > 1
);
```

[Database Queries | Immich](https://immich.app/docs/guides/database-queries/)
```sql
SELECT T1."checksum", array_agg(T2."id") ids FROM "assets" T1
  INNER JOIN "assets" T2 ON T1."checksum" = T2."checksum" AND T1."id" != T2."id" AND T2."deletedAt" IS NULL
  WHERE T1."deletedAt" IS NULL GROUP BY T1."checksum";
```


## Korrupte filer
*Alle bildene/videoene som er korrupte er slettet fra filsystemet*
### Andre
*Får ikke åpnet vanlig heller. Korrupt opplastning?*
library/inger/2024/2024.05.20/27bccdc9-b43d-4b41-8975-093e526fc267.HEIC: bad seek to 3936681
library/inger/2024/2024.05.23/ae350973-6d0b-4476-b15e-84eed65bf183.HEIC: bad seek to 2136731
library/nora/2024/2024.05.17/0284ebf3-63a6-4556-9f2f-6c0943dadb78.HEIC: bad seek to 4020107
library/nora/2024/2024.04.20/a31f2481-2998-4221-baa5-85e4c311ffcc.HEIC

```sh
root@LolbraaNAS:/mnt/user/immich# find . -size 0

./library/library/untracked.txt.save
./library/thumbs/6fcec7fc-6bb7-4930-8b9a-c8483b7864f8/34/09/3409a409-dbac-414d-8f82-c61d31043eeb-thumbnail.webp
./library/thumbs/6fcec7fc-6bb7-4930-8b9a-c8483b7864f8/a7/8f/a78f9a54-6131-4e4c-971f-6b3b8fe9b931-thumbnail.webp
./library/thumbs/6fcec7fc-6bb7-4930-8b9a-c8483b7864f8/72/31/7231baf2-56a8-4a63-8d69-764d5e69699f-thumbnail.webp
./library/thumbs/3cd0aea0-362a-4c81-a355-6329261f4981/30/ae/30aec79a-2291-4048-8470-a4fb9eb76917-preview.jpeg
./library/thumbs/3cd0aea0-362a-4c81-a355-6329261f4981/48/dd/48ddf769-ee42-4652-ae48-61cba2a549ab-preview.jpeg
./library/thumbs/cc4f5ed5-c223-441d-97df-c5e4419241fb/01/d7/01d74ce4-a102-40fb-b28d-ea4683bda936-preview.jpeg
./library/thumbs/cc4f5ed5-c223-441d-97df-c5e4419241fb/44/a0/44a06ef0-9771-41fc-aad3-b5cc04193202-preview.jpeg
./library/thumbs/cc4f5ed5-c223-441d-97df-c5e4419241fb/23/46/2346ce02-de98-4c4a-adb4-4a8e8d1e8bcf-preview.jpeg
./library/thumbs/cc4f5ed5-c223-441d-97df-c5e4419241fb/d3/98/d398c1df-9e55-4bbb-a8ff-279daa0b8d55-preview.jpeg
./library/thumbs/cc4f5ed5-c223-441d-97df-c5e4419241fb/d9/f4/d9f48dd2-5e8e-4e81-bd79-e86b2e9541ea-preview.jpeg
./library/thumbs/cc4f5ed5-c223-441d-97df-c5e4419241fb/48/7a/487a72d0-7e14-4bfa-8009-ec0db82e6525-thumbnail.webp
./library/thumbs/cc4f5ed5-c223-441d-97df-c5e4419241fb/3b/ae/3bae4654-473d-4b57-a074-4fc75b5ca0ab-preview.jpeg
./library/thumbs/cc4f5ed5-c223-441d-97df-c5e4419241fb/b4/d2/b4d2cc49-8a64-4943-b4db-66738ec326a3-preview.jpeg
./library/thumbs/cc4f5ed5-c223-441d-97df-c5e4419241fb/8d/53/8d53b41c-d50f-4544-9565-8e2f5735a83c-preview.jpeg
./library/thumbs/8a6e3d1d-d632-4417-9494-f6dbceac4d76/0e/26/0e264855-ced7-45d8-8beb-702f6b4a554e-preview.jpeg
./library/thumbs/8a6e3d1d-d632-4417-9494-f6dbceac4d76/6a/e4/6ae4698c-55af-4054-a1e6-f2548d62ae60-preview.jpeg
./library/thumbs/8a6e3d1d-d632-4417-9494-f6dbceac4d76/86/95/86953ce4-e4a7-427f-8039-a0e4a57d51d3-preview.jpeg
./library/thumbs/8a6e3d1d-d632-4417-9494-f6dbceac4d76/06/2a/062af321-121e-49ee-9cb2-aecc559d7c3d-preview.jpeg
./library/thumbs/8a6e3d1d-d632-4417-9494-f6dbceac4d76/4f/7f/4f7f9e65-123a-43c7-98a5-d2e487eadfe1-preview.jpeg
./library/thumbs/8a6e3d1d-d632-4417-9494-f6dbceac4d76/a8/4f/a84f67bf-1bc2-4a51-8454-e3de0804600e-preview.jpeg
./untracked/slett/3409a409-dbac-414d-8f82-c61d31043eeb-thumbnail.webp
./untracked/slett/7231baf2-56a8-4a63-8d69-764d5e69699f-thumbnail.webp
./untracked/slett/a78f9a54-6131-4e4c-971f-6b3b8fe9b931-thumbnail.webp

root@LolbraaNAS:/mnt/user/immich# find . -size 0 -delete
```


### Lolandfotobank
Backup mai 2019\\Video\\DVD 7
- M2U00171.MPG
- M2U00172.MPG
- M2U00173.MPG
- …
- M2U00185.MPG

Midlertidig backup 08.12.2021/nora/MOV_0206.mp4

Backup mai 2019/Alle bilder i kataloger/'09_07_31_01/DCIM/101MSDCF/DSC04184.JPG
Backup mai 2019/Alle bilder i kataloger/'09_06_01_01/DCIM/101MSDCF/DSC04108.JPG
Backup mai 2019/Alle bilder i kataloger/'09_04_24_01/DCIM/101MSDCF/DSC03952.JPG
	DSC03867
	DSC03841

*Etter funnet de over manuelt, fant alle .JPG som er 0 størrelse*
```
root@LolbraaNAS:/mnt/user/nextcloud/data/roar/files/Backup/Backup mai 2019/Alle bilder i kataloger# find . -size 0 -name "*.JPG"

./'08_04_06_03/DCIM/101MSDCF/DSC02841.JPG
./'07_03_28_01/DCIM/101MSDCF/DSC02260.JPG
./'07_12_31_01/DCIM/101MSDCF/DSC02544.JPG
./'07_12_31_01/DCIM/101MSDCF/DSC02670.JPG
./'08_04_27_01/DCIM/101MSDCF/DSC02906.JPG
./'08_04_27_01/DCIM/101MSDCF/DSC02914.JPG
./'08_08_25_01/DCIM/101MSDCF/DSC03332.JPG
./'08_11_02_01/DCIM/101MSDCF/DSC03457.JPG
./'09_01_17_01/DCIM/101MSDCF/DSC03673.JPG
./'09_03_09_01/DCIM/101MSDCF/DSC03707.JPG
./'09_12_18_01/DCIM/101MSDCF/DSC04587.JPG

find . -size 0 -name "*.JPG" -delete
```

## FamBraaNAS/Fotobank
```
==> Note: Please use the saved script below for removal, not the above output.
==> In total 1064387 files, whereof 298727 are duplicates in 117104 groups.
==> This equals 1368.67 GB of duplicates which could be removed.
==> 2 other suspicious item(s) found, which may vary in size.
==> Scanning took in total 19h 49m 8.375s.

Wrote a json file to: /mnt/user/Lolbraa Backup/BraaNAS/rmlint.json
Wrote a sh file to: /mnt/user/Lolbraa Backup/BraaNAS/rmlint.sh
==> Note: Please use the saved script below for removal, not the above output.
==> In total 1064387 files, whereof 298727 are duplicates in 117104 groups.
==> This equals 1368.67 GB of duplicates which could be removed
==> 2 other suspicious item(s) found, which may vary in size.
==> Scanning took in total 19h 49m 8.375s.

Wrote a json file to: /mnt/user/Lolbraa Backup/BraaNAS/rmlint.json
Wrote a sh file to: /mnt/user/Lolbraa Backup/BraaNAS/rmlint.sh
```

## Diverse
### 09.10.2024: Fjernet duplikater fra Nora sin konto av bilder fra Kriss sin telefon
Søkte i Nora sin konto på metadata kameraer som tilsvarer Kristoffers tidligere telefoner (og "not in any albums"). Før jeg slettet alle, gikk jeg gjennom og "hjertet" bildene på Kriss' konto som Nora hadde hjertet på sin konto. Brukte et skript med Autokey på Linux som beskrevet under: 

Hadde to firefox-vinduer oppe med Immich i søkemodus. 
- Til venstre, Kriss sin konto kun originalFileName som parameter, https://immich.lolandbraa.no/search?query=%7B%22originalFileName%22%3A%22IMG_20200725_235949%22%7D.
- Til høyre, Noras konto i søkemodus på en telefon og "favorite" valgtt, https://immich.lolandbraa.no/search?query=%7B%22make%22%3A%22Google%22%2C%22model%22%3A%22Pixel+3a%22%2C%22isNotInAlbum%22%3Atrue%7D
Skrev et autokey-skript basert på absolutt pixelverdier av hvor tekst, knapper, o.l. var plassert.
Gikk inn på ett bilde og kjørte skriptet; det går videre til neste bilde, kopierer teksten, skriver den inn som en parameter direkte i det andre vinduets URL, trykker enter, og venter på en eventuell input av "F". Hvis den trykkes, så forsøker den å hjerte de to første bildene. Valgte d som hotkey for å kjøre skriptet.
Etter å ha hjertet alle bilder, gikk jeg tilbake til søkesiden, holdt inne pagedown og valgte alle for sletting.
[API Examples · autokey/autokey Wiki · GitHub](https://github.com/autokey/autokey/wiki/API-Examples#get_clipboard)
```python
import time

# Select chrome-window right
mouse.click_absolute(1745, 829, 1)
time.sleep(0.1)

# click next picture
mouse.click_absolute(2151, 785, 1)
time.sleep(0.5)

# click filename for select
def clickncopy(pos1, pos2):
    mouse.click_absolute(pos1, pos2, 1)
    mouse.click_absolute(pos1, pos2, 1)
    time.sleep(0.3)
    try:
        fileName = clipboard.get_selection()
        time.sleep(0.3)
    except:
        fileName = "DETAILS"
    return fileName
      

fileName = clickncopy(2369, 546)

# check if text is right, else do again
if fileName == "DETAILS":
    time.sleep(0.1)
    fileName = clickncopy(2330, 677)

clipboard.fill_clipboard(fileName)
time.sleep(0.2)
# select other window
mouse.click_absolute(824, 40,1)
time.sleep(0.2)
# double click to select filename to edit in browser addressbar 668, 125
mouse.click_absolute(649, 129,1)
time.sleep(0.1)
mouse.click_absolute(649, 129,1)
time.sleep(0.2)

# send backspace
#keyboard.send_key('<backspace>',repeat=1)
#time.sleep(0.2)

# paste from clipboard
#keyboard.send_keys(fileName)
#mouse.click_absolute(649, 129, 2)  # button 2 is the middle mouse button
keyboard.press_key('<ctrl>')
keyboard.fake_keypress('v', repeat=1)
keyboard.release_key('<ctrl>')
#fill_selection(fileName)
time.sleep(0.5)

# send enter
keyboard.send_key('<enter>',repeat=1)
#time.sleep(1)

# wait for userinput to hit favorite
retCode = keyboard.wait_for_keypress('f',timeOut=5)
if retCode:
    # click-select picture 1
    mouse.click_absolute(32, 333,1)
    time.sleep(0.5)
    # click favorite
    mouse.click_absolute(1173, 225,1)
    time.sleep(0.1)
    # click-unselect picture 1
    mouse.click_absolute(32, 333,1)
    time.sleep(0.5)

    # click-select picture 2
    mouse.click_absolute(213, 339,1)
    time.sleep(0.5)
    # click favorite
    mouse.click_absolute(1173, 225,1)
    time.sleep(0.1)
```

---
# Immich-go
## Initial
Brukt userscripts

## 01.08.2024: Immich-go: Laste opp NextCloud ekstra-backup, duplikater og stacks
som har kjørt parallelt for å sjekke om Immich gjør noe korrupt. Forsøkte først dry-run.
``C:\Users\Kriss\Nextcloud\13 Unraid diagnostikk\Immich\immich-go>``
v0.21.1
```sh
./immich-go.exe -use-configuration="./immich-go.json" -server=http://192.168.0.10:2283 -key="" -log-file="./log1.log" upload -create-stacks -dry-run "C:\Users\Kriss\Nextcloud\Direkteopplasting\Camera"

./immich-go.exe -use-configuration="./immich-go.json" -server=http://192.168.0.10:2283 -key="" -log-file="./log2.log" upload -create-stacks -dry-run "C:\Users\Kriss\Nextcloud\Direkteopplasting\DCIM"
```
Gikk gjennom manuelt hva som evt. ville bli lastet opp. Alle elementene jeg sjekket var bilder som var trashed/archived med vilje. Endte derfor ikke med å laste opp noe, men slette Direkteopplasting-mappa.

Kjørte duplicate, men endte ikke med å fikse så mye. Den fant 3600 duplikater for admin - de fleste duplikater mellom Lolbraafotogenitet-hovedmappe og en utvalgte/prosjekt-mappe (hvor bildene er kopiert over), eller duplikater mellom Kristoffer sine originale bilder og Nora sin Google Takeout "keep-partner-photos" under importering.
```sh
./immich-go.exe -use-configuration="./immich-go.json" -server=http://192.168.0.10:2283 -log-file="./log3.log" duplicate -date 2018-01-01,2030-01-01
```
For å kvitte oss med partner-photoene som er duplisert, forsøker jeg å laste opp Google Takeout-arkivet en gang til, men denne gangen spesifisere at bildene går til et eget album. Forhåpentligvis registrerer den "null" nye bilder, for alle er der fra før, men legger dem allikevel til i albumet. Derifra kan jeg slette alle bilder i albumet.
`/mnt/user/nextcloud/data/kristoffer/files/13 Unraid diagnostikk/Immich/immich-go`
```sh
./immich-go -use-configuration="./immich-go.json" -server=http://192.168.0.10:2283 -key="" -log-file="./log4.log" -time-zone=Europe/Oslo upload -create-stacks -google-photos -partner-album="PartnerKristoffer" -dry-run "/mnt/user/Lolbraa Backup/Takeouts/Nora\ Google\ Takeout\ Photos\ 13.05.2024/takeout-*.zip"
```

Stacket bilder med
```sh
./immich-go.exe -use-configuration="./immich-go.json" -server=http://192.168.0.10:2283 -key="" -log-file="./log3.log" stack -yes
```

## 22.09.2024: Lastet inn iCloud Photos
/home/kriss/Nextcloud/13 Unraid diagnostikk/Immich/immich-go/
/media/kriss/ekstrassd/iCloud Photos/Photos/
```sh
cd /home/kriss/Nextcloud/13 Unraid diagnostikk/Immich/immich-go/
./immich-go -use-configuration="./immich-go.json" -server=http://192.168.0.10:2283 -key="MK4WhbpmJ6UjhSOKfUMBVYWU5nsHnnRovO2JAgeB68" -log-file="./logInger1.log" upload -create-stacks -dry-run "/media/kriss/ekstrassd/iCloud Photos/Photos/"
```


---
# Immich Albums
[GitHub - alvistar/immich-albums: Create immich albums from folder structure](https://github.com/alvistar/immich-albums)'

Måtte mounte smb-share. Unraid-sharen må eksporteres som public.
[Mount an SMB Share in Linux |Linode Docs](https://www.linode.com/docs/guides/linux-mount-smb-share/)
```sh
sudo mount -t cifs -o credentials=~/.credentials "//192.168.0.10/Lolbraa Bilder" /mnt/lolbraanas_manuell_smb

sudo umount -t cifs /mnt/lolbraanas_manuell_smb
```

```sh
cd "/mnt/lolbraanas_manuell_smb/Lolbraa fotogenitet"

im --api-key "ze9B0XDhsx75sshHNZDexpwnhb8YbHSpGUzPsmKGk" --api-host "http://192.168.0.10:2283/api" --original-path "/mnt/lolbraanas_manuell_smb/Lolbraa fotogenitet" --replace-path "/usr/src/app/external/lolbraafotogenitet" --dry-run "/mnt/lolbraanas_manuell_smb/Lolbraa fotogenitet"
```

Ikke fått til å fungere...

---

# Migrering
## Kristoffer
- [x] Google Drive Takeout - 03.2024
- [x] Importert til Nextcloud
- [x] Tatt i bruk Nextcloud
- [x] Google Photos Takeout - 03.2024
- [x] Importert til Immich
- [x] Tatt i bruk Immich
- [x] Ny Google Photos Takeout - 05.2024

## Nora
- [x] Google Drive Takeout - 13.05.2024
- [x] Importert til Nextcloud
- [ ] Tatt i bruk Nextcloud
- [x] Google Photos Takeout - 16.03.2024
- [x] Importert til Immich
- [x] Tatt i bruk Immich
- [x] Ny Google Photos Takeout - 05.2024
      lastet ned til NCGNAS. Overfører med rsync
## Mamma og pappa
- [x] Lagd brukerkontoer
- [x] Lastet ned/satt opp Tailscale og Immich

- [x] Pappa: Init-overføring (hvert fall 1800 filer) og Google Photo-takeout (25GB, 3417 bilder, 275 videoer)
	- [x] Slettet alle Google Photos (borte 18.07.2024?)
	- [ ] Skrudd av synkronisering (må teste hvor driftsikker Tailscale er først)
- [ ] Pappa: Legge inn bilder fra Fotokammeret
- [ ] Pappa: Nextcloud

- [x] Mamma: Init-overføring fra mobil
	-  Inkluderer iCloud Photos nedlastning underveis (ca 41GB, 8221 bilder, 420 videoer)
	-  Forsøkte å laste ned mest mulig i GPhotos (ca 66GB) , men fylte telefonen i forsøket
- [x] Mamma: Google Photo-takeout
- [ ] Mamma: Apple Photo-takeout
	- Utrolig vanskelig å finne, men [Data & privacy](https://privacy.apple.com/) og [Transfer a copy of your iCloud Photos collection to another service - Apple Support](https://support.apple.com/en-us/118257)
- [x] Mamma: Slette begge


## Stats
*2TB-abonnement hos Google kostet 900kr/året før 2024, 1250kr/året etter.

Dette var cirka før noe var slettet (fjernet fra søppelbøtta). Komprimerer alt og fjerner de største filene i Photos. 
### Kristoffer
![[Overgang fra Google til Self Hosted-20240516093333545.jpg|300]]
![[Overgang fra Google til Self Hosted-20240516092519821.jpg|300]]
etter
![[Overgang fra Google til Self Hosted-20240519114517944.jpg|600]]

### Nora
![[Overgang fra Google til Self Hosted-20240516092732324.jpg|300]]
![[Overgang fra Google til Self Hosted-20240516093015563.jpg|300]]
etter
![[Overgang fra Google til Self Hosted-20240519114627725.jpg|600]]

## Checksum Nora
[How to Verify Checksum on Linux](https://itsfoss.com/checksum-tools-guide-linux/)
	NCGNAS: 
```
90047f78442df778475832471ed755eee763967ff269441f67f1c03cdd120fed  takeout-20240513T064528Z-001.zip
851e913a313beb371505d4b159cca702bc8c79374b97ad8fecb6b01e56a7fa99  takeout-20240513T064528Z-002.zip
361b79d75c38d5e2fb3a6b984c79d09508ccb2c3b88a50548f14d7af79778e46  takeout-20240513T064528Z-003.zip
32125898da7559a370f2545b96626c4825646b3ce429c5c3b2a3dfdd6531ee7d  takeout-20240513T064528Z-004.zip
24182e8cf9d4acdc2891f7fd20b65c655d77a6d04800f23f3a6556e2ddfe8b95  takeout-20240513T064528Z-005.zip
e8d4b7845c4edd13d2177b67178ad793ad3779ae526764e540ec217c88d0cdd6  takeout-20240513T064528Z-006.zip
a88002d85575d1ad63209c0f9e52aab9f5b5360df8f9b83dea4a8e473398a3c7  takeout-20240513T064528Z-007.zip
c37233bebba6027dbec70d91bb73b71166109fb06bda4ac8165d21f9913410c3  takeout-20240513T064528Z-008.zip
54b83bbf80f91d157dcda0c97297344785cbf0ef3c3047e93b9aa4cf6682b749  takeout-20240513T064528Z-009.zip
f644430f4cba4d42991d07abdbdd9f25e61ce1705d65825fe15fd4cb4b2755f6  takeout-20240513T064528Z-010.zip
```
	LolbraaNAS:
```
# sha256sum *
90047f78442df778475832471ed755eee763967ff269441f67f1c03cdd120fed  takeout-20240513T064528Z-001.zip
851e913a313beb371505d4b159cca702bc8c79374b97ad8fecb6b01e56a7fa99  takeout-20240513T064528Z-002.zip
361b79d75c38d5e2fb3a6b984c79d09508ccb2c3b88a50548f14d7af79778e46  takeout-20240513T064528Z-003.zip
32125898da7559a370f2545b96626c4825646b3ce429c5c3b2a3dfdd6531ee7d  takeout-20240513T064528Z-004.zip
24182e8cf9d4acdc2891f7fd20b65c655d77a6d04800f23f3a6556e2ddfe8b95  takeout-20240513T064528Z-005.zip
e8d4b7845c4edd13d2177b67178ad793ad3779ae526764e540ec217c88d0cdd6  takeout-20240513T064528Z-006.zip
a88002d85575d1ad63209c0f9e52aab9f5b5360df8f9b83dea4a8e473398a3c7  takeout-20240513T064528Z-007.zip
c37233bebba6027dbec70d91bb73b71166109fb06bda4ac8165d21f9913410c3  takeout-20240513T064528Z-008.zip
54b83bbf80f91d157dcda0c97297344785cbf0ef3c3047e93b9aa4cf6682b749  takeout-20240513T064528Z-009.zip
f644430f4cba4d42991d07abdbdd9f25e61ce1705d65825fe15fd4cb4b2755f6  takeout-20240513T064528Z-010.zip
```
## Checksum Kristoffer
[How to Verify Checksum on Linux](https://itsfoss.com/checksum-tools-guide-linux/)
	NCGNAS: 
```
3fef666e6f5bb1e315e6cee70295a3077da602957a14b28fbba8026f2b128d73  takeout-20240512T052450Z-001.zip
79bd3a29221d41dfbbebeb5a82ebec73176c178ae077ff903941e434f6e43c33  takeout-20240512T052450Z-002.zip
4d7f3a02a00d9e2cd58e10d80354e6577777942343839da9d305534467f7b98d  takeout-20240512T052450Z-003.zip
07301ed7fa1aa43f5791f7c1a5196751bae85c018bed3a2ba59dcd860d09573a  takeout-20240512T052450Z-004.zip
efa930bb63c7bd96c81968099dca6c2bc169795c7d90846ba3f7aa91576b3c22  takeout-20240512T052450Z-005.zip
40df8b52ff0029a96ef8b9240a8c130e8aad4bd88351a27a817d638897fe6a40  takeout-20240512T052450Z-006.zip
7d9dcf5d9756f45d74551057bc151d3880fe3e4cab508c3bfd8dd8e3f13cf094  takeout-20240512T052450Z-007.zip
0987019460cb2663d1fa6f3da704d2562849ef21a8fb8f9e9c3f5e1c2c845f1e  takeout-20240512T052450Z-008.zip
80d97dba162588c5d9d54b8f15cf65aadc2fbfef7576507c598758f6215a6660  takeout-20240512T052450Z-010.zip
c6321bbee96882df9cf45715fe5cd5d5e5177650e7734d575ea366f7baf27ed8  takeout-20240512T052450Z-011.zip
584656c2f3786594bf57f3b6d59f887b410b499a8b65610073700efb0a5eb6a6  takeout-20240512T052450Z-012.zip
```
	LolbraaNAS:
```
# sha256sum *
3fef666e6f5bb1e315e6cee70295a3077da602957a14b28fbba8026f2b128d73  takeout-20240512T052450Z-001.zip
79bd3a29221d41dfbbebeb5a82ebec73176c178ae077ff903941e434f6e43c33  takeout-20240512T052450Z-002.zip
4d7f3a02a00d9e2cd58e10d80354e6577777942343839da9d305534467f7b98d  takeout-20240512T052450Z-003.zip

# kommando brukt for å kun finne checksum av noen filer
# for i in 4 5 6 7 8 10 11 12; do sha256sum *$i.zip; done
07301ed7fa1aa43f5791f7c1a5196751bae85c018bed3a2ba59dcd860d09573a  takeout-20240512T052450Z-004.zip
efa930bb63c7bd96c81968099dca6c2bc169795c7d90846ba3f7aa91576b3c22  takeout-20240512T052450Z-005.zip
40df8b52ff0029a96ef8b9240a8c130e8aad4bd88351a27a817d638897fe6a40  takeout-20240512T052450Z-006.zip
7d9dcf5d9756f45d74551057bc151d3880fe3e4cab508c3bfd8dd8e3f13cf094  takeout-20240512T052450Z-007.zip
0987019460cb2663d1fa6f3da704d2562849ef21a8fb8f9e9c3f5e1c2c845f1e  takeout-20240512T052450Z-008.zip
80d97dba162588c5d9d54b8f15cf65aadc2fbfef7576507c598758f6215a6660  takeout-20240512T052450Z-010.zip
c6321bbee96882df9cf45715fe5cd5d5e5177650e7734d575ea366f7baf27ed8  takeout-20240512T052450Z-011.zip
584656c2f3786594bf57f3b6d59f887b410b499a8b65610073700efb0a5eb6a6  takeout-20240512T052450Z-012.zip
```



# Informasjon fra første deployment
Immich - laget med Docker-Compose
- Oppdatering etter instrukser nederst https://immich.app/docs/install/unraid
- Backup etter instrukser https://immich.app/docs/administration/backup-and-restore
	- Automatisert med instruksene som står der med bildet https://github.com/prodrigestivill/docker-postgres-backup-local
	- Backup-dir: /mnt/user/Lolbraa Backup/Homelab Backups/Immich_Backup/
	- FORELØPIG KUN DATABASE, IKKE ORIGINAL-filer
		- Restore: gunzip < db_dumps/last/immich-latest.sql.gz | docker exec -i immich_postgres psql -U postgres -d immich
- Import av Google Takeout
	- Betalt løsning https://metadatafixer.com/pricing
	- Immich-go (brukt 10.2023 for hele katalogen. Gikk for det meste bra)
	- For å bytte ut Google Photos:
		- Immich (evt Google Memories) må være mer stabilt (alle alternativene er ganske ferske)
		- Bedre og lettere hardware acceleration
		- Bedre instrukser for hvilke transcoding-innstillinger
		- Bedre import-verktøy fra Google-Photos 
			- Immich-go ga noen rar datoer og la ikke automatisk filer i arkivet



# Troubleshooting
## Velge beste codecs for videoer.
encoded videos tar MYE plass - mer enn opplastede medier (ikke medberegnet external libraries)
```
root@LolbraaNAS:/mnt/user/immich/library# du --human-readable --all --total --max-depth=1
22G     ./backups
*1.1T    ./library
643M    ./upload
*990G    ./encoded-video
75G     ./thumbs
788K    ./profile
2.2T    .
2.2T    total
root@LolbraaNAS:/mnt/user/immich/library# du upload/ --human-readable --all --total --max-depth=1
206M    upload/6fcec7fc-6bb7-4930-8b9a-c8483b7864f8
428M    upload/3cd0aea0-362a-4c81-a355-6329261f4981
3.8M    upload/ea829b4b-904e-407b-92f7-e7b88419433d
557K    upload/a68b0f83-1697-40fd-818c-ad662d3000d1
4.0M    upload/cc4f5ed5-c223-441d-97df-c5e4419241fb
1.8M    upload/8a6e3d1d-d632-4417-9494-f6dbceac4d76
0       upload/a8423591-065f-40b7-9cd0-9e656a980884
4.0K    upload/.immich
643M    upload/
643M    total
```

## Error fra database etter oppdatering og forsøkt ny ML-modell
Stuck i boot-loop etter denne erroren etter oppdatering til 1.125.2
```
immich_server            | [Nest] 7  - 01/24/2025, 10:20:27 PM     LOG [Microservices:SmartInfoService] Dimension size of model ViT-B-32__openai is 512, but database expects 1024.
immich_server            | [Nest] 7  - 01/24/2025, 10:20:27 PM     LOG [Microservices:SmartInfoService] Updating database CLIP dimension size to 512.
immich_server            | Query failed : {
immich_server            |   durationMs: 20.02325799999744,
immich_server            |   error: PostgresError: syntax error at or near "'vector(512)'"
immich_server            |       at ErrorResponse (/usr/src/app/node_modules/postgres/cjs/src/connection.js:788:26)
immich_server            |       at handle (/usr/src/app/node_modules/postgres/cjs/src/connection.js:474:6)
immich_server            |       at Socket.data (/usr/src/app/node_modules/postgres/cjs/src/connection.js:315:9)
immich_server            |       at Socket.emit (node:events:524:28)
immich_server            |       at addChunk (node:internal/streams/readable:561:12)
immich_server            |       at readableAddChunkPushByteMode (node:internal/streams/readable:512:3)
immich_server            |       at Readable.push (node:internal/streams/readable:392:5)
immich_server            |       at TCP.onStreamRead (node:internal/stream_base_commons:189:23) {
immich_server            |     severity_local: 'ERROR',
immich_server            |     severity: 'ERROR',
immich_server            |     code: '42601',
immich_server            |     position: '58',
immich_server            |     file: 'scan.l',
immich_server            |     line: '1176',
immich_server            |     routine: 'scanner_yyerror'
immich_server            |   },
immich_server            |   sql: `alter table "smart_search" alter column "embedding" type 'vector(512)'`,
immich_server            |   params: []
immich_server            | }
immich_server            | PostgresError: syntax error at or near "'vector(512)'"
immich_server            |     at ErrorResponse (/usr/src/app/node_modules/postgres/cjs/src/connection.js:788:26)
immich_server            |     at handle (/usr/src/app/node_modules/postgres/cjs/src/connection.js:474:6)
immich_server            |     at Socket.data (/usr/src/app/node_modules/postgres/cjs/src/connection.js:315:9)
immich_server            |     at Socket.emit (node:events:524:28)
immich_server            |     at addChunk (node:internal/streams/readable:561:12)
immich_server            |     at readableAddChunkPushByteMode (node:internal/streams/readable:512:3)
immich_server            |     at Readable.push (node:internal/streams/readable:392:5)
immich_server            |     at TCP.onStreamRead (node:internal/stream_base_commons:189:23) {
immich_server            |   severity_local: 'ERROR',
immich_server            |   severity: 'ERROR',
immich_server            |   code: '42601',
immich_server            |   position: '58',
immich_server            |   file: 'scan.l',
immich_server            |   line: '1176',
immich_server            |   routine: 'scanner_yyerror'
immich_server            | }
immich_server            | microservices worker error: PostgresError: syntax error at or near "'vector(512)'"
immich_server            | microservices worker exited with code 1
immich_server            | Killing api process
immich_server            | Initializing Immich v1.125.2
immich_server            | Detected CPU Cores: 4
immich_server            | Starting api worker
immich_server            | Starting microservices worker
```
[Updating the smart search model causes Postgres syntax error · Issue #15590 · immich-app/immich · GitHub](https://github.com/immich-app/immich/issues/15590)
```
docker exec -it immich_postgres psql --dbname=immich --username=postgres

alter table "smart_search" alter column "embedding" type vector(512); 
```