https://forums.serverbuilds.net/t/guide-hardware-transcoding-the-jdm-way-quicksync-and-nvenc/1408/3


# Software
## Jellyfin 
[Hardware Selection | Jellyfin](https://jellyfin.org/docs/general/administration/hardware-selection/)
[NVIDIA GPU | Jellyfin](https://jellyfin.org/docs/general/administration/hardware-acceleration/nvidia/)

H265 støttes ikke av alle klienter! VP9 og AV1 er mer utbredt [Codec Support | Jellyfin](https://jellyfin.org/docs/general/clients/codec-support/)

### Config
[https://hub.docker.com/r/linuxserver/jellyfin](https://hub.docker.com/r/linuxserver/jellyfin)
```
EXTRA-PARAMETERS HWTRANSCODING i docker-template: --runtime=nvidia -e NVIDIA_VISIBLE_DEVICES=all
```


## Immich
[Hardware Transcoding \[Experimental\] | Immich](https://immich.app/docs/features/hardware-transcoding/)
[Hardware-Accelerated Machine Learning \[Experimental\] | Immich](https://immich.app/docs/features/ml-hardware-acceleration/)
[Reddit - Dive into anything](https://www.reddit.com/r/immich/comments/17qd9mw/hw_acceleration_with_unraid/)

Acceleration
[CUDA GPUs - Compute Capability | NVIDIA Developer](https://developer.nvidia.com/cuda-gpus)

---
# Hardware
## P400 (pascal)
Kjøpte p400 for 500kr + frakt.
Se [[Annen hardware#LolbraaKVM]]
### Specs
Fra [Video Encode and Decode GPU Support Matrix | NVIDIA Developer](https://developer.nvidia.com/video-encode-and-decode-gpu-support-matrix-new):

#### NVENC

| BOARD       | FAMILY | NVENC  <br>Generation | Desktop/  <br>Mobile | # OF  <br>CHIPS | Total  <br># of  <br>NVENC | Max # of  <br>concurrent  <br>sessions | H.264  <br>(AVCHD)  <br>YUV 4:2:0 | H.264  <br>(AVCHD)  <br>YUV 4:4:4 | H.264  <br>(AVCHD)  <br>Lossless | H.265  <br>(HEVC)  <br>4K YUV 4:2:0 | H.265  <br>(HEVC)  <br>4K YUV 4:4:4 | H.265  <br>(HEVC)  <br>4K Lossless | H.265  <br>(HEVC)  <br>8K | HEVC  <br>10-bit  <br>support | AV1 |
| ----------- | ------ | --------------------- | -------------------- | --------------- | -------------------------- | -------------------------------------- | --------------------------------- | --------------------------------- | -------------------------------- | ----------------------------------- | ----------------------------------- | ---------------------------------- | ------------------------- | ----------------------------- | --- |
| Quadro P400 | Pascal | 6th Gen               | D                    | 1               | 1                          | 8                                      | YES                               | YES                               | YES                              | YES                                 | YES                                 | YES                                | YES                       | YES                           | NO  |
#### *NVDEC*

| BOARD       | FAMILY | NVDEC  <br>Generation | Desktop/  <br>Mobile | # OF  <br>CHIPS | Total  <br># of  <br>NVDEC | MPEG-1 | MPEG-2 | VC-1 | VP8 | VP9<br>---<br>8 Bit | 10 Bit | 12 Bit | H.264  <br>(AVCHD) | H.265 (HEVC) 4:2:0<br>---<br>8 Bit | 10 Bit | 12 Bit | H.265 (HEVC) 4:4:4<br>---<br>8 Bit | 10 Bit | 12 Bit | AV1<br>---<br>8 Bit | 10 Bit |
| ----------- | ------ | --------------------- | -------------------- | --------------- | -------------------------- | ------ | ------ | ---- | --- | ------------------- | ------ | ------ | ------------------ | ---------------------------------- | ------ | ------ | ---------------------------------- | ------ | ------ | ------------------- | ------ |
| Quadro P400 | Pascal | 3rd Gen               | D                    | 1               | 1                          | YES    | YES    | YES  | NO  | YES                 | YES    | YES    | YES                | YES                                | YES    | YES    | NO                                 | NO     | NO     | NO                  | NO     |

## Intel QuickSync
[Intel Core i5-3570K Processor](https://www.komplett.no/product/660227?noredirect=true "‌")!
Familie: Ivy Bridge
Intel® HD Graphics 4000
![[Hardwaretranscoding-20240815104424982.jpg]]

[Intel x86-64 (Generic) | LibreELEC.wiki](https://wiki.libreelec.tv/hardware/intel-x86-64-generic)

|CPU|Codename|Driver|H264|HEVC|AV1|4K|HDR|
|---|---|---|---|---|---|---|---|
|Gen1|Nehalem|i965|Yes|No|No|No|No|
|Gen2|Sandy-bridge|i965|Yes|No|No|No|No|
|Gen3|Ivy-Bridge|i965|Yes|No|No|No|No|
|Gen4|Haswell|i965|Yes|No|No|No|No|
|Gen5|Broadwell, Braswell|i915|Yes|No|No|No|No|
|Gen6|Skylake|i915|Yes|Yes|No|DP|No|
|Gen7|Kaby-lake, Apollo-lake|i915|Yes|Yes|No|Yes|HDMI|
|Gen8|Coffee-lake, Kaby-lake refresh, Whiskey-lake|i915|Yes|Yes|No|Yes|HDMI|
|Gen9|Coffee-lake refresh|i915|Yes|Yes|No|Yes|HDMI|
|Gen10|Comet-lake, Ice-lake, Amber-lake|i915|Yes|Yes|No|Yes|Yes|
|Gen11|Rocket-lake, Tiger-lake|i915|Yes|Yes|Yes|Yes|Yes|
|Gen12|Alder-lake|i915|Yes|Yes|Yes|Yes|Yes|
|Gen13|Raptor-lake|i915|Yes|Yes|Yes|Yes|Yes|

- Gen6 CPUs (Skylake) have HDMI 1.4b and DisplayPort 1.2 connectors. HDMI can run at max 1920x1200@60 resolution, while DP can run at max 3840x2160@60 resolution.
    
- Gen7 and Gen8 CPUs use an LSPCON chip for HDMI 2.0 output. HDR is supported only when the HDMI output is connected to an HDMI 2.0 port on the TV. Users with Intel NUC devices are recommended to run the latest Intel firmware for their device. Lots of bugs in original/factory LSPCON firmwares have been fixed.
    
- Linux supports LSPCON chips for HDR from Linux 5.12 onwards
    
- Linux has full support for Tiger-Lake CPUs from Linux 5.12 onwards
    
- Intel GPUs are known as _Integrated graphics processors (IGPs)_ and are embedded within the CPU core. Each CPU generation uses a single GPU generation but the generation ID's do not match, e.g. Gen10 CPUs have Gen11 GPUs.