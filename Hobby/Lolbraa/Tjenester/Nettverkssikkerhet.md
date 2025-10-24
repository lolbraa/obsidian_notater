# Cloudflare
## Proxy
Alle DNS-records som ikke **må** lede direkte til WAN IP-addressen, blir proxied gjennom Cloudflare-sine servere. Altså det er Cloudflare sin IP som blir resolved. Det er for å skjule den ekte IP-addressen.

I praksis må noen tjenester få direkte IP. Det gjøres ved at [[Hobby/Lolbraa/Nettverksinfrastruktur#DDNS|DDNS-skriptet]] oppdaterer to records:
1. lolandbraa.no - som er proxied.
2. nas.lolandbraa.no - som ikke er proxied.
Tjenester som trenger direkte tilgang kan CNAMEs til nas.lolandbraa.no, mens alt annet blir som standard sendt til lolandbraa.no (\*.lolandbraa.no).

### OBS: Limitations ved pakkestørrelse
Cloudflare har en grense (free tier) på 100MB-pakker som kan overføres over Cloudflare sine servere. Man kan derfor ikke ha på proxy eller bruke et annet produkt som Tunnel.
[Limits · Cloudflare Workers docs](https://developers.cloudflare.com/workers/platform/limits/#request-limits)

## WAF / brannmur
Cloudflare er navnetjener-hovedserver.
Alt går gjennom Cloudflare's WAF, en brannmur hvor:
1. bots blir blokkert.
2. alle utenom Europa blir blokkert.
3. alle utenom Norge får captcha.


## Access - OAuth
*Siden [1.113.0](https://github.com/immich-app/immich/releases/tag/v1.113.0) er OAuth redirect url for mobil endret, men det går ikke overens med Cloudflare Access (?). Noe galt skjer hvert fall, selv om Override URL er satt i Immich-config. Håer det fikses i en senere update, evt. må nedgradere*

Dette er originalt satt opp for Immich, derav navnene i 1pass og på Cloudflare, men dette burde kunne gjøres for alle tjenester?

*Immich kjører gjennom Cloudflare Tunnel på https://immich.lolandbraa.no. Cloudflare Tunnel er en docker.*
Immich brukere er definert av epost-addressen. Admin-brukeren kristoffer@lolandbraa.no kan derfor også logges inn med GitHub-OAuth hvor kristoffer@lolandbraa.no er mailadressen.
Det er kun godkjent med pålogginger fra Norge gjennom Google eller GitHub, og mailaddressene må være listet på [Cloudflare One: My Team > Lists > Godkjente mailadresser](https://one.dash.cloudflare.com/f37e9597c6af23e99998705333941408/team/lists/c22861b7-b4b2-4cba-8d2c-c6960ad35275). Se [[Cloudflare Access regler.jpg]].

### Godkjente mailadresser liste

| User email                | Description    | Created                 |
| ------------------------- | -------------- | ----------------------- |
| martinandrebraa@gmail.com |                | Aug 3, 2024 • 5:06 PM   |
| elloland@outlook.com      | Ellen og Roar  | Jul 19, 2024 • 10:10 AM |
| karoline081998@gmail.com  |                | Aug 3, 2024 • 5:36 PM   |
| nora@lolandbraa.no        |                | Jul 19, 2024 • 10:20 AM |
| ingerhbraa@gmail.com      |                | Jul 19, 2024 • 10:20 AM |
| stigsbraa@gmail.com       |                | Jul 19, 2024 • 10:20 AM |
| noraloland@outlook.com    |                | Jul 19, 2024 • 10:20 AM |
| kristoffer@lolandbraa.no  |                | Jul 9, 2024 • 3:43 PM   |
| krissernbraa@hotmail.com  |                | Jul 9, 2024 • 3:43 PM   |
| krissernbraa@gmail.com    |                | Jul 9, 2024 • 3:43 PM   |
| ingridloland@outlook.com  |                | Jul 22, 2024 • 1:49 PM  |
| ingridloland0@gmail.com   | google-kontoen | Jul 22, 2024 • 1:57 PM  |
| lise.braa@gmail.com       |                | Jul 21, 2024 • 2:44 PM  |
| geirbraa@gmail.com        |                | 28.12.2024              |
### Research
Google https://developers.cloudflare.com/cloudflare-one/identity/idp-integration/google/
Immich https://github.com/immich-app/immich/discussions/categories/community-guides?discussions_q=cloudflare+tunnels+category%3A%22Community+Guides%22 og docs https://immich.app/docs/administration/oauth/#prerequisites. Og fiks for mobil [\[Guide\] Cloudflare Tunnels with SSO/OAuth working for immich · immich-app/immich · Discussion #8299 · GitHub](https://github.com/immich-app/immich/discussions/8299#discussioncomment-9992390)



## Tunnel 
En løsning som fungerer som en VPN + reverse proxy ved at Cloudflare sine servere er reverse proxy som kommuniserer med endepunktet gjennom en VPN (feks en Cloudflare Tunnel-docker).
Immich https://github.com/ppr88/immich-guides/blob/main/open-immich-custom-domain.md


---

# Nginx Proxy Manager (NPM)
## Access Lists - dobbeltsikring
Det er to Access Lists:
1. `passord` - enkelt passord for å øke sikkerhet (lite brukt)
2. `lolbraa.no (lokal og tailscale)` - tillater kun det lokale subnettet (192.168.0.0/24) og tailnettet (100.64.0.0/10). Burde brukes på alle lolbraa.no-domener.

## Crowdsec - brute-forcing og IP-reputation
- Fulgt denne mest [Setup Crowdsec with Nginx Proxy Manager - Part 1 - YouTube](https://www.youtube.com/watch?v=qnviPAMwAuw)
  https://raw.githubusercontent.com/geek2gether/random_files/main/crowdsec-nginx-proxy-manager.yml
- [Protect Your Websites with CrowdSec and Nginx Proxy Manager](https://www.crowdsec.net/blog/crowdsec-with-nginx-proxy-manager)
- [Setup Crowdsec with Nginx Proxy Manager - Part 2 (Multi-server setup) - YouTube](https://www.youtube.com/watch?v=8bQh88z3FuY)
- [Unraid | CrowdSec](https://docs.ibracorp.io/crowdsec/crowdsec/unraid)

1. Gikk fra standard Nginx-Proxy-Manager-Official-template på Unraid Appstore til NginxProxyManager-CrowdSec, og bare kopierte over all dataen 
```
fra /mnt/user/appdata/Nginx-Proxy-Manager-Official/data
	og /mnt/user/appdata/Nginx-Proxy-Manager-Official/letsencrypt
til /mnt/user/appdata/NginxProxyManager-CrowdSec
```
2. Endret så portene på ny template slik at de erstattet gamle
3. og måtte bare gå gjennom hver eneste proxy-host i WebUIen for at den skulle reloade config-filen. Fra loggen:
```
[app         ] [8/3/2024] [11:25:47 PM] [Global   ] › ⬤  debug     CMD: /usr/sbin/nginx -t 
[app         ] [8/3/2024] [11:25:47 PM] [Nginx    ] › ⬤  debug     Deleting file: /data/nginx/proxy_host/5.conf
[app         ] [8/3/2024] [11:25:47 PM] [Global   ] › ⬤  debug     CMD: /usr/sbin/nginx -t 
[app         ] [8/3/2024] [11:25:47 PM] [Global   ] › ⬤  debug     CMD: /usr/sbin/nginx -t 
[app         ] [8/3/2024] [11:25:47 PM] [Nginx    ] › ℹ  info      Reloading Nginx
[app         ] [8/3/2024] [11:25:47 PM] [Global   ] › ⬤  debug     CMD: /usr/sbin/nginx -s reload
```
4. Installere agents? Konfigurere collections?

### Research
[Fail2Ban vs Crowdsec](https://www.reddit.com/r/selfhosted/comments/sesz1b/should_i_replace_fail2ban_with_crowdsec/)

Fail2Ban
- Mye konfigurering, men alle komponenter i ett
[Configuring Fail2ban with Nginx Proxy Manager (NPM)](https://blog.lrvt.de/fail2ban-with-nginx-proxy-manager/)

Crowdsec
- En spiritual successor til Fail2Ban ved at alle angrep blir delt med hverandre
- Flere komponenter, men skal være greit å konfigurere
- Må endre NPM-logging?
	- [CrowdSec Console](https://app.crowdsec.net/hub/author/crowdsecurity/collections/nginx-proxy-manager)




---


# DNS
Test av adblock/analytics-block [Test Ad Block - Toolz](https://d3ward.github.io/toolz/adblock).

Bruker pihole som sinkhole med følgende blacklists
```
https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts	
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/NorwegianExperimentalList%20alternate%20versions/NordicFiltersPiHole.txt	
https://raw.githubusercontent.com/ZingyAwesome/easylists-for-pihole/master/easyprivacy.txt	
https://easylist.to/easylist/easyprivacy.txt	
https://easylist.to/easylist/fanboy-social.txt	
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/NorwegianList.txt	
https://secure.fanboy.co.nz/fanboy-annoyance.txt	
https://secure.fanboy.co.nz/fanboy-cookiemonster.txt	
https://easylist.to/easylist/easylist.txt	
https://raw.githubusercontent.com/d3ward/toolz/master/src/d3host.txt
```

Pihole er satt som global nameserver i tailscale med override local dns. Da skal forhåpentligvis alle klienter bruke pihole.

Test på linux (POP) med resolvectl om hvilken DNS-server som betjener forespørsel
```sh
kristoffer@krisslaptoppop:~$ resolvectl query lolandbraa.no
lolandbraa.no: 104.21.65.103                   -- link: tailscale0
               172.67.161.150                  -- link: tailscale0
               2606:4700:3035::6815:4167       -- link: tailscale0
               2606:4700:3031::ac43:a196       -- link: tailscale0

-- Information acquired via protocol DNS in 807us.
-- Data is authenticated: no; Data was acquired via local or encrypted transport: no
-- Data from: cache
kristoffer@krisslaptoppop:~$ resolvectl query vg.no
vg.no: 195.88.55.16                            -- link: tailscale0
       195.88.54.16                            -- link: tailscale0
       2001:67c:21e0::16                       -- link: tailscale0

-- Information acquired via protocol DNS in 36.2ms.
-- Data is authenticated: no; Data was acquired via local or encrypted transport: no
-- Data from: network
kristoffer@krisslaptoppop:~$ resolvectl query adtago.s3.amazonaws.com
adtago.s3.amazonaws.com: ::                    -- link: tailscale0
                         0.0.0.0               -- link: tailscale0

-- Information acquired via protocol DNS in 23.1ms.
-- Data is authenticated: no; Data was acquired via local or encrypted transport: no
-- Data from: network
kristoffer@krisslaptoppop:~$ resolvectl query adtago.s3.amazonaws.com^C
kristoffer@krisslaptoppop:~$ resolvectl query stats.g.doubleclick.net
stats.g.doubleclick.net: ::                    -- link: tailscale0
                         0.0.0.0               -- link: tailscale0

-- Information acquired via protocol DNS in 133.7ms.
-- Data is authenticated: no; Data was acquired via local or encrypted transport: no
-- Data from: network
kristoffer@krisslaptoppop:~$ resolvectl query identify.hotjar.com
identify.hotjar.com: 0.0.0.0                   -- link: tailscale0
                     ::                        -- link: tailscale0

-- Information acquired via protocol DNS in 77.5ms.
-- Data is authenticated: no; Data was acquired via local or encrypted transport: no
-- Data from: network

```

Skrudde på accept-dns for sikkerhets skyld
```sh
kristoffer@krisslaptoppop:~$ tailscale set --accept-dns
kristoffer@krisslaptoppop:~$ resolvectl query click.googleanalytics.com
click.googleanalytics.com: 0.0.0.0             -- link: tailscale0
                           ::                  -- link: tailscale0

-- Information acquired via protocol DNS in 24.0ms.
-- Data is authenticated: no; Data was acquired via local or encrypted transport: no
-- Data from: network
kristoffer@krisslaptoppop:~$ resolvectl query myprint.hvl.no
myprint.hvl.no: 158.37.32.46                   -- link: wlp0s20f3

-- Information acquired via protocol DNS in 78.4ms.
-- Data is authenticated: no; Data was acquired via local or encrypted transport: no
-- Data from: network
kristoffer@krisslaptoppop:
```