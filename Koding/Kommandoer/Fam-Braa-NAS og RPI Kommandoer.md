# LolbraaKVM
Oppdatere
```
pikvm-update
```
[First steps - PiKVM Handbook](https://docs.pikvm.org/first_steps/#getting-access-to-pikvm)
# BraaRPI
Raspberry Pi 3B plassert på Tolvsrød
DDNS /home/braa/cf/ : https://gist.github.com/Firsh/c9f72970eaae3aec04beb1106cc304bc

Wireguard: https://pimylifeup.com/raspberry-pi-wireguard/

## Lage ny wg-profil:
```
sudo pivpn add
scp braa@192.168.1.3:/home/braa/configs/* "C:\Users\kriss\Desktop\vpn"
```

# [Liste over alle kommandoer](https://stackoverflow.com/questions/948008/linux-command-to-list-all-available-commands-and-aliases)
```
/bin:
addgroup       chown          dnsdomainname  ionice         mktemp         ping6          sleep          uname
adduser        cp             echo           ipcalc         more           printenv       stat           usleep
ash            date           egrep          kill           mount          ps             sysctl         vi
bash           dd             false          ln             mv             pwd            tar
busybox        delgroup       fgrep          login          nice           rm             tinylogin
cat            deluser        getopt         ls             passwd         rmdir          touch
chgrp          df             grep           mkdir          pidof          sed            true
chmod          dmesg          hostname       mknod          ping           sh             umount

/sbin:
adjtimex    getty       init        mdev        pivot_root  swapoff     syslogd     zcip
arp         ifconfig    logread     mkswap      poweroff    swapon      udhcpc
fsck        ifenslave   losetup     modprobe    route       sysctl      vconfig

/usr/bin:
ar                         free                       nandfirstgood              snmpget
arping                     fuser                      nandwrite                  snmptranslate
atop                       gdisk                      net                        snmptrap
atopacctd                  genisoimage                netstat                    snmpwalk
atopsar                    getconf                    newgrp                     sort
avahi-browse               getent                     nmbd                       split
avahi-daemon               getfacl                    nmblookup                  ssh
awk                        gpasswd                    nohup                      ssh-keygen
badblocks                  groupmod                   noip2                      sudo
basename                   gunzip                     nslookup                   sysctl
blkid                      gzip                       perl                       tac
blockdev                   hdparm                     php                        tail
chfn                       head                       php-fpm                    tee
clear                      i2cget                     pkill                      testparm
cmp                        i2cset                     printf                     tftp
cp                         id                         pure-ftpd                  tftpd
crontab                    insmod                     pure-ftpd_s                top
curl                       iperf                      python                     tr
cut                        iptables-xml               quotacheck                 traceroute
dbus-daemon                killall                    quotaoff                   traceroute6
dbus-uuidgen               kinit                      quotaon                    tty
detect_char_encode         logger                     readlink                   tune2fs
dhcp6c                     logname                    renice                     ubiattach
dhcp6ctl                   lsmod                      repquota                   ubidetach
diff                       lsof                       resize2fs                  ubimkvol
dirname                    lspci                      rmmod                      unix2dos
djpeg                      lsusb                      rotatelogs                 unlink
dmsetup                    lvm                        scp                        unzip
dos2unix                   mdadm                      sdparm                     upnp_nas_device
dpkg                       minizip                    seq                        uptime
du                         mke2fs                     setfacl                    userdel
dumpe2fs                   mkfifo                     setquota                   usermod
dumpleases                 msmtp                      sftp                       utelnetd
e2fsck                     mt-daapd                   sftp-server                visudo
env                        mutt                       sg_inq                     watch
exif                       mv_eth_tool                sg_sat_identify            wavstreamer
expand                     my_print_defaults          sg_sat_set_features        wbinfo
expr                       mysql                      sg_scan                    wc
ez-ipupdate                mysql_install_db           smartctl                   wget
find                       mysql_secure_installation  smbclient                  winbindd
flac                       mysqladmin                 smbd                       xargs
flash_eraseall             mysqld_safe                smbpasswd                  zeroconf
flock                      nanddump                   snmpd                      zip

/usr/local/bin:
onbrdnetloccomm  ps               top              wdlog            wdnotifier

/usr/local/sbin:
20-checkRAID.sh                           isFactoryFresh.sh
CheckRequiredCommands.sh                  jmeter.sh
CheckRequiredSystemDirectories.sh         languageChange.sh
GoProFin.py                               ledConfig.sh
LogDataSize.sh                            ledCtrl.sh
PullWdlogConfig.sh                        listMediaShares.sh
StorageSet.ini                            logExtract.pl
StorageTrans.py                           masterInstall.sh
ackAlert.sh                               mionet_share_update.php
addUser.sh                                modAcl.sh
addUserVendor.sh                          modAutoFirmwareUpdateConfig.sh
addUser_apache.sh                         modDeviceName.sh
add_device_user.sh                        modDlnaDeviceDescription.sh
alert_email_config.sh                     modDlnaDeviceName.sh
changeOwner.sh                            modDlnaServerEnable.sh
changeRunLevel.pl                         modDlnaShareServing.sh
checkAutoUpdate.sh                        modExtraNtpServer.sh
checkForSshLogin.sh                       modHddStandbyConfig.sh
cleanAlert.sh                             modMediaServerEnable.sh
clearAlerts.sh                            modShareDescription.sh
cmdDlnaServer.sh                          modShareMediaServing.sh
cmdMediaServer.sh                         modShareName.sh
cmdSmartTest.sh                           modShareRemoteAccess.sh
copyImage.sh                              modUserName.sh
copySaveSettingsToDir.sh                  modUserPassword.sh
createAlertDb.sh                          modWorkgroup.sh
createDataVolume.sh                       modifyUserVendor.sh
createShare.sh                            monitorSmartStatus.sh
createUsbSwapDrive.sh                     monitorTemperature.sh
crud_share_db.sh                          monitorVolume.sh
custom_booting_init.sh                    monitorio.sh
custom_shutdown.sh                        multiStepConvertRAID.sh
data-volume-config_helper.sh              networkDhcp.sh
db_init.php                               notifyAckAlert.sh
deleteBackup.sh                           partitionDisk.sh
deleteShare.sh                            privacyOptions.sh
deleteUser.sh                             ps_mem.py
deleteUserVendor.sh                       queueReboot.sh
deleteUser_apache.sh                      raidMigrateLinearToRAID1.sh
disk-param.sh                             raidMigrateRAID1ToLinear.sh
disk_monitor.sh                           raid_configuration_status.sh
drive_helper.sh                           raid_get_drives_info.sh
enableLocalSwap.sh                        raid_get_drives_status.sh
envvars                                   raid_init.sh
factoryRestore.sh                         randomSleep.sh
formatDataVolume.sh                       rescanItunes.sh
freshUpdateFromFile.sh                    resetButtonAction.sh
genApacheAccessRules.sh                   restart_service.sh
genApacheGroupsFile.sh                    restoreConfig.sh
genAppleVolumes.sh                        restoreSettingsFromDir.sh
genHostsConfig.sh                         restoreUserShareState.sh
genItunesConfig.sh                        rotateApache.sh
genMDNSResponderConfig.sh                 rotateLogs.sh
getAcl.sh                                 saveConfigFile.sh
getAutoFirmwareUpdateConfig.sh            saveUserShareState.sh
getBackupModTime.sh                       schedulerAdd.sh
getBackupShareList.sh                     schedulerExists.sh
getBackupShares.sh                        schedulerGet.sh
getBackupSize.sh                          schedulerRemove.sh
getCurrentFirmwareDesc.sh                 sendAlert.sh
getDataVolumePercentUsed.sh               sendEmailAlerts.sh
getDataVolumeUsage.sh                     sendLogToSupport.sh
getDeviceDescription.sh                   send_info.sh
getDeviceModelName.sh                     send_invite_email.sh
getDeviceName.sh                          setAfpSignature.sh
getDlnaDbInfo.sh                          setExternalStorageScan.sh
getDlnaServer.sh                          setNetworkDhcp.sh
getDlnaServerConnectedList.sh             setNetworkStatic.sh
getExternalStorageScan.sh                 setServiceStartup.sh
getExtraNtpServer.sh                      setSharePrivate.sh
getFirmwareUpdateStatus.sh                setSharePublic.sh
getFixedNtpServer.sh                      setTimeMachineConfig.sh
getFreeSpaceStatus.sh                     setTrustees.sh
getHddStandbyConfig.sh                    setUserRaidConfiguration.sh
getMacAddress.sh                          setWdLogAnalytics.sh
getMediaServerConnectedList.sh            settingsManager.sh
getMediaServerDbInfo.sh                   share-param.sh
getNetworkConfig.sh                       shareFunc.sh
getNewFirmwareAvailable.sh                smbReload.sh
getNewFirmwareUpgrade.sh                  smbShare.sh
getOwner.sh                               smbShareAccess.sh
getRaEnhancedLogs.sh                      ssl_cert_job.sh
getRunLevel.pl                            storage_transfer_get_config.sh
getSaveSettingsList.sh                    storage_transfer_set_config.sh
getSerialNumber.sh                        storage_transfer_start_now.sh
getServiceStartup.sh                      updateFirmwareFromFile.sh
getShareDescription.sh                    updateFirmwareToLatest.sh
getShareMediaServing.sh                   updateNasUpnpDevice.sh
getShareRemoteAccess.sh                   update_count_get.sh
getShares.sh                              update_count_set.sh
getSmartStatus.sh                         urlEncode.sh
getSmartTestStatus.sh                     userDataRAIDMonitor.sh
getSystemCapacity.sh                      userRaidConfiguration.sh
getSystemHealth.sh                        userRaidConversionStatus.sh
getSystemLog.sh                           userRaidPartitionsStatus.sh
getSystemState.sh                         userRaidStatus.sh
getTemperatureStatus.sh                   usrPwdExists.sh
getTimeMachineConfig.sh                   usrPwdHash.sh
getUpdateCounts.pm                        vft
getUpnp_uuid.sh                           vol_uuid_change.sh
getUserInfo.sh                            volume_mount.sh
getUserNameFromId.sh                      watchTemp.sh
getUsers.sh                               wd2go.sh
getVolumeStatus.sh                        wdAutoMountAdm.pm
getWipeFactoryRestoreStatus.sh            wdAutoMountBridge.php
getWorkgroup.sh                           wdAutoMountUdevHandler.pm
howMuchToDeleteToConvertLinearToRaid1.sh  wdLogUploader.sh
incUpdateCount.pm                         wdStatus.sh
inc_update_counts.sh                      wdmc_rescan_volume.py
internalDrives.sh                         wipeFactoryRestore.sh

/usr/sbin:
Network_UPS                    iscsid                         sata_pwr_ctl
SetDate                        isnsctl                        sata_test
SetTimeZone                    isoMountIf                     sataumount
UPS_Setting                    iso_mount                      save_alert_email_config.sh
access_mtd                     itune_tool                     save_mtd
account                        itunes.sh                      scandisk
account_mgr                    jhead                          scheddler
afp                            kill_process.sh                schedule_poweron
afpcom                         kill_running_process           scsi_tunning
afpd                           klogd                          send_gen_mail
alert_led.sh                   language.sh                    send_mail_event_at_cron
alert_test                     ldconfig                       send_sms
allow_all_hdd.sh               led                            set_ddns
alphaAlert.sh                  lighty                         set_jumbo_frame.sh
apache                         lighty_check_function.sh       set_lan_speed
apkg                           lighty_ssl                     set_pwm
apkg_favorite                  linkfile                       set_wol
apollo                         lld2d                          sevcd
apps_beta                      lltd.sh                        shutdown.sh
auto_clear_recycle_bin.sh      load_default                   smart_ch_hd_result
auto_fw                        load_module                    smart_report
avahi_restart                  loadphp                        smart_test
avahi_tm_serv                  locale                         smb
before_system_ready.sh         localedef                      smbac
bonding.sh                     log_conf                       smbcmd
cgroup_cpu.sh                  logwdmsg                       smbcom
cgroupfs-mount                 mac_read                       smbcv
cgroupfs-umount                mac_write                      smbgp
check-mtp-device               mail_daemon                    smbif
chk_blockip                    maild                          smbwddb
chk_fw_ver                     make_auth.sh                   snmp_tool
chk_hotplug                    makedav                        sntp
chk_image                      mcu_upgrade                    sqlctl
chk_io                         md_sync_speed.sh               sqldb
chk_quota                      media_analytics.sh             sqlite3
chk_sata                       mem_rw                         sqlsearch
chk_timezone.sh                memory_rw                      ssh
chk_update_firmware            mfg_start                      ssh-keygen
chk_usbdev                     mmfc                           ssh_daemon
chk_wfs_download               mmfm                           sshd
chroot                         mnotify.sh                     startup-mysql
cnid_dbd                       modPhpTimeZone.sh              stime
cnid_metad                     modify_alert_email_config.sh   swapup
compare_image.sh               mount_config.sh                sync
config_set                     mpstat                         sys_diag
creat_perl_link.sh             mserver                        sysinfo_update.sh
crond                          msw                            sysinfod
cryptsetup                     mtd_check                      syslogd
ddns-start                     mtp_backup                     system_daemon
default.script                 mtp_init.sh                    system_init
del_apkg                       mtp_share                      test-filesys
deleteDeviceInfo.sh            mycloud_reloadConfig           test-gp-port
dhcp6c.sh                      mymusic                        test-gphoto2
dhcprelay                      myphoto                        testlibshare
disable_send_mail.sh           mysqlmgr                       traceroute_wd.sh
disk_chk                       netatalk                       transmission-daemon
disk_monitor.sh                network                        transmission-remote
diskmgr                        newp2p                         truncate
dmsetup                        nfs                            tune_performance
do_printer_ups.sh              nfs_config                     tunl_broker.sh
do_reboot                      nfs_usb                        twonky.sh
do_thumbnail                   offl_chk                       twonky_analytics.sh
docker_daemon.sh               openssl                        twonky_rebuild.sh
drive_sleep.sh                 openssl-0.9.8                  twonky_reset.sh
e2igrow                        openvpn                        uart_test
elephant_drive                 operate_auth                   udhcpd
elephantdrive                  p2p.sh                         umount.sh
elephantdriveDaemon            p2p_dog.sh                     umount_config.sh
ethtool                        p2p_done_script.sh             umount_dev.sh
expire.sh                      p2p_send_mail                  unload_usb_storage_driver.sh
exportfs                       phy_link_led.sh                untar_backupfile.sh
ext4_lazy_init.sh              pidstat                        up_read_daemon
fan_control                    portforwarding.sh              up_send_ctl
fireAlert                      portmap                        up_send_daemon
fix_wd_config.sh               post_fwinst.sh                 up_send_init_info
fsort                          power_off_scheduling           updateHdState
ftp                            pre_fwinst.sh                  updateMountStatus
ftp_download                   pre_usb.sh                     updateWDDatabase
ftpcom                         prealloc                       update_image.sh
fusermount                     print-camera-list              update_timezone_config.sh
fvc                            prtrscan                       update_usb_volume_database.sh
fw_update_chk.sh               quota_monitor                  upload_apkg
fw_upgrade                     quota_set                      upload_firmware
ga_cron.sh                     quota_tab_backup               upnp_igdctrl
ganalytics                     raid_config                    upnp_nas_xml
genSelfSignedCert.sh           raid_expand                    upnpnas.sh
getHddWhiteList.sh             raid_expand_disks              ups_action.sh
getIPv6Address.sh              raid_update_info               ups_info
get_parent_info.sh             raidsync                       upsc
get_suffix_product.sh          random_check                   upscan
getexip                        rc.init.sh                     upscmd
getinfo                        rc.messagebus                  upsd
gphoto2                        rdate                          upsdrvctl
gphotofs                       read_hidden_encryption         upsmon
halt                           read_version                   upssched
hardware_init.sh               reboot                         upssched-cmd
hdVerify                       remote_access.sh               usb_backup
hd_standby.sh                  remove_alert                   usb_disk
hiddenumount                   rescue_fw                      usb_power.sh
hotPlug.sh                     rlog                           usb_probe
htpasswd                       rm_log_account_info.sh         usbmount
httpd                          routeap                        usbreset
immediately_shutdown.sh        rpc.mountd                     usbumount
info.sh                        rpc.nfsd                       ve_ctl
init_dir.sh                    rpc.statd                      vlan.sh
inode_growth.sh                rpcbind                        volume_stop.sh
inotify_upnp                   rpcinfo                        vvctl
install_twonky.sh              rsnap                          wakehd.sh
internal_backup                rsnapshot                      wd_compinit
iostat                         rsync                          wd_crontab.sh
ip                             rsyncmd                        wd_read_serial
ip.sh                          rsyncmd.sh                     wd_set_ip
ip6tables                      rsyncom                        wd_write_serial
ip6tables-restore              rt_script.sh                   wdmcmon.sh
ip6tables-save                 rtc                            wipeit
iptables                       run_ssl_cert_job.sh            wto
iptables-restore               run_wget                       xmldb
iptables-save                  s3                             xmldbc
iptables_install.sh            sadc                           xtables-multi
ipv6.sh                        safe_mode.sh                   zcip.script
ipv6_install.sh                samba_tmpfs.sh                 zip_system_log.sh
isEnhancedLoggingEnabled.sh    sar                            zoneinfo
iscsiadm                       sata_disk
iscsictl                       sata_power.sh

```