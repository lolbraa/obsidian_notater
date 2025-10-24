[Jellyfin](https://stream.lolandbraa.no/)
[Prowlarr](http://media:9696/)
[Radarr](http://media:7878/)
[Sonarr](http://media:8989/)
[Bazarr](http://media:6767)
[qBittorent](http://media:6880/)
[AutomaticRippingMachine](http://192.168.0.10:8088)

| https://stream.lolandbraa.no/   |                    |     |
| ------------------------------- | ------------------ | --- |
| https://prowlarr.lolbraa.no/    | media:9696         |     |
| https://qbit.lolbraa.no/        | media:6880         |     |
| https://bazarr.lolbraa.no/      | media:6767         |     |
| https://sonarr.lolbraa.no/      | media:8989         |     |
| https://radarr.lolbraa.no/      | media:7878         |     |
|                                 |                    |     |
| https://yt.lolbraa.no/          | 100.94.243.41:3000 |     |
| https://jdownloader.lolbraa.no/ | 100.94.243.41:5800 |     |

```
--net=container:media-ts
```


# Jellyfin
[Package qbittorrent · GitHub](https://github.com/orgs/linuxserver/packages/container/package/qbittorrent)
[List of known Jellyfin Plugin Repos – 2023 Update](https://www.reddit.com/r/jellyfin/comments/13naewh/list_of_known_jellyfin_plugin_repos_2023_update/)
## Hardwaretranscoding
Se [[Hardwaretranscoding#Jellyfin]]

## Tyzen OS
[GitHub - Georift/install-jellyfin-tizen: Install Jellyfin on your Samsung TV](https://github.com/Georift/install-jellyfin-tizen)
```
docker run --rm georift/install-jellyfin-tizen 192.168.1.147 Jellyfin-TrueHD
```


# Arrs
[TRaSH Guides](https://trash-guides.info)
[Servarr | Servarr Wiki](https://wiki.servarr.com)
## API
Prowlarr: 686d5cc04b724fbeb5dda3631902dc9a
Radarr: 458ac70109d14b24b0b882b3ffe82492
Sonarr: e404f9ca631e41d69d7c07dcdfd730a7


# qBittorent
[IP/DNS Detect - What is your IP, what is your DNS, what informations you send to websites.](https://ipleak.net/)

# Folder structure
Adoptert fra [unRAID - TRaSH Guides](https://trash-guides.info/Hardlinks/How-to-setup-for/Unraid/#folder-structure)
```
data (hostpath: /mnt/user/mediashare/)
├── torrents
│   ├── books
│   ├── movies
│   ├── music
│   └── tv
└── media
    ├── audiobooks
    ├── movies
    ├── music
    └── tv
```


# Ripping
## Automatic Ripping Machine
[From Disc to Drive:  A Beginner's Guide to Preparing Your Media for Jellyfin](https://forum.jellyfin.org/t-from-disc-to-drive-a-beginner-s-guide-to-preparing-your-media-for-jellyfin)
OMDBAPI http://www.omdbapi.com/?apikey=40622655&

## Manuell workflow
På krisstasjonerpop: MakeMKV og Handbrake via flatpacks.
Key: [MakeMKV Beta Key](https://cable.ayra.ch/makemkv/)


### Liste over titler
```
Cars (2006) [imdbid-tt0317219] - [Bluray-1080p][AAC 5.1][x265][Norwegian]-Ripped
Cars 2 (2011) [imdbid-tt1216475] - [Bluray-1080p][AAC 5.1][x265][Norwegian]-Ripped
Ratatouille (2007) [imdbid-tt0382932] - [Bluray-1080p][AAC 5.1][x265][Norwegian]-Ripped
WALL·E (2008) [imdbid-tt0910970] - [Bluray-1080p][AAC 5.1][x265][Norwegian]-Ripped
Lady and the Tramp (1955) [imdbid-tt0048280] - [Bluray-1080p][AAC 5.1][x265][Norwegian]-Ripped
How to train your dragon [Bluray-1080p][AAC 5.1][x265][Norwegian]-Ripped
Up (2009) [imdbid-tt1049413] - [Bluray-1080p][AAC 5.1][x265][Norwegian]-Ripped
Ice Age (2002) [imdbid-tt0268380] - [x265][Norwegian]-Ripped
PostmanPat og Sjørøverne - [DVD-576p][x265].mkv
Pippi Langstrømpe på Skolebenken - [DVD-576p][x265].mkv
Toy Story 2 (1999) [imdbid-tt0120363] - [Bluray-1080p][AAC 5.1][x265][Norwegian]-Ripped
Toy Story 3 (2010) [imdbid-tt0435761] - [Bluray-1080p][AAC 5.1][x265][Norwegian]-Ripped
Madagascar Escape 2 Africa (2008) - [Bluray-1080p][AAC 5.1][x265][Norwegian]-Ripped
Madagascar 3 Europes Most Wanted (2012) [imdbid-tt1277953] - [Bluray-1080p][AAC 5.1][x265][Norwegian]-Ripped
Tigergutt og Brumm: Supersnusernes Skattejakt vol1 - [DVD-576p][x265].mkv
```

### Handbrake
- [Codec Support | Jellyfin](https://jellyfin.org/docs/general/clients/codec-support/)
- [Convert BLURAY to H.265 HEVC with Handbrake Optimal Settings](https://www.thewebernets.com/2023/02/20/best-optimal-settings-convert-bluray-to-h-265-hevc-with-handbrake-1080-on-mac-windows-linux/)
- [Ischemia37 comments on \[deleted by user\]](https://old.reddit.com/r/handbrake/comments/1362na5/deleted_by_user/js8uy8n/)
- [HandBrake – H.265 NVEnc 1080p Ripping Chart and Guidelines – Ryan and Debi & Toren](https://www.ryananddebi.com/2020/10/04/handbrake-h-265-nvenc-1080p-ripping-chart-and-guidelines/)

#### Format
Audio
- AC3 eller AAC
- 5.1
Video
- H.265 10bit
- 

# AudioBookShelf
