
# WireGuard
## Klienter
- LolbraaNAS (endpoint: vpn.lolandbraa.no)
	- Tunnel wg0
		- Local tunnel pool: 10.253.132.0/24
	- Tunnel wg1
		- Local tunnel pool: 10.201.132.0/24
- LolbraaRPI
- BraaRPI på Tolvsrød (endpoint: braavpn.lolandbraa.no)
	- Tunnel 1: eth0

# Tailscale
Tailscale subnets
```
100.64.0.0/10
fd7a:115c:a1e0::/48
```
## Klienter
- LolbraaNAS
	- Andre klienter:
		- VPNVM
		- Homeassistant
		- Audio (audiobookshelf)
		- Media
- LolbraaKVM
- Lolbraa

[WireGuard AllowedIPs Calculator | Pro Custodibus](https://www.procustodibus.com/blog/2021/03/wireguard-allowedips-calculator/)
```
Allowed IPs: 0.0.0.0/0, ::0/0

Disallowed IPs: 100.64.0.0/10,fd7a:115c:a1e0::/48, 192.168.0.0/24

AllowedIPs = 0.0.0.0/2, 64.0.0.0/3, 96.0.0.0/6, 100.0.0.0/10, 100.128.0.0/9, 101.0.0.0/8, 102.0.0.0/7, 104.0.0.0/5, 112.0.0.0/4, 128.0.0.0/2, 192.0.0.0/9, 192.128.0.0/11, 192.160.0.0/13, 192.168.1.0/24, 192.168.2.0/23, 192.168.4.0/22, 192.168.8.0/21, 192.168.16.0/20, 192.168.32.0/19, 192.168.64.0/18, 192.168.128.0/17, 192.169.0.0/16, 192.170.0.0/15, 192.172.0.0/14, 192.176.0.0/12, 192.192.0.0/10, 193.0.0.0/8, 194.0.0.0/7, 196.0.0.0/6, 200.0.0.0/5, 208.0.0.0/4, 224.0.0.0/3, ::/1, 8000::/2, c000::/3, e000::/4, f000::/5, f800::/6, fc00::/8, fd00::/10, fd40::/11, fd60::/12, fd70::/13, fd78::/15, fd7a::/20, fd7a:1000::/24, fd7a:1100::/26, fd7a:1140::/28, fd7a:1150::/29, fd7a:1158::/30, fd7a:115c::/33, fd7a:115c:8000::/35, fd7a:115c:a000::/40, fd7a:115c:a100::/41, fd7a:115c:a180::/42, fd7a:115c:a1c0::/43, fd7a:115c:a1e1::/48, fd7a:115c:a1e2::/47, fd7a:115c:a1e4::/46, fd7a:115c:a1e8::/45, fd7a:115c:a1f0::/44, fd7a:115c:a200::/39, fd7a:115c:a400::/38, fd7a:115c:a800::/37, fd7a:115c:b000::/36, fd7a:115c:c000::/34, fd7a:115d::/32, fd7a:115e::/31, fd7a:1160::/27, fd7a:1180::/25, fd7a:1200::/23, fd7a:1400::/22, fd7a:1800::/21, fd7a:2000::/19, fd7a:4000::/18, fd7a:8000::/17, fd7b::/16, fd7c::/14, fd80::/9, fe00::/7
```


## Tailscale + Docker: 
Vilkårlig docker-container festet til Tailscale docker-klient

Deploy tailscale-docker med 
1. Extra parameters (advanced view): `--cap-add=NET_ADMIN --hostname=qbit`
2. UP_FLAGS: `--exit-node=100.97.139.107 --exit-node-allow-lan-access=true`
3. Start container og åpne loggen. Trykk på login-linken og autoriser container-instancen.

Deploy vilkårlig docker med:
1. Set the network type to ‘none’.
2. Extra parameters (advanced view): 
```
--net=container:vpnvm-monitoring-ts
--net=container:media-ts
--net=container:audio-ts
```
4. Fjern port-åpninger (dockeren fester seg til den andre dockeren som viderefører nettverk internt, så docker-driveren skal ikke ha noen åpne porter mot maskina/nettverket direkte!)
5. Test med 
```
curl ifconfig.io
```

Ref:[How to route any Docker container on Unraid through a VPN](https://unraid-guides.com/2021/05/19/how-to-route-any-docker-container-on-unraid-through-a-vpn/)

# Tailscale med VPN som exit-node
## VM-løsningen
[Reddit: Løsning med VM](https://www.reddit.com/r/Tailscale/comments/sjyc6k/route_exit_node_traffic_into_vpn/)

### 1. VM -> Surfshark (via WireGuard)
[How to Set Up WireGuard VPN Client on Ubuntu Desktop — tech.serhatteker.com](https://tech.serhatteker.com/post/2021-01/how-to-set-up-wireguard-client-on-ubuntu-desktop/)
```
# Keys generert av SurfShark
pubkey LTVkC0D9gA8Dd0XEVEDvclyts/XA6coVy
privkey SPvYUggyNSvN8x9kqGe8tGjaIrzo3Zh7dRDRom7ybGw=

# SurfShark-server info
Norway・Oslo
no-osl.prod.surfshark.com
146.70.103.251
pXfZi2vsdd88qrnqh+bwqHG4IYD42pj3T1wCm3PIGmw=


# Konfig i vpnvm
sudoedit /etc/wireguard/wg0.conf

# Andre kommandoer brukt
sudo wg-quick up wg0
sudo systemctl enable wg-quick@wg0
curl ifconfig.me

```

![[surfsharkvpnvm.conf]]
- *Error [/usr/bin/wg-quick: line 31: resolvconf: command not found \[WireGuard | Debian\] - Super User](https://superuser.com/questions/1500691/usr-bin-wg-quick-line-31-resolvconf-command-not-found-wireguard-debian)*
- ~~[How to Allow Local Network When Using WireGuard VPN Tunnel in Windows 10 - Tech Journey](https://techjourney.net/how-to-allow-local-network-when-using-wireguard-vpn-tunnel-in-windows-10/)~~ 
  ~~[WireGuard AllowedIPs Calculator](https://www.procustodibus.com/blog/2021/03/wireguard-allowedips-calculator/#a-better-alternative)~~
  ~~tatt i bruk for at klientene skal kunne nå intern trafikk (at ikke all trafikk i VM går inn Tailnet og ut Surfshark, men feks 192.168.0.10 når LolbraaNAS)~~~~~~
- [How to allow local IPs on Windows 10 client?](https://www.procustodibus.com/blog/2021/03/wireguard-allowedips-calculator/)

Kunne brukt [Surfshark Legacy client](https://support.surfshark.com/hc/en-us/articles/360017418334-How-to-set-up-Surfshark-VPN-on-Linux-Legacy-version) (ikke GUI)
### 2. Klient -> VM (via Tailnet)
[Exit Nodes (route all traffic) · Tailscale Docs](https://tailscale.com/kb/1103/exit-nodes)
- Alternatively, set `--exit-node-allow-lan-access` to true to allow direct access to your local network when traffic is routed via an exit node.

### 3. Routing
[How to change routing priority so that wireguard can coexist with tailscale](https://www.reddit.com/r/WireGuard/comments/n3nkk7/how_to_change_routing_priority_so_that_wireguard/)
> in the below tailscaled entry, for "After", you must use your specific wireguard instance (ex. [wg-quick@wg0.service](mailto:wg-quick@wg0.service)) rather than generic wireguard startup ([wg-quick@.service](mailto:wg-quick@.service)). It turns out tailscaled also calls wg-quick so it wouldn't work.

```
[Unit]
After = wg-quick@wg0.service.service

[Service]
ExecStartPost=/usr/bin/ip rule add pref 65 table 52
ExecStopPost=/usr/bin/ip rule del pref 65 table 52
```

Testing
[DNS leak test - Surfshark](https://surfshark.com/dns-leak-test)
[How too see traceroute info?](https://www.reddit.com/r/Tailscale/comments/17lqxr4/how_too_see_traceroute_info/)


## vpnvm-monitoring
1. Laget et custom docker-network "vpnvm-monitoring" basert på [HOW TO - Share services with a custom domain, no DDNS, using Tailscale](https://www.reddit.com/r/unRAID/comments/10xdx5g/how_to_share_services_with_a_custom_domain_no/) og [docker network create | Docker Docs](https://docs.docker.com/reference/cli/docker/network/create/).
	- 8e6cb7a8d2ced98dbf9eb2f2bea918c84a93d466f8bd6d09f38a3862bd3ed502
2. Run Tailscale-docker på vpnvm-monitoring
	- Data: ``/mnt/user/appdata/vpnvm-monitoring/ts``
	- Up-flags: ``--exit-node=100.97.139.107 --exit-node-allow-lan-access=true``
	- [Exit Nodes (route all traffic) · Tailscale Docs](https://tailscale.com/kb/1103/exit-nodes)
3. Speedtest-tracker
	- Data: `/mnt/user/appdata/vpnvm-monitoring/speedtest-tracker`
	- Extra Parameters field.: ``--net=container:vpnvm-monitoring-ts``
1. Smokeping
	- Data: `/mnt/user/appdata/vpnvm-monitoring/smokeping/data`
	- DB: `/mnt/user/appdata/vpnvm-monitoring/smokeping/db`



## Docker-løsningen
### Research
- Docker composes
	- [Github Note Chris: Tailscale for docker containers](https://github.com/ChrisLAS/notes/blob/master/Tailscale%20for%20Docker%20Containers.md)
	- https://rnorth.org/tailscale-docker/
- [Tailscale.com: Docker-Tailscale guide](https://tailscale.com/blog/docker-tailscale-guide)
- [Reddit: Tailscale sidecar docker?](https://www.reddit.com/r/unRAID/comments/1ar02ij/tailscale_sidecar_docker/)
- [# HOW TO - Share services using Tailscale via a public domain, with SSL enabled, no port forwarding required](https://www.reddit.com/r/unRAID/comments/192oag7/how_to_share_services_using_tailscale_via_a/)
- [# HOW TO - Share services with a custom domain, no DDNS, using Tailscale](https://www.reddit.com/r/unRAID/comments/10xdx5g/how_to_share_services_with_a_custom_domain_no/)
- [Integrert løsning med Mullvad](https://tailscale.com/mullvad)
	- Ganske dyr, 5EUR
- Spinne opp en docker med både Tailscale OG exit-node
	- [Gluetun](https://github.com/qdm12/gluetun)-docker attached til en Tailscale-docker?
### Et forsøk
[Specifying an exit node in a docker container results in "selected but offline" : r/Tailscale](https://www.reddit.com/r/Tailscale/comments/16fjx0e/specifying_an_exit_node_in_a_docker_container/)
https://tailscale.com/kb/1103/exit-nodes
https://github.com/hussainalhaddad/docker-templates/raw/master/tailscale/logo.png
```shell
echo 'net.ipv4.ip_forward = 1' | tee -a /etc/sysctl.d/99-tailscale.conf
echo 'net.ipv6.conf.all.forwarding = 1' | tee -a /etc/sysctl.d/99-tailscale.conf
sysctl -p /etc/sysctl.d/99-tailscale.conf
```
```
iptables -A FORWARD --in-interface tailscale0 -j ACCEPT
iptables -A FORWARD --out-interface tailscale0 -j ACCEPT
iptables -t nat -A POSTROUTING --source 100.64.0.0/10 --out-interface wlan0 -j MASQUERADE
```

```bash
wget -q -O- http://ipecho.net/plain
```



