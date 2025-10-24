
[[Workshop Troubleshooting HDD]]
[[#Datarecovery Stigs eksterne harddisk Ødelagt partisjon]]

# Unraidtroubles

## *For restarting av maskinen bruk*
1. *CTRL + ALT + DELETE*
   *Er vel en custom kommando i Unraid som forsøker en graceful shutdown hvor den samler inn diagnostikk!*
*Se [[Linux Kommandoer#Førstehjelp]]*
2. *Force-restart gjennom shortcut i Linux-kernelen [[Linux Kommandoer#REISUB - low level key]]* 
	1. *Forsøke kun RE ?*

## *Unraid-kommandoer*
*Se [[Unraid Kommandoer]]*
```
mover stop
```



---

## USB spam

> [!NOTE]-
> ```log
> Jun  7 12:48:29 LolbraaNAS kernel: usb usb3-port2: attempt power cycle
> Jun  7 12:48:29 LolbraaNAS kernel: usb 3-2: new high-speed USB device number 49 using xhci_hcd
> Jun  7 12:48:35 LolbraaNAS kernel: xhci_hcd 0000:00:14.0: Timeout while waiting for setup device command
> Jun  7 12:48:40 LolbraaNAS kernel: xhci_hcd 0000:00:14.0: Timeout while waiting for setup device command
> Jun  7 12:48:40 LolbraaNAS kernel: usb 3-2: device not accepting address 49, error -62
> Jun  7 12:48:40 LolbraaNAS kernel: usb 3-2: new high-speed USB device number 50 using xhci_hcd
> Jun  7 12:48:46 LolbraaNAS kernel: xhci_hcd 0000:00:14.0: Timeout while waiting for setup device command
> Jun  7 12:48:51 LolbraaNAS kernel: xhci_hcd 0000:00:14.0: Timeout while waiting for setup device command
> Jun  7 12:48:52 LolbraaNAS kernel: usb 3-2: device not accepting address 50, error -62
> Jun  7 12:48:52 LolbraaNAS kernel: usb usb3-port2: unable to enumerate USB device
> Jun  7 12:48:52 LolbraaNAS kernel: xhci_hcd 0000:07:00.0: xHC error in resume, USBSTS 0x401, Reinit
> Jun  7 12:48:52 LolbraaNAS kernel: usb usb5: root hub lost power or was reset
> Jun  7 12:48:52 LolbraaNAS kernel: usb usb6: root hub lost power or was reset
> Jun  7 12:48:52 LolbraaNAS kernel: usb 3-2: new high-speed USB device number 51 using xhci_hcd
> Jun  7 12:48:58 LolbraaNAS kernel: usb 3-2: device descriptor read/64, error -110
> Jun  7 12:49:14 LolbraaNAS kernel: usb 3-2: device descriptor read/64, error -110
> Jun  7 12:49:14 LolbraaNAS kernel: usb 3-2: new high-speed USB device number 52 using xhci_hcd
> Jun  7 12:49:19 LolbraaNAS kernel: usb 3-2: device descriptor read/64, error -110
> Jun  7 12:49:35 LolbraaNAS kernel: usb 3-2: device descriptor read/64, error -110
> Jun  7 12:49:35 LolbraaNAS kernel: usb usb3-port2: attempt power cycle
> Jun  7 12:49:36 LolbraaNAS kernel: usb 3-2: new high-speed USB device number 53 using xhci_hcd
> Jun  7 12:49:41 LolbraaNAS kernel: xhci_hcd 0000:00:14.0: Timeout while waiting for setup device command
> Jun  7 12:49:46 LolbraaNAS kernel: xhci_hcd 0000:00:14.0: Timeout while waiting for setup device command
> ```

Virker som det er USB koblingen til LolbraaKVM. Oppdaterte nylig, og det kom nylig.

## Spam av "traps: lsof ... general protection fault ip:..."
### Feilmeldinger:
Mange av disse
```log
Jan 17 20:42:59 LolbraaNAS kernel: traps: lsof[31825] general protection fault ip:151d3a241c6e sp:d3d60dc1a2a21a43 error:0 in libc-2.37.so[151d3a229000+169000]
```

### Fiks
[UNRaid kernel: traps: lsof\[28497\] general protection fault ip: - Page 3 - General Support - Unraid](https://forums.unraid.net/topic/100286-unraid-kernel-traps-lsof28497-general-protection-fault-ip/page/3/)
```
Hi all, just thought to chip in with my experience, I too had an error of this nature and turned out to be that I had a SMB mount via a tailscale tunnel which when that mount was not reachable I got this error. When unmounting the unreachable share the errors stopped. 
```
Skru av SMB-shares som IKKE er tilgjengelig.

## Out of memory
### Feiloppførsel:
- Går en gnag i blant out of memory. 

### Feilmeldinger:
Ulike feilmeldinger. Eks Syslog

> [!NOTE]- syslog
> ```SYSLOG
> Jan 17 13:30:31 LolbraaNAS kernel: sysrq: Manual OOM execution
> Jan 17 13:30:31 LolbraaNAS kernel: kworker/2:2 invoked oom-killer: gfp_mask=0xcc0(GFP_KERNEL), order=-1, oom_score_adj=0
> Jan 17 13:30:31 LolbraaNAS kernel: CPU: 2 PID: 8961 Comm: kworker/2:2 Tainted: P           O       6.1.106-Unraid #1
> Jan 17 13:30:31 LolbraaNAS kernel: Hardware name: System manufacturer System Product Name/P8Z77-V LK, BIOS 1402 03/21/2014
> Jan 17 13:30:31 LolbraaNAS kernel: Workqueue: events moom_callback
> Jan 17 13:30:31 LolbraaNAS kernel: Call Trace:
> Jan 17 13:30:31 LolbraaNAS kernel: \<TASK\>
> Jan 17 13:30:31 LolbraaNAS kernel: dump_stack_lvl+0x44/0x5c
> Jan 17 13:30:31 LolbraaNAS kernel: dump_header+0x4a/0x211
> Jan 17 13:30:31 LolbraaNAS kernel: oom_kill_process+0x80/0x111
> Jan 17 13:30:31 LolbraaNAS kernel: out_of_memory+0x3b3/0x3e5
> Jan 17 13:30:31 LolbraaNAS kernel: moom_callback+0x7c/0xb6
> Jan 17 13:30:31 LolbraaNAS kernel: process_one_work+0x1ab/0x295
> Jan 17 13:30:31 LolbraaNAS kernel: worker_thread+0x18b/0x244
> Jan 17 13:30:31 LolbraaNAS kernel: ? rescuer_thread+0x281/0x281
> Jan 17 13:30:31 LolbraaNAS kernel: kthread+0xe7/0xef
> Jan 17 13:30:31 LolbraaNAS kernel: ? kthread_complete_and_exit+0x1b/0x1b
> Jan 17 13:30:31 LolbraaNAS kernel: ret_from_fork+0x22/0x30
> Jan 17 13:30:31 LolbraaNAS kernel: \</TASK\>
> Jan 17 13:30:31 LolbraaNAS kernel: Mem-Info:
> Jan 17 13:30:31 LolbraaNAS kernel: active_anon:1350124 inactive_anon:5310043 isolated_anon:0
> Jan 17 13:30:31 LolbraaNAS kernel: active_file:4190 inactive_file:20533 isolated_file:48
> Jan 17 13:30:31 LolbraaNAS kernel: unevictable:397488 dirty:658 writeback:0
> Jan 17 13:30:31 LolbraaNAS kernel: slab_reclaimable:255744 slab_unreclaimable:640692
> Jan 17 13:30:31 LolbraaNAS kernel: mapped:436437 shmem:1463631 pagetables:33495
> Jan 17 13:30:31 LolbraaNAS kernel: sec_pagetables:554 bounce:0
> Jan 17 13:30:31 LolbraaNAS kernel: kernel_misc_reclaimable:0
> Jan 17 13:30:31 LolbraaNAS kernel: free:69030 free_pcp:661 free_cma:0
> Jan 17 13:30:31 LolbraaNAS kernel: Node 0 active_anon:5400496kB inactive_anon:21240172kB active_file:16760kB inactive_file:82132kB unevictable:1589952kB isolated(anon):0kB isolated(file):192kB mapped:1745748kB dirty:2632kB writeback:0kB shmem:5854524kB shmem_thp: 0kB shmem_pmdmapped: 0kB anon_thp: 2062336kB writeback_tmp:0kB kernel_stack:35984kB pagetables:133980kB sec_pagetables:2216kB all_unreclaimable? no
> Jan 17 13:30:31 LolbraaNAS kernel: Node 0 DMA free:15360kB boost:0kB min:28kB low:40kB high:52kB reserved_highatomic:0KB active_anon:0kB inactive_anon:0kB active_file:0kB inactive_file:0kB unevictable:0kB writepending:0kB present:15984kB managed:15360kB mlocked:0kB bounce:0kB free_pcp:0kB local_pcp:0kB free_cma:0kB
> Jan 17 13:30:31 LolbraaNAS kernel: lowmem_reserve[]: 0 3403 32009 32009 32009
> Jan 17 13:30:31 LolbraaNAS kernel: Node 0 DMA32 free:122208kB boost:0kB min:7180kB low:10664kB high:14148kB reserved_highatomic:0KB active_anon:268992kB inactive_anon:2749848kB active_file:1048kB inactive_file:11028kB unevictable:220168kB writepending:1012kB present:3609712kB managed:3519568kB mlocked:220168kB bounce:0kB free_pcp:812kB local_pcp:308kB free_cma:0kB
> Jan 17 13:30:31 LolbraaNAS kernel: lowmem_reserve[]: 0 0 28606 28606 28606
> Jan 17 13:30:31 LolbraaNAS kernel: Node 0 Normal free:138552kB boost:0kB min:60368kB low:89660kB high:118952kB reserved_highatomic:0KB active_anon:5131504kB inactive_anon:18490104kB active_file:13548kB inactive_file:71516kB unevictable:1369784kB writepending:1592kB present:29868032kB managed:29292684kB mlocked:1369784kB bounce:0kB free_pcp:1832kB local_pcp:204kB free_cma:0kB
> Jan 17 13:30:31 LolbraaNAS kernel: lowmem_reserve[]: 0 0 0 0 0
> Jan 17 13:30:31 LolbraaNAS kernel: Node 0 DMA: 0*4kB 0*8kB 0*16kB 0*32kB 0*64kB 0*128kB 0*256kB 0*512kB 1*1024kB (U) 1*2048kB (M) 3*4096kB (M) = 15360kB
> Jan 17 13:30:31 LolbraaNAS kernel: Node 0 DMA32: 15*4kB (E) 304*8kB (UME) 772*16kB (UME) 598*32kB (UME) 416*64kB (UME) 258*128kB (UME) 72*256kB (UM) 18*512kB (UM) 0*1024kB 0*2048kB 0*4096kB = 121276kB
> Jan 17 13:30:31 LolbraaNAS kernel: Node 0 Normal: 4610*4kB (UME) 3311*8kB (UME) 2353*16kB (UME) 1747*32kB (UE) 0*64kB 0*128kB 0*256kB 0*512kB 0*1024kB 0*2048kB 0*4096kB = 138480kB
> Jan 17 13:30:31 LolbraaNAS kernel: Node 0 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=2048kB
> Jan 17 13:30:31 LolbraaNAS kernel: 1530149 total pagecache pages
> Jan 17 13:30:31 LolbraaNAS kernel: 0 pages in swap cache
> Jan 17 13:30:31 LolbraaNAS kernel: Free swap  = 0kB
> Jan 17 13:30:31 LolbraaNAS kernel: Total swap = 0kB
> Jan 17 13:30:31 LolbraaNAS kernel: 8373432 pages RAM
> Jan 17 13:30:31 LolbraaNAS kernel: 0 pages HighMem/MovableOnly
> Jan 17 13:30:31 LolbraaNAS kernel: 166529 pages reserved
> Jan 17 13:30:31 LolbraaNAS kernel: 0 pages cma reserved
> Jan 17 13:30:31 LolbraaNAS kernel: Tasks state (memory values in pages):
> Jan 17 13:30:31 LolbraaNAS kernel: [  pid  ]   uid  tgid total_vm      rss pgtables_bytes swapents oom_score_adj name
> Jan 17 13:30:31 LolbraaNAS kernel: [    825]     0   825     4707     1018    57344        0         -1000 udevd
> Jan 17 13:30:31 LolbraaNAS kernel: [   1378]    81  1378     1295      538    45056        0             0 dbus-daemon
> Jan 17 13:30:31 LolbraaNAS kernel: [   1389]     0  1389     1605      798    45056        0             0 elogind-daemon
> Jan 17 13:30:31 LolbraaNAS kernel: [   1527]    44  1527    18665      786    61440        0             0 ntpd
> Jan 17 13:30:31 LolbraaNAS kernel: [   1534]     0  1534      650      429    40960        0             0 acpid
> Jan 17 13:30:31 LolbraaNAS kernel: [   1552]     0  1552      643      461    49152        0             0 crond
> Jan 17 13:30:31 LolbraaNAS kernel: [   1556]     0  1556      664      351    40960        0             0 atd
> Jan 17 13:30:31 LolbraaNAS kernel: [   1767]     0  1767     1013      679    40960        0             0 upnp_poller
> Jan 17 13:30:31 LolbraaNAS kernel: [   1852]     0  1852      800       38    40960        0             0 mcelog
> Jan 17 13:30:31 LolbraaNAS kernel: [   2062]     0  2062     1004      641    40960        0             0 monitor_nchan
> Jan 17 13:30:31 LolbraaNAS kernel: [   7740]     0  7740     1283      796    45056        0             0 atd
> Jan 17 13:30:31 LolbraaNAS kernel: [   7743]     0  7743      996      742    45056        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [   7745]     0  7745     1115      746    45056        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [   7747]     0  7747      693      229    40960        0             0 inotifywait
> Jan 17 13:30:31 LolbraaNAS kernel: [  12800]     0 12800      652      225    40960        0             0 agetty
> Jan 17 13:30:31 LolbraaNAS kernel: [  12801]     0 12801      652      229    40960        0             0 agetty
> Jan 17 13:30:31 LolbraaNAS kernel: [  12802]     0 12802      652      219    40960        0             0 agetty
> Jan 17 13:30:31 LolbraaNAS kernel: [  12803]     0 12803      652      232    40960        0             0 agetty
> Jan 17 13:30:31 LolbraaNAS kernel: [  12804]     0 12804      652      208    40960        0             0 agetty
> Jan 17 13:30:31 LolbraaNAS kernel: [  13137]     0 13137    37221     2532    81920        0             0 nginx
> Jan 17 13:30:31 LolbraaNAS kernel: [  13151]     0 13151     1081       58    45056        0             0 inetd
> Jan 17 13:30:31 LolbraaNAS kernel: [  13152]     0 13152    86310     1122    90112        0             0 emhttpd
> Jan 17 13:30:31 LolbraaNAS kernel: [  13489]     0 13489    23209     2116   159744        0             0 php-fpm
> Jan 17 13:30:31 LolbraaNAS kernel: [  13711]     0 13711     1303      918    40960        0             0 rc.flash_backup
> Jan 17 13:30:31 LolbraaNAS kernel: [  14427]     0 14427   446076    40662  1212416        0             0 tailscaled
> Jan 17 13:30:31 LolbraaNAS kernel: [  14428]     0 14428      846      389    45056        0             0 grep
> Jan 17 13:30:31 LolbraaNAS kernel: [  14429]     0 14429    23944     3516   167936        0             0 tailscale-watch
> Jan 17 13:30:31 LolbraaNAS kernel: [  18613]     0 18613    52217      724    65536        0             0 shfs
> Jan 17 13:30:31 LolbraaNAS kernel: [  18626]     0 18626   172473    13412   286720        0             0 shfs
> Jan 17 13:30:31 LolbraaNAS kernel: [  19327]     0 19327    91868     1496    98304        0             0 rsyslogd
> Jan 17 13:30:31 LolbraaNAS kernel: [  23105]     0 23105  1166923    39296  4075520        0             0 dockerd
> Jan 17 13:30:31 LolbraaNAS kernel: [  23157]     0 23157   189171     6975   253952        0             0 containerd
> Jan 17 13:30:31 LolbraaNAS kernel: [  25190]     0 25190     8110     1443   102400        0             0 virtlockd
> Jan 17 13:30:31 LolbraaNAS kernel: [  25216]     0 25216     8127     1516   102400        0             0 virtlogd
> Jan 17 13:30:31 LolbraaNAS kernel: [  25324]     0 25324   432547     4682   331776        0             0 libvirtd
> Jan 17 13:30:31 LolbraaNAS kernel: [  25452]    99 25452     1890      517    53248        0             0 dnsmasq
> Jan 17 13:30:31 LolbraaNAS kernel: [  25453]     0 25453     1857       83    53248        0             0 dnsmasq
> Jan 17 13:30:31 LolbraaNAS kernel: [   6751]     0  6751   177706     2093    81920        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   6757]     0  6757   177706     2100    81920        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   6771]     0  6771   177706     2095    81920        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   6779]     0  6779   177706     1586    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   6796]     0  6796   177706     2096    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   6801]     0  6801   177706     1590    73728        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   6820]     0  6820   177866     1960   106496        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   6828]     0  6828   177770     1586    73728        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   6850]     0  6850   180805     2572   126976        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [   6875]     0  6875      174       65    36864        0             0 cinit
> Jan 17 13:30:31 LolbraaNAS kernel: [   7359]     0  7359    33823     9598   147456        0             0 nginx
> Jan 17 13:30:31 LolbraaNAS kernel: [   7383]     0  7383    61142    11426  1724416        0             0 node
> Jan 17 13:30:31 LolbraaNAS kernel: [  15400]     0 15400   180677     2843   131072        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  15423]     0 15423     7924     4465   102400        0             0 python
> Jan 17 13:30:31 LolbraaNAS kernel: [  17399]     0 17399   180741     2434   126976        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  17421]     0 17421      407        5    36864        0             0 docker-entrypoi
> Jan 17 13:30:31 LolbraaNAS kernel: [  17455]     0 17455   411956    28072   978944        0             0 tailscaled
> Jan 17 13:30:31 LolbraaNAS kernel: [  19777]     0 19777      403        6    40960        0             0 sleep
> Jan 17 13:30:31 LolbraaNAS kernel: [  27167]     0 27167   180741     1926   122880        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  27191]   100 27191      262       11    24576        0             0 docker-init
> Jan 17 13:30:31 LolbraaNAS kernel: [  27582]   100 27582   282179    74356   753664        0             0 coolwsd
> Jan 17 13:30:31 LolbraaNAS kernel: [  27797]   100 27797   149146    44942  1044480        0             0 forkit
> Jan 17 13:30:31 LolbraaNAS kernel: [  27819]     0 27819   180677     2287   131072        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  27853]   999 27853      262       12    24576        0             0 docker-init
> Jan 17 13:30:31 LolbraaNAS kernel: [  27946]   999 27946      589       71    40960        0             0 start.sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  27963]   999 27963   103672    44098   458752        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  28008]   999 28008   104026    37644   458752        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  28010]   999 28010   104014    37294   458752        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  28015]   999 28015   103681     2791   122880        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  28016]   999 28016   104980      983   172032        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  28017]   999 28017   104954      747   151552        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  28157]     0 28157   180741      976   131072        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  28182]   999 28182      262       10    24576        0             0 docker-init
> Jan 17 13:30:31 LolbraaNAS kernel: [  28235]   999 28235    11088     1079   110592        0             0 redis-server
> Jan 17 13:30:31 LolbraaNAS kernel: [  28608]     0 28608   180805     1064   131072        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  28637]  1000 28637      625      295    45056        0             0 tini
> Jan 17 13:30:31 LolbraaNAS kernel: [  28917]  1000 28917   635488    25769   438272        0             0 java
> Jan 17 13:30:31 LolbraaNAS kernel: [  29551]  1000 29551  1313491   495424  4612096        0             0 java
> Jan 17 13:30:31 LolbraaNAS kernel: [  29557]     0 29557   180741     1077   126976        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  29598] 65534 29598      262       12    24576        0             0 docker-init
> Jan 17 13:30:31 LolbraaNAS kernel: [  29967]  1000 29967    22627      731    86016        0             0 controller
> Jan 17 13:30:31 LolbraaNAS kernel: [  30287] 65534 30287      579       59    36864        0             0 start.sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  30305] 65534 30305   454704    67775  1400832        0             0 imaginary
> Jan 17 13:30:31 LolbraaNAS kernel: [  30720]     0 30720   180677     1091   126976        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  30748]     0 30748      262       11    24576        0             0 docker-init
> Jan 17 13:30:31 LolbraaNAS kernel: [  30833]     0 30833     7807     4427   106496        0             0 supervisord
> Jan 17 13:30:31 LolbraaNAS kernel: [  31068]     0 31068   180805     1035   131072        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  31115]    33 31115      262       10    24576        0             0 docker-init
> Jan 17 13:30:31 LolbraaNAS kernel: [  31214]    33 31214      581       65    40960        0             0 start.sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  31422]     0 31422   177930      537   102400        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  31477]     0 31477   180741      984   131072        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  31523]    33 31523      262       11    24576        0             0 docker-init
> Jan 17 13:30:31 LolbraaNAS kernel: [  31618]    33 31618     7792     4402    98304        0             0 supervisord
> Jan 17 13:30:31 LolbraaNAS kernel: [   4330]    33  4330      984      459    45056        0             0 cron.sh
> Jan 17 13:30:31 LolbraaNAS kernel: [   4331]    33  4331      374       23    40960        0             0 nc
> Jan 17 13:30:31 LolbraaNAS kernel: [   4332]     0  4332    98883     6708   270336        0             0 php-fpm
> Jan 17 13:30:31 LolbraaNAS kernel: [   4333]    33  4333      587       70    45056        0             0 run-exec-comman
> Jan 17 13:30:31 LolbraaNAS kernel: [   4474]    33  4474     6422      321    81920        0             0 notify_push
> Jan 17 13:30:31 LolbraaNAS kernel: [   5058]    33  5058      408        6    40960        0             0 apachectl
> Jan 17 13:30:31 LolbraaNAS kernel: [   5059]    33  5059   317067     5117   245760        0             0 caddy
> Jan 17 13:30:31 LolbraaNAS kernel: [   5061]    33  5061     1370      322    45056        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [   5083]    33  5083     5821     2620    90112        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [   5084]    33  5084     5268     2191    77824        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [   5086]    33  5086     6498     2475    98304        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [   5894]    33  5894     1634      133    45056        0             0 sleep
> Jan 17 13:30:31 LolbraaNAS kernel: [   7402]    33  7402     5826     2432    86016        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [  32649]   100 32649   149179    44959   782336        0             0 kit_spare_008
> Jan 17 13:30:31 LolbraaNAS kernel: [   4338]     0  4338   177770      133    81920        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   4347]     0  4347   177706      120    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   4388]     0  4388   180741     1522   126976        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [   4408]    99  4408   447980     4909   249856        0             0 signal-cli-rest
> Jan 17 13:30:31 LolbraaNAS kernel: [   2885]     0  2885     2181     1620    53248        0             0 tmux: server
> Jan 17 13:30:31 LolbraaNAS kernel: [   2886]     0  2886     3175     2286    61440        0             0 bash
> Jan 17 13:30:31 LolbraaNAS kernel: [  13368]     0 13368   177706     1024    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  13375]     0 13375   177706      631    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  13390]     0 13390   177930     1421    98304        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  13396]     0 13396   177706     1134    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  13411]     0 13411   177642     1541    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  13418]     0 13418   177706     1542    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  13433]     0 13433   177930     2067   114688        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  13439]     0 13439   177642     1530    73728        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  13488]     0 13488   180741     2248   131072        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  13526]     0 13526      109       14    24576        0             0 s6-svscan
> Jan 17 13:30:31 LolbraaNAS kernel: [  13818]     0 13818       55        6    24576        0             0 s6-supervise
> Jan 17 13:30:31 LolbraaNAS kernel: [  13822]     0 13822       52        1    24576        0             0 s6-linux-init-s
> Jan 17 13:30:31 LolbraaNAS kernel: [  13885]     0 13885       55        5    24576        0             0 s6-supervise
> Jan 17 13:30:31 LolbraaNAS kernel: [  13886]     0 13886       55        5    24576        0             0 s6-supervise
> Jan 17 13:30:31 LolbraaNAS kernel: [  13889]     0 13889       55        6    24576        0             0 s6-supervise
> Jan 17 13:30:31 LolbraaNAS kernel: [  13890]     0 13890       55        6    24576        0             0 s6-supervise
> Jan 17 13:30:31 LolbraaNAS kernel: [  13904]     0 13904       52        6    24576        0             0 s6-ipcserverd
> Jan 17 13:30:31 LolbraaNAS kernel: [  14192]    99 14192 68902047   427711  4513792        0             0 jellyfin
> Jan 17 13:30:31 LolbraaNAS kernel: [  14195]     0 14195     1835       65    53248        0             0 bash
> Jan 17 13:30:31 LolbraaNAS kernel: [  14214]     0 14214     1421       23    53248        0             0 sleep
> Jan 17 13:30:31 LolbraaNAS kernel: [  20209]     0 20209   177706     1131    81920        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  20222]     0 20222   177706      120    81920        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  20245]     0 20245   180677     1088   126976        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  20266]     0 20266      597       75    45056        0             0 start.sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  20724]     0 20724     7814     4418   102400        0             0 supervisord
> Jan 17 13:30:31 LolbraaNAS kernel: [  20767]     0 20767     2762      616    57344        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [  20768]     0 20768      591       72    40960        0             0 backup-time-fil
> Jan 17 13:30:31 LolbraaNAS kernel: [  20769]    33 20769   316939     2468   196608        0             0 caddy
> Jan 17 13:30:31 LolbraaNAS kernel: [  20772]     0 20772      592       74    45056        0             0 cron.sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  20778]    33 20778    17548     1069   110592        0             0 php
> Jan 17 13:30:31 LolbraaNAS kernel: [  20780]     0 20780    17538     1034   110592        0             0 php-fpm
> Jan 17 13:30:31 LolbraaNAS kernel: [  20781]     0 20781      591       72    45056        0             0 session-dedupli
> Jan 17 13:30:31 LolbraaNAS kernel: [  20783]     0 20783      586       68    40960        0             0 bash
> Jan 17 13:30:31 LolbraaNAS kernel: [  20883]    33 20883     4483      883    69632        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [  20884]    33 20884     3923      843    65536        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [  20890]    33 20890     3923      843    65536        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [  21082]    33 21082     3886      833    65536        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [   4693]   100  4693   149179    44959   782336        0             0 kit_spare_01c
> Jan 17 13:30:31 LolbraaNAS kernel: [  25822]     0 25822   177706      114    81920        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  25860]     0 25860   177706      120    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  26661]     0 26661   180741      999   126976        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  26718]     0 26718      536       15    36864        0             0 dumb-init
> Jan 17 13:30:31 LolbraaNAS kernel: [  27305]     0 27305  2858278    29664  3567616        0             0 node
> Jan 17 13:30:31 LolbraaNAS kernel: [  30821]     0 30821     9110     8814   110592        0             0 inotifywait
> Jan 17 13:30:31 LolbraaNAS kernel: [  30823]     0 30823     1004      628    40960        0             0 watcher
> Jan 17 13:30:31 LolbraaNAS kernel: [  30840]     0 30840      751      350    45056        0             0 inotifywait
> Jan 17 13:30:31 LolbraaNAS kernel: [  30841]     0 30841     1001       81    40960        0             0 watcher
> Jan 17 13:30:31 LolbraaNAS kernel: [  30847]     0 30847     3687     3375    65536        0             0 inotifywait
> Jan 17 13:30:31 LolbraaNAS kernel: [  30848]     0 30848     1005      617    40960        0             0 watcher
> Jan 17 13:30:31 LolbraaNAS kernel: [  22428]     0 22428     3175     2289    65536        0             0 bash
> Jan 17 13:30:31 LolbraaNAS kernel: [  23184]     0 23184     4043     1961    65536        0             0 mc
> Jan 17 13:30:31 LolbraaNAS kernel: [  23189]     0 23189     3185     2291    61440        0             0 bash
> Jan 17 13:30:31 LolbraaNAS kernel: [   1148]    33  1148     4053     1679    69632        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [   1289]    33  1289     4897     2077    73728        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [   1290]    33  1290     3275     1095    61440        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [   1563]    33  1563     2565      591    53248        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [   1657]    33  1657     2574      593    53248        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [   1658]    33  1658     2835      717    57344        0             0 httpd
> Jan 17 13:30:31 LolbraaNAS kernel: [  22845]   100 22845   149179    44959   782336        0             0 kit_spare_040
> Jan 17 13:30:31 LolbraaNAS kernel: [  18979]     0 18979      848      173    45056        0             0 mount.exfat
> Jan 17 13:30:31 LolbraaNAS kernel: [   1724]     0  1724   177770      120    81920        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   1732]     0  1732   177706      121    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [   1800]     0  1800   180741      872   131072        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [   1820]     0  1820   320349     6144   249856        0             0 beszel
> Jan 17 13:30:31 LolbraaNAS kernel: [  12119]     0 12119   180677      820   131072        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  12145]     0 12145   308138     1265   143360        0             0 agent
> Jan 17 13:30:31 LolbraaNAS kernel: [  11844]     0 11844   180741      932   122880        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  11883]     0 11883      212        9    40960        0             0 tini
> Jan 17 13:30:31 LolbraaNAS kernel: [  11903]   977 11903     4857     1164    73728        0             0 uwsgi
> Jan 17 13:30:31 LolbraaNAS kernel: [  12069]   977 12069    39717    22608   323584        0             0 bd23f1f1-1303-4
> Jan 17 13:30:31 LolbraaNAS kernel: [  12074]   977 12074    41455    23915   319488        0             0 b31d7374-e242-4
> Jan 17 13:30:31 LolbraaNAS kernel: [  12078]   977 12078    45302    27295   356352        0             0 26863c35-3e4b-4
> Jan 17 13:30:31 LolbraaNAS kernel: [  12080]   977 12080    45805    27812   356352        0             0 d1e5957e-b35d-4
> Jan 17 13:30:31 LolbraaNAS kernel: [  27576]     0 27576     2129      758    57344        0         -1000 sshd
> Jan 17 13:30:31 LolbraaNAS kernel: [  28594]   100 28594   149179    44959   782336        0             0 kit_spare_049
> Jan 17 13:30:31 LolbraaNAS kernel: [   1784]     0  1784   420011   287920  3301376        0             0 qemu-system-x86
> Jan 17 13:30:31 LolbraaNAS kernel: [  23526]     0 23526   180741      900   122880        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  23527]     0 23527   180805      921   122880        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  23603]   999 23603   160231     8329   229376        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  23628]   999 23628   739050   274198  5074944        0             0 redis-server
> Jan 17 13:30:31 LolbraaNAS kernel: [  23914]     0 23914   180741     1010   126976        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  23953]     0 23953   460275      492   188416        0             0 go-cron
> Jan 17 13:30:31 LolbraaNAS kernel: [  24076]   999 24076    19953      630   118784        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  24082]   999 24082   799315   154013  3706880        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  24091]   999 24091   160476   138495  1245184        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  24092]   999 24092   160267   137268  1236992        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  24093]   999 24093   160231     4811   172032        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  24094]   999 24094   160400      994   180224        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  24095]   999 24095    20061      721   118784        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  24097]   999 24097   160339      856   155648        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  28798]     0 28798   177930      627   106496        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  28814]     0 28814   177706      116    81920        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  28854]     0 28854   180805      923   131072        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  28858]     0 28858   180741      994   126976        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  28912]     0 28912      642       23    40960        0             0 tini
> Jan 17 13:30:31 LolbraaNAS kernel: [  28914]     0 28914      618       24    40960        0             0 tini
> Jan 17 13:30:31 LolbraaNAS kernel: [  29298]     0 29298      644       23    40960        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  29301]     0 29301  3646700    79866 12918784        0             0 immich
> Jan 17 13:30:31 LolbraaNAS kernel: [  29317]     0 29317    18678     8957   176128        0             0 gunicorn
> Jan 17 13:30:31 LolbraaNAS kernel: [    673]     0   673  2926171    33914  4231168        0             0 immich-api
> Jan 17 13:30:31 LolbraaNAS kernel: [   4386]   999  4386   160524     2553   176128        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [   6500]   999  6500   162141     5014   258048        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  16826]     0 16826    20005     1708   143360        0             0 smbd
> Jan 17 13:30:31 LolbraaNAS kernel: [  16848]     0 16848    19551     1212   139264        0             0 smbd-notifyd
> Jan 17 13:30:31 LolbraaNAS kernel: [  16849]     0 16849    19555     1083   135168        0             0 cleanupd
> Jan 17 13:30:31 LolbraaNAS kernel: [  16901]     0 16901      647      388    40960        0             0 wsdd2
> Jan 17 13:30:31 LolbraaNAS kernel: [  16958]     0 16958    19029     1434   122880        0             0 winbindd
> Jan 17 13:30:31 LolbraaNAS kernel: [  16990]     0 16990    19047     1588   122880        0             0 winbindd
> Jan 17 13:30:31 LolbraaNAS kernel: [  17420]    61 17420     1428      642    45056        0             0 avahi-daemon
> Jan 17 13:30:31 LolbraaNAS kernel: [  17426]    61 17426     1329       67    45056        0             0 avahi-daemon
> Jan 17 13:30:31 LolbraaNAS kernel: [  17439]     0 17439      669       31    40960        0             0 avahi-dnsconfd
> Jan 17 13:30:31 LolbraaNAS kernel: [  24005]     0 24005    19232     1313   126976        0             0 winbindd
> Jan 17 13:30:31 LolbraaNAS kernel: [  18220]     0 18220   177770      195    86016        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  18255]     0 18255   177706      120    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  18295]     0 18295   177770      121    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  18303]     0 18303   177706      116    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  18542]     0 18542   180805      852   131072        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  18543]     0 18543   180741      911   122880        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  18585]     0 18585      981       73    45056        0             0 run.sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  18591]     0 18591      583       64    45056        0             0 bash
> Jan 17 13:30:31 LolbraaNAS kernel: [  18907]     0 18907   314312     3139   188416        0             0 duplicacy_web
> Jan 17 13:30:31 LolbraaNAS kernel: [  18930]     0 18930      407       14    40960        0             0 tail
> Jan 17 13:30:31 LolbraaNAS kernel: [  19779]     0 19779   180741     1025   122880        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  19826]     0 19826      110       15    28672        0             0 s6-svscan
> Jan 17 13:30:31 LolbraaNAS kernel: [  19977]     0 19977       55        5    24576        0             0 s6-supervise
> Jan 17 13:30:31 LolbraaNAS kernel: [  19978]     0 19978       55        6    28672        0             0 s6-supervise
> Jan 17 13:30:31 LolbraaNAS kernel: [  19979]     0 19979       52        1    24576        0             0 s6-linux-init-s
> Jan 17 13:30:31 LolbraaNAS kernel: [  19980]     0 19980       74       10    36864        0             0 s6-log
> Jan 17 13:30:31 LolbraaNAS kernel: [  19990]     0 19990       55        7    24576        0             0 s6-supervise
> Jan 17 13:30:31 LolbraaNAS kernel: [  19991]     0 19991       55        4    24576        0             0 s6-supervise
> Jan 17 13:30:31 LolbraaNAS kernel: [  19992]     0 19992       55        6    24576        0             0 s6-supervise
> Jan 17 13:30:31 LolbraaNAS kernel: [  20000]     0 20000       52        7    24576        0             0 s6-ipcserverd
> Jan 17 13:30:31 LolbraaNAS kernel: [  20036]     0 20036      407       13    36864        0             0 crond
> Jan 17 13:30:31 LolbraaNAS kernel: [  20624]     0 20624     3859      318    65536        0             0 sshd
> Jan 17 13:30:31 LolbraaNAS kernel: [  12824]     0 12824  2861773    43008  4370432        0             0 unraid-api
> Jan 17 13:30:31 LolbraaNAS kernel: [   3065]     0  3065   211660    38601   872448        0             0 gunicorn
> Jan 17 13:30:31 LolbraaNAS kernel: [   4711]     0  4711      994      738    40960        0             0 mover
> Jan 17 13:30:31 LolbraaNAS kernel: [   4725]     0  4725    23911     3044   163840        0             0 mover.php
> Jan 17 13:30:31 LolbraaNAS kernel: [   4737]     0  4737     1485     1089    49152        0             0 age_mover
> Jan 17 13:30:31 LolbraaNAS kernel: [   3659]   999  3659   197138   143268  1507328        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  21318]   999 21318   196880   142977  1503232        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  22326]   999 22326   199195   145290  1523712        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  20735]   999 20735   161640   140107  1269760        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  20737]   999 20737   196544   142591  1503232        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [  16458]     0 16458    33982     9144   143360        0             0 nginx
> Jan 17 13:30:31 LolbraaNAS kernel: [  16459]     0 16459    33982     7879   139264        0             0 nginx
> Jan 17 13:30:31 LolbraaNAS kernel: [  16461]     0 16461    33982     8667   143360        0             0 nginx
> Jan 17 13:30:31 LolbraaNAS kernel: [  16462]     0 16462    33956     9055   139264        0             0 nginx
> Jan 17 13:30:31 LolbraaNAS kernel: [  16464]     0 16464    33659     9385   143360        0             0 nginx
> Jan 17 13:30:31 LolbraaNAS kernel: [  22089]     0 22089      643      395    40960        0             0 move
> Jan 17 13:30:31 LolbraaNAS kernel: [  22090]     0 22090      997      745    45056        0             0 in_use
> Jan 17 13:30:31 LolbraaNAS kernel: [  22092]     0 22092      646      204    40960        0             0 fuser
> Jan 17 13:30:31 LolbraaNAS kernel: [  25027]     0 25027     1283      797    45056        0             0 atd
> Jan 17 13:30:31 LolbraaNAS kernel: [  25029]     0 25029      997      757    40960        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  25030]     0 25030    23911     2967   176128        0             0 startBackground
> Jan 17 13:30:31 LolbraaNAS kernel: [  25031]     0 25031      996      741    45056        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  25032]     0 25032     1033      786    40960        0             0 script
> Jan 17 13:30:31 LolbraaNAS kernel: [  25043]     0 25043      646      203    40960        0             0 fuser
> Jan 17 13:30:31 LolbraaNAS kernel: [  11685]     0 11685    37732     3689   102400        0             0 nginx
> Jan 17 13:30:31 LolbraaNAS kernel: [  12464]     0 12464     1283      797    45056        0             0 atd
> Jan 17 13:30:31 LolbraaNAS kernel: [  12473]     0 12473      997      757    45056        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  12475]     0 12475    23911     2965   172032        0             0 startBackground
> Jan 17 13:30:31 LolbraaNAS kernel: [  12476]     0 12476      996      729    40960        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  12477]     0 12477     1033      820    40960        0             0 script
> Jan 17 13:30:31 LolbraaNAS kernel: [  12494]     0 12494      646      227    40960        0             0 fuser
> Jan 17 13:30:31 LolbraaNAS kernel: [  12273]     0 12273   177706      113    81920        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  12278]     0 12278   177706      121    77824        0             0 docker-proxy
> Jan 17 13:30:31 LolbraaNAS kernel: [  12368]     0 12368   180677      793   122880        0             1 containerd-shim
> Jan 17 13:30:31 LolbraaNAS kernel: [  12401]  5050 12401     7378     4210   102400        0             0 gunicorn
> Jan 17 13:30:31 LolbraaNAS kernel: [  12626]     0 12626     2191       85    53248        0             0 master
> Jan 17 13:30:31 LolbraaNAS kernel: [  12628]   100 12628     2199       79    57344        0             0 qmgr
> Jan 17 13:30:31 LolbraaNAS kernel: [  13576]  5050 13576   137139   120803  1146880        0             0 gunicorn
> Jan 17 13:30:31 LolbraaNAS kernel: [  29152]     0 29152     1283      797    45056        0             0 atd
> Jan 17 13:30:31 LolbraaNAS kernel: [  29154]     0 29154      997      784    40960        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  29157]     0 29157    23911     3021   167936        0             0 startBackground
> Jan 17 13:30:31 LolbraaNAS kernel: [  29161]     0 29161      996      786    45056        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  29163]     0 29163     1033      830    40960        0             0 script
> Jan 17 13:30:31 LolbraaNAS kernel: [  29181]     0 29181      646      214    40960        0             0 fuser
> Jan 17 13:30:31 LolbraaNAS kernel: [  14104]     0 14104     1283      797    45056        0             0 atd
> Jan 17 13:30:31 LolbraaNAS kernel: [  14109]     0 14109      997      742    40960        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  14113]     0 14113    23911     3002   167936        0             0 startBackground
> Jan 17 13:30:31 LolbraaNAS kernel: [  14120]     0 14120      996      753    40960        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [  14122]     0 14122     1033      803    45056        0             0 script
> Jan 17 13:30:31 LolbraaNAS kernel: [  14150]     0 14150      646      230    40960        0             0 fuser
> Jan 17 13:30:31 LolbraaNAS kernel: [   5955]     0  5955      998      738    40960        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [   5959]     0  5959  2941203    20676  1052672        0             0 node
> Jan 17 13:30:31 LolbraaNAS kernel: [   6009]     0  6009 66062313  3043759 37187584        0             0 node
> Jan 17 13:30:31 LolbraaNAS kernel: [   6012]     0  6012  2954654    32872   856064        0             0 node
> Jan 17 13:30:31 LolbraaNAS kernel: [   6082]     0  6082  2890829    15039   786432        0             0 node
> Jan 17 13:30:31 LolbraaNAS kernel: [   6273]     0  6273   240822    11827   614400        0             0 node
> Jan 17 13:30:31 LolbraaNAS kernel: [   8279]     0  8279      993      745    40960        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [   8630]     0  8630    18028     1288   118784        0             0 samba-dcerpcd
> Jan 17 13:30:31 LolbraaNAS kernel: [   8713]     0  8713   313341     1385   163840        0             0 docker
> Jan 17 13:30:31 LolbraaNAS kernel: [   8714]     0  8714      472       20    40960        0             0 grep
> Jan 17 13:30:31 LolbraaNAS kernel: [   8788]     0  8788      994      746    40960        0             0 sh
> Jan 17 13:30:31 LolbraaNAS kernel: [   8810]     0  8810    16327      357    90112        0             0 monitor
> Jan 17 13:30:31 LolbraaNAS kernel: [   8818]     0  8818    16327      310    86016        0             0 startCustom.php
> Jan 17 13:30:31 LolbraaNAS kernel: [   8832]   100  8832     2187       77    53248        0             0 pickup
> Jan 17 13:30:31 LolbraaNAS kernel: [   8833]    33  8833     7890       44    69632        0             0 php
> Jan 17 13:30:31 LolbraaNAS kernel: [   8847]   999  8847   105077     1105   176128        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [   8911]   999  8911   160465     1280   167936        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [   8917]    33  8917     7890       44    73728        0             0 php
> Jan 17 13:30:31 LolbraaNAS kernel: [   8918]    33  8918     1634      119    49152        0             0 sleep
> Jan 17 13:30:31 LolbraaNAS kernel: [   8925]   999  8925   739084   274261  5070848        0             0 redis-server
> Jan 17 13:30:31 LolbraaNAS kernel: [   8947]   999  8947   104997     1070   172032        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [   8975]     0  8975     1494      530    49152        0             0 awk
> Jan 17 13:30:31 LolbraaNAS kernel: [   9020]   999  9020   160465     1299   167936        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [   9038]     0  9038     1476      263    45056        0             0 awk
> Jan 17 13:30:31 LolbraaNAS kernel: [   9070]     0  9070      652      235    40960        0             0 agetty
> Jan 17 13:30:31 LolbraaNAS kernel: [   9128]     0  9128      644      217    40960        0             0 sleep
> Jan 17 13:30:31 LolbraaNAS kernel: [   9138]   999  9138   103973      547    98304        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [   9155]     0  9155      591       72    45056        0             0 session-dedupli
> Jan 17 13:30:31 LolbraaNAS kernel: [   9160]     0  9160      644      227    40960        0             0 sleep
> Jan 17 13:30:31 LolbraaNAS kernel: [   9161]   999  9161   103672      432    77824        0             0 postgres
> Jan 17 13:30:31 LolbraaNAS kernel: [   9168]     0  9168     1013      495    40960        0             0 upnp_poller
> Jan 17 13:30:31 LolbraaNAS kernel: [   9169]     0  9169      646      224    40960        0             0 timeout
> Jan 17 13:30:31 LolbraaNAS kernel: [   9170]     0  9170      862      391    40960        0             0 grep
> Jan 17 13:30:31 LolbraaNAS kernel: [   9171]     0  9171      650      227    40960        0             0 tr
> Jan 17 13:30:31 LolbraaNAS kernel: [   9172]     0  9172      646      236    40960        0             0 stdbuf
> Jan 17 13:30:31 LolbraaNAS kernel: oom-kill:constraint=CONSTRAINT_NONE,nodemask=(null),cpuset=/,mems_allowed=0,global_oom,task_memcg=/c71,task=node,pid=6009,uid=0
> Jan 17 13:30:31 LolbraaNAS kernel: Out of memory: Killed process 6009 (node) total-vm:264249252kB, anon-rss:12123208kB, file-rss:0kB, shmem-rss:51828kB, UID:0 pgtables:36316kB oom_score_adj:0
> Jan 17 13:30:31 LolbraaNAS kernel: oom_reaper: reaped process 6009 (node), now anon-rss:0kB, file-rss:0kB, shmem-rss:0kB
> Jan 17 13:30:33 LolbraaNAS upnpc: Added port 51820/udp
> Jan 17 13:32:02 LolbraaNAS kernel: sysrq: Show Memory
> Jan 17 13:32:02 LolbraaNAS kernel: Mem-Info:
> Jan 17 13:32:02 LolbraaNAS kernel: active_anon:1350107 inactive_anon:2279917 isolated_anon:0
> Jan 17 13:32:02 LolbraaNAS kernel: active_file:180542 inactive_file:447763 isolated_file:0
> Jan 17 13:32:02 LolbraaNAS kernel: unevictable:397492 dirty:1326 writeback:0
> Jan 17 13:32:02 LolbraaNAS kernel: slab_reclaimable:255719 slab_unreclaimable:633388
> Jan 17 13:32:02 LolbraaNAS kernel: mapped:532302 shmem:1463542 pagetables:22750
> Jan 17 13:32:02 LolbraaNAS kernel: sec_pagetables:554 bounce:0
> Jan 17 13:32:02 LolbraaNAS kernel: kernel_misc_reclaimable:0
> Jan 17 13:32:02 LolbraaNAS kernel: free:2502088 free_pcp:6523 free_cma:0
> Jan 17 13:32:02 LolbraaNAS kernel: Node 0 active_anon:5400428kB inactive_anon:9119668kB active_file:722168kB inactive_file:1791052kB unevictable:1589968kB isolated(anon):0kB isolated(file):0kB mapped:2129208kB dirty:5304kB writeback:0kB shmem:5854168kB shmem_thp: 0kB shmem_pmdmapped: 0kB anon_thp: 2064384kB writeback_tmp:0kB kernel_stack:35296kB pagetables:91000kB sec_pagetables:2216kB all_unreclaimable? no
> Jan 17 13:32:02 LolbraaNAS kernel: Node 0 DMA free:15360kB boost:0kB min:28kB low:40kB high:52kB reserved_highatomic:0KB active_anon:0kB inactive_anon:0kB active_file:0kB inactive_file:0kB unevictable:0kB writepending:0kB present:15984kB managed:15360kB mlocked:0kB bounce:0kB free_pcp:0kB local_pcp:0kB free_cma:0kB
> Jan 17 13:32:02 LolbraaNAS kernel: lowmem_reserve[]: 0 3403 32009 32009 32009
> Jan 17 13:32:02 LolbraaNAS kernel: Node 0 DMA32 free:2146596kB boost:0kB min:7180kB low:10664kB high:14148kB reserved_highatomic:0KB active_anon:268980kB inactive_anon:724896kB active_file:2316kB inactive_file:10660kB unevictable:220168kB writepending:0kB present:3609712kB managed:3519568kB mlocked:220168kB bounce:0kB free_pcp:2716kB local_pcp:24kB free_cma:0kB
> Jan 17 13:32:02 LolbraaNAS kernel: lowmem_reserve[]: 0 0 28606 28606 28606
> Jan 17 13:32:02 LolbraaNAS kernel: Node 0 Normal free:7846396kB boost:0kB min:60368kB low:89660kB high:118952kB reserved_highatomic:0KB active_anon:5131448kB inactive_anon:8394772kB active_file:719852kB inactive_file:1780392kB unevictable:1369800kB writepending:5172kB present:29868032kB managed:29292684kB mlocked:1369800kB bounce:0kB free_pcp:23376kB local_pcp:2228kB free_cma:0kB
> Jan 17 13:32:02 LolbraaNAS kernel: lowmem_reserve[]: 0 0 0 0 0
> Jan 17 13:32:02 LolbraaNAS kernel: Node 0 DMA: 0*4kB 0*8kB 0*16kB 0*32kB 0*64kB 0*128kB 0*256kB 0*512kB 1*1024kB (U) 1*2048kB (M) 3*4096kB (M) = 15360kB
> Jan 17 13:32:02 LolbraaNAS kernel: Node 0 DMA32: 4605*4kB (UME) 3714*8kB (UME) 5964*16kB (UME) 5557*32kB (UME) 4131*64kB (UME) 3238*128kB (UME) 1948*256kB (UM) 849*512kB (UM) 208*1024kB (UM) 0*2048kB 0*4096kB = 2146596kB
> Jan 17 13:32:02 LolbraaNAS kernel: Node 0 Normal: 32551*4kB (ME) 90778*8kB (UME) 75509*16kB (UME) 59650*32kB (UME) 29686*64kB (UME) 10975*128kB (UME) 1728*256kB (UME) 210*512kB (UM) 18*1024kB (M) 0*2048kB 0*4096kB = 7846396kB
> Jan 17 13:32:02 LolbraaNAS kernel: Node 0 hugepages_total=0 hugepages_free=0 hugepages_surp=0 hugepages_size=2048kB
> Jan 17 13:32:02 LolbraaNAS kernel: 2133404 total pagecache pages
> Jan 17 13:32:02 LolbraaNAS kernel: 0 pages in swap cache
> Jan 17 13:32:02 LolbraaNAS kernel: Free swap  = 0kB
> Jan 17 13:32:02 LolbraaNAS kernel: Total swap = 0kB
> Jan 17 13:32:02 LolbraaNAS kernel: 8373432 pages RAM
> Jan 17 13:32:02 LolbraaNAS kernel: 0 pages HighMem/MovableOnly
> Jan 17 13:32:02 LolbraaNAS kernel: 166529 pages reserved
> Jan 17 13:32:02 LolbraaNAS kernel: 0 pages cma reserved
> ```
> 

### Årsak:
Kan være flere ulike årsaker
- 

### Fiks:
Kan gå på LolbraaKVM og bruke SYSRSQ for å kjøre Out Of Memory prosess-killer. Dreper
```
Jan 17 13:30:31 LolbraaNAS kernel: Out of memory: Killed process 6009 (node) total-vm:264249252kB, anon-rss:12123208kB, file-rss:0kB, shmem-rss:51828kB, UID:0 pgtables:36316kB oom_score_adj:0
Jan 17 13:30:31 LolbraaNAS kernel: oom_reaper: reaped process 6009 (node), now anon-rss:0kB, file-rss:0kB, shmem-rss:0kB
```

#### Finne prosessen
Ser i HTOP at en node-prosess har kommandolinje som deler mange fellessttrek med entrypoint som UptimeKuma har. 
```sh
docker ps
root@LolbraaNAS:/mnt/user# docker inspect --type=image --format='{{json .Config.Entrypoint}}' louislam/uptime-kuma
["/usr/bin/dumb-init","--","extra/entrypoint.sh"]
```

---

## nginx masse errors ?
### Feiloppførsel:
- WebUI laster skjelettet som vanlig, men ingen informasjon dukker opp. Får ikke interagert med selve maskina?
- Kommer inn med SSH

### Feilmeldinger:
Syslog spammes flere ganger i sekundet
```SYSLOG
Oct 11 21:02:00 LolbraaNAS nginx: 2024/10/11 21:02:00 [error] 7620#7620: *1729956 nchan: error publishing message (HTTP status code 507), client: unix:, server: , request: "POST /pub/cpuload?buffer_length=1 HTTP/1.1", host: "localhost"
Oct 11 21:02:01 LolbraaNAS nginx: 2024/10/11 21:02:01 [crit] 7620#7620: ngx_slab_alloc() failed: no memory
Oct 11 21:02:01 LolbraaNAS nginx: 2024/10/11 21:02:01 [error] 7620#7620: shpool alloc failed
Oct 11 21:02:01 LolbraaNAS nginx: 2024/10/11 21:02:01 [error] 7620#7620: nchan: Out of shared memory while allocating channel /disks. Increase nchan_max_reserved_memory.
Oct 11 21:02:01 LolbraaNAS nginx: 2024/10/11 21:02:01 [error] 7620#7620: *1729957 nchan: error publishing message (HTTP status code 507), client: unix:, server: , request: "POST /pub/disks?buffer_length=1 HTTP/1.1", host: "localhost"
Oct 11 21:02:01 LolbraaNAS nginx: 2024/10/11 21:02:01 [crit] 7620#7620: ngx_slab_alloc() failed: no memory
Oct 11 21:02:01 LolbraaNAS nginx: 2024/10/11 21:02:01 [error] 7620#7620: shpool alloc failed
Oct 11 21:02:01 LolbraaNAS nginx: 2024/10/11 21:02:01 [error] 7620#7620: nchan: Out of shared memory while allocating channel /cpuload. Increase nchan_max_reserved_memory.
Oct 11 21:02:01 LolbraaNAS nginx: 2024/10/11 21:02:01 [error] 7620#7620: *1729958 nchan: error publishing message (HTTP status code 507), client: unix:, server: , request: "POST /pub/cpuload?buffer_length=1 HTTP/1.1", host: "localhost"
Oct 11 21:02:02 LolbraaNAS nginx: 2024/10/11 21:02:02 [crit] 7620#7620: ngx_slab_alloc() failed: no memory
Oct 11 21:02:02 LolbraaNAS nginx: 2024/10/11 21:02:02 [error] 7620#7620: shpool alloc failed
Oct 11 21:02:02 LolbraaNAS nginx: 2024/10/11 21:02:02 [error] 7620#7620: nchan: Out of shared memory while allocating channel /disks. Increase nchan_max_reserved_memory.
Oct 11 20:01:05 LolbraaNAS nginx: 2024/10/11 20:01:05 [error] 7620#7620: *1723524 nchan: error publishing message (HTTP status code 507), client: unix:, server: , request: "POST /pub/disks?buffer_length=1 HTTP/1.1", host: "localhost"
Oct 11 20:01:05 LolbraaNAS nginx: 2024/10/11 20:01:05 [crit] 7620#7620: ngx_slab_alloc() failed: no memory
Oct 11 20:01:05 LolbraaNAS nginx: 2024/10/11 20:01:05 [error] 7620#7620: shpool alloc failed
Oct 11 20:01:05 LolbraaNAS nginx: 2024/10/11 20:01:05 [error] 7620#7620: nchan: Out of shared memory while allocating channel /shares. Increase nchan_max_reserved_memory.
```

### Årsak:
idk ass

### Fiks:
Restartet nginx
```
/etc/rc.d/rc.nginx restart 
```

---

## IO Notify Full Watch
### Feiloppførsel:
- Meste fungerte som det skulle, men mest sannsynlig fungerte ikke alle funksjoner for overvåkning av endringer i filer
- Fikk feilmeldinger ved bruk av mange ulike programmer. Feks VSCode og syslog. 
- Det er en prosess som tar alle watches.
- Unraid kommer med maks limit (så vidt jeg har forstått)

### Feilmeldinger:
Ulike feilmeldinger. Eks Syslog
```SYSLOG
May 21 13:18:54 LolbraaNAS inotifywait[16825]: Couldn't watch new directory /mnt/disk1/immich/library/library/admin/2021/2021.09.24/: No space left on device
```
Visual Studio Code
``` VSCode
Unable to watch for file changes. Please follow the instructions link to resolve this issue.
```

### Årsak:
Kan være flere ulike årsaker
- Trolig Immich ``External Libraries > Library Watching (EXPERIMENTAL)``
- Kan også være ``Mover Tuning > Ignore files listed inside of a text file:``
- Eller iftop eller iotop (installert med nerdtools)
- Ser ikke ut til å være en docker?

### Fiks:
Undersøke hvilke prosesser som har reservert IONOTIFY [linux - How do I find out what inotify watches have been registered? - Stack Overflow](https://stackoverflow.com/questions/13758877/how-do-i-find-out-what-inotify-watches-have-been-registered)
```
sh /boot/config/plugins/user.scripts/scripts/div_ionotify_consumers/script
```
Utklippet resultat:
```
 484658         1     16825 root        inotifywait -mrs -e open,attrib,move,create,delete,modify --excludei (appdata|syslogs|system) --timefmt %b %d %H:%M:%S --format %T %e => %w%f --fromfile /tmp/file.activity/file.activity.disks
```
Etter avskrudd Immich External Libraries gikk den ned til ``488060  WATCHES TOTAL COUNT`` og feilmeldinger i syslog sluttet.

Avinstallert iftop/iotop


Etter restart gikk det ned til 4865 (som det står på https://lolbraanas/Settings/TipsAndTweaks)


---

## Full USB
### Feiloppførsel:
- Hadde SSH-tilgang, men WebUI var blank hvit. Kunne nå login-skjerm.

### Feilmeldinger:
```
Mar 22 15:07:01 LolbraaNAS winbindd[11334]: [2024/03/22 15:07:01.932890,  0] ../../source3/winbindd/winbindd_samr.c:71(open_internal_samr_conn)

Mar 22 15:07:01 LolbraaNAS winbindd[11334]:   open_internal_samr_conn: Could not connect to samr pipe: NT_STATUS_CONNECTION_DISCONNECTED
```

### Årsak:
- Kopierte filer rett fra Midnight Commander-interface til en annen mappe. Filene la seg i /tmp som visstnok ble lagret på USB-minnepennen.
- Fant ut at USB-minnepennen var full ved at `df -h` viste / som 100% brukt

### Fiks:
```
cd /tmp
rm -r mc-root/
```


---

## Frysing, trolig pga. ZFS-kræsj
### Feiloppførsel:
- Dockers, WebGUI, og "alt annet" er stort sett fryst. 
- Kan SSH inn uten problemer
- Får ikke tilgang til /mnt/user (ingen ting under /mnt)
- Får ikke spesielle feilmeldinger. Trolig pga. fuselayer ikke fungerer (?) og får derfor ikke skrevet syslog - eller kræsjer hver gang den forsøker.
- Hver gang jeg restarter PHP så fungerer det frem til den må hente noen ressurser, trolig fra array elns.
- Får ikke gått inn på Cache-siden fra Main (ZFS-formatert), men Diverse (BTRFS)

### Feilmeldinger:
Siste Syslog skrevet til /var/log/syslog.
Problemet startet muligens senere, men idk.
```SYSLOG
Jun 30 15:00:01 LolbraaNAS kernel: BTRFS info (device sdj1): balance: start -dusage=50
Jun 30 15:00:01 LolbraaNAS kernel: BTRFS info (device sdj1): relocating block group 587534958592 flags data|raid1
```
Log på skjerm (PiKVM)
![[Workshop troubleshooting-20240630233435263.jpg]]

### Årsak:
- Mistenker at ZFS (eller noe annet filsystem-greier) kræsjet, og må reboote by force [UI unresponsive - ZFS broken? - General Support - Unraid](https://forums.unraid.net/topic/160208-ui-unresponsive-zfs-broken/)

### Fiks:
1. Forsøkt å restarte Docker, Nginx, PHP, VMs osv... uten hell ([[Unraid Kommandoer#Restart PHP/nginx/Docker/VMs]]).
2. Klarerer ikke å reboote med noen kommandoer, for den klarerer ikke å unmounte?
3. Force-rebooter med PiKVM
```

```



---

# Datarecovery Stigs eksterne harddisk: Ødelagt partisjon
### Feiloppførsel:
- Disk ble gjenkjent i Windows Disk Management og div. andre programmer.
- Det ble gjenkjent en partisjon som RAW, men denne kunne ikke mountes som NTFS (som jeg mistenkte det egt var)
- Denne partisjonen var på ~200GB, mens resten (1.8TB) var ikke partisjonert.

### Fiks:
1. Forsøkte Killdisk Eraser for den har et bra grensesnitt på disker og man kan utforske råverdier. Så at det var masse data skrevet (binært).
2. Google fram til denne Reddittråden ([Recovering a lost partition - need advice on program/utility to do so](https://www.reddit.com/r/DataHoarder/comments/10hs2fb/recovering_a_lost_partition_need_advice_on/)) som linket videre til denne gode oversikten over data recovery-programmer ([What is the best 5 data recovery software for Mac & Windows in 2024 (Free/Paid)](https://www.reddit.com/r/DataRecoveryHelp/comments/18ye3oa/what_is_the_best_5_data_recovery_software_for_mac/?utm_source=share&utm_medium=web2x&context=3))
3. Forsøkte Disk Drill. 
	1. Gjorde binær backup. 
	2. Den fant filer i Recovery-mode, men å faktisk gjenopprette koster 1000kr.
4. Testet FOSS-programmet TestDisk som fungerte dritbra! [CGSecurity - Data recovery: TestDisk & PhotoRec](https://www.cgsecurity.org/wiki/Main_Page)
	1. Kjørte først PhotoRec som henter ut enkeltfiler.

### Arkivering
![[CGSecurity - Data recovery_ TestDisk & PhotoRec (28_03_2024 21_59_06).html]]
![[What is the best 5 data recovery software for Mac & Windows in 2024 (Free_Paid) _ r_DataRecoveryHelp (28_03_2024 22_07_10).html]]



---
# Template
## Tittel
### Feiloppførsel:
- 

### Feilmeldinger:
Ulike feilmeldinger. Eks Syslog
```SYSLOG
```

### Årsak:
Kan være flere ulike årsaker
- 

### Fiks:
```

```