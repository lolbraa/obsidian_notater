# Strategi

- Vil helst standardisere mest mulig
- Mulig å bruke samme program for backup på systemer og offsite-backup av NCGNAS?
	- Virker som det er store forskjeller.

# Onsite-backups
## Programvare
Script/snapshot/borgbackup/osv

Proxmox Backup Server
- Kan kjøres i en VM på NCGNAS
- Backup av:
	- Har en klient som kan installeres på hver maskin
	- Databaseintegrasjon? Skript-dump?
	- God integrasjon mot Proxmox VE
- Research
	- [Backup Solutions (Suggestions)](https://www.reddit.com/r/sysadmin/comments/1b0xhbi/proxmox_and_xcpng_backup_solutions_suggestions/)

[Storware](https://storware.eu/)





## Offsite-backup

### Sikkerhet
Kryptert
På egen disk (enkel transplantsjon når dataen skal flyttes)
Ransomware-beskyttelse: Alarm hvis mye endres!

### Detaljer
Oppdatere: Daglig? Ukentlig?
Retention: Hvert fall en måned bak i tid.

### Verktøy
Velger Borg med Borgmatic pga:
- Veldig anerkjent teknologi. Det er veldig mange verktøy og informasjon der ute, også om best-practices osv.
- Det har vært en del sikkerhetssårbarheter, men en V2 er på vei. Tenker å migrere over når den tid kommer.
- Har en del erfaring
- Virker som den mest strømløse overføringsprotokollen server-server med en klient på mottaker som kan utføre mange prosesser.
- Velger Borgmatic for at konfigurering i etterkant skal være greit enkelt å få oversikt over, har en del ekstra features, er lett å ha i en docker-container, er aktivt utviklet, grei dokumentasjon, og støtter SSH out of the box. Skal ha mulighet for database-backup.

[https://github.com/gilbertchen/duplicacy?tab=readme-ov-file#comparison-with-other-backup-tools](http://Comparison-chart)
- Restic

- Alder: Ikke lansert enda
- Erfaring: Null

- Duplicacy (CLI eller GUI?)

- Alder: 2015?
- Kostnad: Koster penger for GUI
- Erfaring: Har en del erfaring.
- Overføring: SFTP eller SMB

- Borg, evt [Borgmatic](https://torsion.org/borgmatic/docs/how-to/set-up-backups/)

- Alder: 2015
- Kostnad: Gratis
- Erfaring: en del erfaring.
- Overføring: SSH

- Kan offloade prosessering til Borg-instance på LolbraaNAS.
- Over Tailscale eller WireGuard?
- [https://borgbackup.readthedocs.io/en/stable/faq.html#what-is-the-difference-between-a-repo-on-an-external-hard-drive-vs-repo-on-a-server](https://borgbackup.readthedocs.io/en/stable/faq.html#what-is-the-difference-between-a-repo-on-an-external-hard-drive-vs-repo-on-a-server)

- [SSH script](https://borgbackup.readthedocs.io/en/stable/usage/notes.html#ssh-batch-mode)-tips

- Sikkerhetstiltak

- [https://borgbackup.readthedocs.io/en/stable/faq.html#what-is-the-difference-between-a-repo-on-an-external-hard-drive-vs-repo-on-a-server](https://borgbackup.readthedocs.io/en/stable/faq.html#what-is-the-difference-between-a-repo-on-an-external-hard-drive-vs-repo-on-a-server)
- [https://borgbackup.readthedocs.io/en/stable/usage/notes.html#append-only-mode-forbid-compaction](https://borgbackup.readthedocs.io/en/stable/usage/notes.html#append-only-mode-forbid-compaction)
- [https://borgbackup.readthedocs.io/en/stable/deployment/hosting-repositories.html#hosting-repositories](https://borgbackup.readthedocs.io/en/stable/deployment/hosting-repositories.html#hosting-repositories)

- Egen bruker med egen SSH og  konfigurasjon som tillater kun trygge operasjoner

- [https://github.com/borgbackup/community/](https://github.com/borgbackup/community/)
- [https://framagit.org/framasoft/borgbackup/borg-dashboard-vue](https://framagit.org/framasoft/borgbackup/borg-dashboard-vue)
- [https://github.com/hagai-helman/docker-borg-server](https://github.com/hagai-helman/docker-borg-server)
- Bruke docker: [BorgServer](https://hub.docker.com/r/nold360/borgserver)
- Kjøre BorgBench - verktøy for å finne beste hashing?

- rSync

- Ikke en backup

- LuckyBackup

- Utdatert

## On-site backup

### Verktøy

- [Amanda](https://wiki.zmanda.com/index.php/FAQ)

- Alder: Gammelt, virker veldig legitimt for servere.
- Kostnad: Amanda er gratis-versjon av Zmanda (database-backups?)

- [Bacula](https://help.ubuntu.com/community/Bacula)

- Offisiell?

- Borg - Pull mode

- [https://borgbackup.readthedocs.io/en/stable/deployment/pull-backup.html#pull-backup](https://borgbackup.readthedocs.io/en/stable/deployment/pull-backup.html#pull-backup)

- Borg

- [https://borgbackup.readthedocs.io/en/stable/deployment/central-backup-server.html](https://borgbackup.readthedocs.io/en/stable/deployment/central-backup-server.html)

[https://askubuntu.com/questions/103037/what-is-the-easiest-most-effective-backup-system-for-ubuntu-servers](https://askubuntu.com/questions/103037/what-is-the-easiest-most-effective-backup-system-for-ubuntu-servers)



### Pterodactyl
[Site Unreachable](https://builtbybit.com/resources/node-backup-for-pterodactyl.31358/)
```
Good evening!
We're looking into purchasing the Node Backup for Pterodactyl-plugin, but I'm a little confused as to what it actually does. Hence, I want some clarification as to what exactly is backed up, and how?

It's described as a "comprehensive solution" that "ensures the safety of your data, configurations and progress", and "you can restore your nodes to a desired state with just a few clicks".

It may be a lack of understanding of Pterodactyl (I'm not the hostmaster), but does it do a complete system-snapshot to capture everything, or just copy some config-/important files while also wrapping around the builtin server-backup-function?
What kind of remote execution does it utilise, if any? (tar, rSync, borg, spinup a custom docker, etc)
How does it handle processes writing to disk while backups happen, like databases, to hinder corruption?
```




# Troubleshooting
04.05.2024 Borgmatic-NCGOffsite-Admin

To defekte chunks. 
- chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214 is defect.
- chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74 is defect.

```bash
borgmatic -v 2 check // kjørte vel i cirka ett døgn

...
Remote: checking segment file /backup/ncgoffsite.pub/RepoNCGNASOffsite/data/3/3205...
Remote: checking segment file /backup/ncgoffsite.pub/RepoNCGNASOffsite/data/3/3206...
Remote: Starting repository index check
Remote: Index object count match.
Remote: Completed repository check, no problems found.
Starting archive consistency check...
Remote: Verified integrity of /backup/ncgoffsite.pub/RepoNCGNASOffsite/index.3206
Starting cryptographic data integrity verification...

----------------------
chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214, integrity error: MAC Authentication failed
chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74, integrity error: Data integrity error: Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74: id verification failed
----------------------

----------------------
Found defect chunks. With --repair, they would get deleted, so affected files could get repaired then and maybe healed later.
chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214 is defect.
chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74 is defect.
Finished cryptographic data integrity verification, verified 468785 chunks with 2 integrity errors.
----------------------

TAM-verified manifest                                                  
--glob-archives 5172aa3f7665-* does not match any archives    
RepositoryCache: current items 0, size 0 B / 2.15 GB, 0 hits, 0 misses, 0 slow misses (+0.0s), 0 evictions, 0 ENOSPC hit
Orphaned objects check skipped (needs all archives checked).
Archive consistency check complete, problems found.     

RemoteRepository: 25.97 MB bytes sent, 1.18 TB bytes received, 473488 messages sent

terminating with warning status, rc 1                         
Writing check time at /root/.borgmatic/checks/edc548f8b11656c289b70549e532022f14a06902d2e5a7db4211b460926c0075/repository
Writing check time at /root/.borgmatic/checks/edc548f8b11656c289b70549e532022f14a06902d2e5a7db4211b460926c0075/archives/5b39eb3d2ace2c2200255d
d92f1565be627b366f3fa7f32ee9113f7fd548afc6                    
Writing check time at /root/.borgmatic/checks/edc548f8b11656c289b70549e532022f14a06902d2e5a7db4211b460926c0075/data/5b39eb3d2ace2c2200255dd92f
1565be627b366f3fa7f32ee9113f7fd548afc6                        
BORG_PASSPHRASE=*** BORG_EXIT_CODES=*** borg list --last 1 --short ssh://lolbraanas/./ncgoffsite.pub/RepoNCGNASOffsite
ssh://lolbraanas/./ncgoffsite.pub/RepoNCGNASOffsite: Latest archive is backup-2024-05-02T10:00:01
BORG_PASSPHRASE=*** BORG_EXIT_CODES=*** borg extract --dry-run --debug --show-rc --list ssh://lolbraanas/./ncgoffsite.pub/RepoNCGNASOffsite::b
ackup-2024-05-02T10:00:01

using builtin fallback logging configuration
33 self tests completed in 0.59 seconds
SSH command line: ['ssh', 'lolbraanas', 'borg', 'serve', '--debug']
Remote: using builtin fallback logging configuration
Remote: 35 self tests completed in 0.17 seconds
Remote: using builtin fallback logging configuration
Remote: Initialized logging system for JSON-based protocol
Remote: Resolving repository path b'/./ncgoffsite.pub/RepoNCGNASOffsite'
Remote: Resolved repository path to '/backup/ncgoffsite.pub/RepoNCGNASOffsite'
Remote: Verified integrity of /backup/ncgoffsite.pub/RepoNCGNASOffsite/index.3206
TAM-verified manifest
security: read previous location 'ssh://lolbraanas/./ncgoffsite.pub/RepoNCGNASOffsite'
security: read manifest timestamp '2024-05-02T08:30:06.130418'
security: determined newest manifest timestamp as 2024-05-02T08:30:06.130418
security: repository checks ok, allowing access
Archive authentication DISABLED.
TAM-verified archive
mnt/user/backup
mnt/user/backup/README.txt
mnt/user/backup/plesk
mnt/user/backup/plesk/test.txt
mnt/user/backup/plesk/wordpress-backups-10.2024.zip
mnt/user/backup/plesk/proservere.com
mnt/user/backup/plesk/mainjob
mnt/user/backup/plesk/mainjob/backup_2404280010_2404290010.tar
mnt/user/backup/plesk/mainjob/backup_2404020010_2404030010.tar
mnt/user/backup/plesk/mainjob/backup_2404090010_2404100010.tar
mnt/user/backup/plesk/mainjob/backup_2404090010_2404110010.tar
mnt/user/backup/plesk/mainjob/backup_2404090010_2404120010.tar
mnt/user/backup/plesk/mainjob/backup_2404090010_2404130010.tar
mnt/user/backup/plesk/mainjob/backup_2404280010_2404300010.tar
mnt/user/backup/plesk/mainjob/backup_2404280010_2405010010.tar
mnt/user/backup/plesk/mainjob/backup_2402130110.tar
mnt/user/backup/plesk/mainjob/backup_2402130110_2402140110.tar
mnt/user/backup/plesk/mainjob/backup_2404280010_2405020010.tar
mnt/user/backup/plesk/mainjob/backup_2402130110_2402150010.tar
mnt/user/backup/plesk/mainjob/backup_2404090010_2404140010.tar
mnt/user/backup/plesk/mainjob/backup_2402130110_2402160010.tar
mnt/user/backup/plesk/mainjob/backup_2402130110_2402170010.tar
mnt/user/backup/plesk/mainjob/backup_2402130110_2402180010.tar
mnt/user/backup/plesk/mainjob/backup_2402130110_2402190010.tar
mnt/user/backup/plesk/mainjob/backup_2402200010.tar
mnt/user/backup/plesk/mainjob/backup_2402200010_2402210010.tar
mnt/user/backup/plesk/mainjob/backup_2403050010.tar                                                                                           
RemoteRepository: 3.84 MB bytes sent, 145.59 GB bytes received, 72202 messages sent                                                           
still 169 cached responses left in RemoteRepository                                                                                           
Data integrity error: Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74: id verification failed                          
Traceback (most recent call last):                                                                                                            
  File "/usr/local/lib/python3.12/site-packages/borg/archiver.py", line 5401, in main                                                         
    exit_code = archiver.run(args)                                     
                ^^^^^^^^^^^^^^^^^^                                     
  File "/usr/local/lib/python3.12/site-packages/borg/archiver.py", line 5321, in run                                                          
    return set_ec(func(args))                                                                                                                 
                  ^^^^^^^^^^                                                                                                                  
  File "/usr/local/lib/python3.12/site-packages/borg/archiver.py", line 190, in wrapper
    return method(self, args, repository=repository, **kwargs)         
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^                                                                                
  File "/usr/local/lib/python3.12/site-packages/borg/archiver.py", line 205, in wrapper                                                       
    return method(self, args, repository=repository, manifest=manifest, key=key, archive=archive, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^                                   
  File "/usr/local/lib/python3.12/site-packages/borg/archiver.py", line 918, in do_extract                                                    
    archive.extract_item(item, dry_run=True, pi=pi)                                                                                           
  File "/usr/local/lib/python3.12/site-packages/borg/archive.py", line 781, in extract_item                                                   
    for data in self.pipeline.fetch_many([c.id for c in item.chunks], is_preloaded=True):                                                     
  File "/usr/local/lib/python3.12/site-packages/borg/archive.py", line 342, in fetch_many                                                     
    yield self.key.decrypt(id_, data)                                                                                                         
          ^^^^^^^^^^^^^^^^^^^^^^^^^^^                                                                                                         
  File "/usr/local/lib/python3.12/site-packages/borg/crypto/key.py", line 458, in decrypt                                                     
    self.assert_id(id, data)                                           
  File "/usr/local/lib/python3.12/site-packages/borg/crypto/key.py", line 219, in assert_id                                                   
    raise IntegrityError('Chunk %s: id verification failed' % bin_to_hex(id))                                                                 
borg.helpers.errors.IntegrityError: Data integrity error: Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74: id verificat
ion failed                                                                                                                                    
Platform: Linux 5172aa3f7665 6.1.79-Unraid #1 SMP PREEMPT_DYNAMIC Fri Mar 29 13:34:03 PDT 2024 x86_64                                         
Linux: Unknown Linux                                                   
Borg: 1.2.8  Python: CPython 3.12.3 msgpack: 1.0.8 fuse: llfuse 1.5.0 [pyfuse3,llfuse]                                                        
PID: 20921  CWD: /                                                     
sys.argv: ['/usr/local/bin/borg', 'extract', '--dry-run', '--debug', '--show-rc', '--list', 'ssh://lolbraanas/./ncgoffsite.pub/RepoNCGNASOffsi
te::backup-2024-05-02T10:00:01']                                       
SSH_ORIGINAL_COMMAND: None

terminating with error status, rc 2                           
reponcgnasoffsite: Error running actions for repository       
Command 'borg extract --dry-run --debug --show-rc --list ssh://lolbraanas/./ncgoffsite.pub/RepoNCGNASOffsite::backup-2024-05-02T10:00:01' retu
rned non-zero exit status 2.                                                                                                                  
/etc/borgmatic.d/config.yaml: Calling healthchecks hook function ping_monitor
/etc/borgmatic.d/config.yaml: Pinging Healthchecks log
/etc/borgmatic.d/config.yaml: Using Healthchecks ping URL https://hc-ping.com/4a34f551-d784-4948-a168-877e2beba7c8/log
/etc/borgmatic.d/config.yaml: Running command for on-error hook
echo "Error while creating a backup."
Error while creating a backup.
/etc/borgmatic.d/config.yaml: Calling healthchecks hook function ping_monitor
/etc/borgmatic.d/config.yaml: Pinging Healthchecks fail
/etc/borgmatic.d/config.yaml: Using Healthchecks ping URL https://hc-ping.com/4a34f551-d784-4948-a168-877e2beba7c8/fail
/etc/borgmatic.d/config.yaml: Calling healthchecks hook function destroy_monitor
/etc/borgmatic.d/config.yaml: An error occurred

summary:
/etc/borgmatic.d/config.yaml: Loading configuration file
/etc/borgmatic.d/config.yaml: An error occurred
reponcgnasoffsite: Error running actions for repository
...
  File "/usr/local/lib/python3.12/site-packages/borg/archiver.py", line 190, in wrapper
    return method(self, args, repository=repository, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.12/site-packages/borg/archiver.py", line 205, in wrapper
    return method(self, args, repository=repository, manifest=manifest, key=key, archive=archive, **kwargs)
           ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.12/site-packages/borg/archiver.py", line 918, in do_extract
    archive.extract_item(item, dry_run=True, pi=pi)
  File "/usr/local/lib/python3.12/site-packages/borg/archive.py", line 781, in extract_item
    for data in self.pipeline.fetch_many([c.id for c in item.chunks], is_preloaded=True):
  File "/usr/local/lib/python3.12/site-packages/borg/archive.py", line 342, in fetch_many
    yield self.key.decrypt(id_, data)
          ^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/usr/local/lib/python3.12/site-packages/borg/crypto/key.py", line 458, in decrypt
    self.assert_id(id, data)
  File "/usr/local/lib/python3.12/site-packages/borg/crypto/key.py", line 219, in assert_id
    raise IntegrityError('Chunk %s: id verification failed' % bin_to_hex(id))
borg.helpers.errors.IntegrityError: Data integrity error: Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74: id verificat
ion failed
Platform: Linux 5172aa3f7665 6.1.79-Unraid #1 SMP PREEMPT_DYNAMIC Fri Mar 29 13:34:03 PDT 2024 x86_64
Linux: Unknown Linux
Borg: 1.2.8  Python: CPython 3.12.3 msgpack: 1.0.8 fuse: llfuse 1.5.0 [pyfuse3,llfuse]
PID: 20921  CWD: /
sys.argv: ['/usr/local/bin/borg', 'extract', '--dry-run', '--debug', '--show-rc', '--list', 'ssh://lolbraanas/./ncgoffsite.pub/RepoNCGNASOffsi
te::backup-2024-05-02T10:00:01']
SSH_ORIGINAL_COMMAND: None
terminating with error status, rc 2 
Command 'borg extract --dry-run --debug --show-rc --list ssh://lolbraanas/./ncgoffsite.pub/RepoNCGNASOffsite::backup-2024-05-02T10:00:01' retu
rned non-zero exit status 2.

Need some help? https://torsion.org/borgmatic/#issues
```

TAM
- [Important notes — Borg - Deduplicating Archiver 1.2.8 documentation](https://borgbackup.readthedocs.io/en/stable/changes.html#pre-1-2-5-archives-spoofing-vulnerability-cve-2023-36811)
- [Data integrity error: Archive authentication did not verify · Issue #7802 · borgbackup/borg · GitHub](https://github.com/borgbackup/borg/issues/7802#issuecomment-1715956539)

Repair
```
borgmatic -v 2 check --repair --progres --force --only data

BORG_PASSPHRASE=*** BORG_EXIT_CODES=*** borg --version --debug --show-rc
/etc/borgmatic.d/config.yaml: Borg 1.2.8
/etc/borgmatic.d/config.yaml: Calling healthchecks hook function initialize_monitor
/etc/borgmatic.d/config.yaml: Calling healthchecks hook function ping_monitor
/etc/borgmatic.d/config.yaml: Pinging Healthchecks start
/etc/borgmatic.d/config.yaml: Using Healthchecks ping URL https://hc-ping.com/4a34f551-d784-4948-a168-877e2beba7c8/start
reponcgnasoffsite: Running actions for repository
/etc/borgmatic.d/config.yaml: No commands to run for pre-actions hook
/etc/borgmatic.d/config.yaml: No commands to run for pre-check hook
reponcgnasoffsite: Running consistency checks
BORG_PASSPHRASE=*** BORG_EXIT_CODES=*** borg info --json ssh://lolbraanas/./ncgoffsite.pub/RepoNCGNASOffsite
BORG_PASSPHRASE=*** BORG_EXIT_CODES=*** borg check --repair --archives-only --glob-archives {hostname}-* --verify-data --debug --show-rc --progress ssh://lolbraanas/./ncgoffsite.pub/RepoNCGNASOffsite > 
using builtin fallback logging configuration
33 self tests completed in 0.50 seconds
SSH command line: ['ssh', 'lolbraanas', 'borg', 'serve', '--debug']
Remote: using builtin fallback logging configuration
Remote: 35 self tests completed in 0.23 seconds
Remote: using builtin fallback logging configuration
Remote: Initialized logging system for JSON-based protocol
Remote: Resolving repository path b'/./ncgoffsite.pub/RepoNCGNASOffsite'
Remote: Resolved repository path to '/backup/ncgoffsite.pub/RepoNCGNASOffsite'
This is a potentially dangerous function.
check --repair might lead to data loss (for kinds of corruption it is not
capable of dealing with). BE VERY CAREFUL!

Type 'YES' if you understand this and want to continue: YES
Starting archive consistency check...
Remote: Verified integrity of /backup/ncgoffsite.pub/RepoNCGNASOffsite/index.3210
Starting cryptographic data integrity verification...
chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214, integrity error: MAC Authentication failed                            
chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74, integrity error: Data integrity error: Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74: id verification failed
Found defect chunks. They will be deleted now, so affected files can get repaired now and maybe healed later.                                 
Remote: Cleaned up 0 uncommitted segment files (== everything after segment 3210).
Remote: Verified integrity of /backup/ncgoffsite.pub/RepoNCGNASOffsite/hints.3210
chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214 deleted.
chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74 deleted.
Finished cryptographic data integrity verification, verified 468785 chunks with 2 integrity errors.
TAM-verified manifest
--glob-archives 5172aa3f7665-* does not match any archives
RepositoryCache: current items 0, size 0 B / 2.15 GB, 0 hits, 0 misses, 0 slow misses (+0.0s), 0 evictions, 0 ENOSPC hit                      
Orphaned objects check skipped (needs all archives checked).
Writing Manifest.
Committing repo.
Remote: check_free_space: required bytes 666505108, free bytes 13552074747904
Archive consistency check complete, problems found.
RemoteRepository: 25.97 MB bytes sent, 1.18 TB bytes received, 473495 messages sent
terminating with success status, rc 0
Writing check time at /root/.borgmatic/checks/edc548f8b11656c289b70549e532022f14a06902d2e5a7db4211b460926c0075/archives/5b39eb3d2ace2c2200255dd92f1565be627b366f3fa7f32ee9113f7fd548afc6
Writing check time at /root/.borgmatic/checks/edc548f8b11656c289b70549e532022f14a06902d2e5a7db4211b460926c0075/data/5b39eb3d2ace2c2200255dd92f1565be627b366f3fa7f32ee9113f7fd548afc6
/etc/borgmatic.d/config.yaml: No commands to run for post-check hook
/etc/borgmatic.d/config.yaml: No commands to run for post-actions hook
/etc/borgmatic.d/config.yaml: Calling healthchecks hook function ping_monitor
/etc/borgmatic.d/config.yaml: Pinging Healthchecks log
/etc/borgmatic.d/config.yaml: Using Healthchecks ping URL https://hc-ping.com/4a34f551-d784-4948-a168-877e2beba7c8/log
/etc/borgmatic.d/config.yaml: Calling healthchecks hook function ping_monitor
/etc/borgmatic.d/config.yaml: Pinging Healthchecks finish
/etc/borgmatic.d/config.yaml: Using Healthchecks ping URL https://hc-ping.com/4a34f551-d784-4948-a168-877e2beba7c8
/etc/borgmatic.d/config.yaml: Calling healthchecks hook function destroy_monitor

summary:
/etc/borgmatic.d/config.yaml: Loading configuration file
/etc/borgmatic.d/config.yaml: Successfully ran configuration file
/ # borgmatic -v 2 check --repair --progres --force --only data
```


Påfølgende crontab (blant annet reparerende fiks for --repair fra check). Tok 4.5 timer.
```
[2024-05-05 10:00:01,043] INFO: /etc/borgmatic.d/config.yaml: Pinging Healthchecks start
[2024-05-05 10:00:01,221] INFO: /etc/borgmatic.d/config.yaml: Running command for pre-backup hook
[2024-05-05 10:00:01,222] WARNING: Starting a backup job.
[2024-05-05 10:00:01,222] INFO: reponcgnasoffsite: Creating archive
[2024-05-05 10:00:03,516] ANSWER: Creating archive at "ssh://lolbraanas/./RepoNCGNASOffsite::backup-2024-05-05T10:00:01"
[2024-05-05 10:00:03,877] ANSWER: Synchronizing chunks cache...
[2024-05-05 10:00:03,887] ANSWER: Archives: 14, w/ cached Idx: 11, w/ outdated Idx: 9, w/o cached Idx: 12.
[2024-05-05 10:00:03,918] ANSWER: Fetching and building archive index for 5172aa3f7665-2024-05-05T08:00:01.604027 ...
[2024-05-05 10:00:03,945] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:03,946] ANSWER: Reading cached archive chunk index for backup-2024-02-14T09:56:08 ...
[2024-05-05 10:00:03,946] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:03,946] ANSWER: Reading cached archive chunk index for backup-2024-02-29T10:00:01 ...
[2024-05-05 10:00:03,981] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:04,027] ANSWER: Fetching and building archive index for backup-2024-03-17T10:00:01 ...
[2024-05-05 10:00:05,373] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:05,403] ANSWER: Fetching and building archive index for backup-2024-03-24T10:00:01 ...
[2024-05-05 10:00:05,859] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:05,889] ANSWER: Fetching and building archive index for backup-2024-03-31T10:00:01 ...
[2024-05-05 10:00:06,325] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:06,356] ANSWER: Fetching and building archive index for backup-2024-04-07T10:00:01 ...
[2024-05-05 10:00:06,789] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:06,821] ANSWER: Fetching and building archive index for backup-2024-04-14T10:00:01 ...
[2024-05-05 10:00:07,269] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:07,300] ANSWER: Fetching and building archive index for backup-2024-04-16T10:00:01 ...
[2024-05-05 10:00:07,720] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:07,753] ANSWER: Fetching and building archive index for backup-2024-04-28T10:00:01 ...
[2024-05-05 10:00:08,321] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:08,352] ANSWER: Fetching and building archive index for backup-2024-04-29T10:00:01 ...
[2024-05-05 10:00:08,745] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:08,776] ANSWER: Fetching and building archive index for backup-2024-04-30T10:00:01 ...
[2024-05-05 10:00:09,172] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:09,202] ANSWER: Fetching and building archive index for backup-2024-05-01T10:00:01 ...
[2024-05-05 10:00:09,589] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:09,620] ANSWER: Fetching and building archive index for backup-2024-05-02T10:00:01 ...
[2024-05-05 10:00:10,017] ANSWER: Merging into master chunks index ...
[2024-05-05 10:00:10,050] ANSWER: Done.
[2024-05-05 12:04:23,458] ANSWER: ------------------------------------------------------------------------------
[2024-05-05 12:04:23,459] ANSWER: Repository: ssh://lolbraanas/./RepoNCGNASOffsite
[2024-05-05 12:04:23,459] ANSWER: Archive name: backup-2024-05-05T10:00:01
[2024-05-05 12:04:23,459] ANSWER: Archive fingerprint: bcdb8d1b03151010b6a4b2e775dff1d0e72504ef6956392e90b61eb81feb11c9
[2024-05-05 12:04:23,460] ANSWER: Time (start): Sun, 2024-05-05 10:00:03
[2024-05-05 12:04:23,460] ANSWER: Time (end):   Sun, 2024-05-05 12:04:15
[2024-05-05 12:04:23,460] ANSWER: Duration: 2 hours 4 minutes 11.81 seconds
[2024-05-05 12:04:23,460] ANSWER: Number of files: 5228
[2024-05-05 12:04:23,461] ANSWER: Utilization of max. archive size: 0%
[2024-05-05 12:04:23,461] ANSWER: ------------------------------------------------------------------------------
[2024-05-05 12:04:23,461] ANSWER:                        Original size      Compressed size    Deduplicated size
[2024-05-05 12:04:23,461] ANSWER: This archive:                1.19 TB              1.18 TB             82.52 GB
[2024-05-05 12:04:23,461] ANSWER: All archives:               14.92 TB             14.75 TB              1.27 TB
[2024-05-05 12:04:23,682] ANSWER:                        Unique chunks         Total chunks
[2024-05-05 12:04:23,683] ANSWER: Chunk index:                  501538              6026108
[2024-05-05 12:04:23,683] ANSWER: ------------------------------------------------------------------------------
[2024-05-05 12:04:23,684] INFO: /etc/borgmatic.d/config.yaml: Running command for post-backup hook
[2024-05-05 12:04:23,685] WARNING: Backup created.
[2024-05-05 12:04:23,685] INFO: reponcgnasoffsite: Pruning archives
[2024-05-05 12:04:31,285] ANSWER: ------------------------------------------------------------------------------
[2024-05-05 12:04:31,286] ANSWER:                        Original size      Compressed size    Deduplicated size
[2024-05-05 12:04:31,286] ANSWER: Deleted data:               -1.11 TB             -1.09 TB           -892.58 kB
[2024-05-05 12:04:31,286] ANSWER: All archives:               13.81 TB             13.66 TB              1.27 TB
[2024-05-05 12:04:31,379] ANSWER:                        Unique chunks         Total chunks
[2024-05-05 12:04:31,380] ANSWER: Chunk index:                  501526              5583282
[2024-05-05 12:04:31,380] ANSWER: ------------------------------------------------------------------------------
[2024-05-05 12:04:31,381] INFO: reponcgnasoffsite: Compacting segments
[2024-05-05 12:04:33,791] INFO: reponcgnasoffsite: Running consistency checks
[2024-05-05 12:04:36,854] INFO: Remote: Starting repository check
[2024-05-05 14:30:20,666] INFO: Remote: Starting repository index check
[2024-05-05 14:30:20,666] INFO: Remote: Index object count match.
[2024-05-05 14:30:20,921] INFO: Remote: Completed repository check, no problems found.
[2024-05-05 14:30:20,927] INFO: Starting archive consistency check...
[2024-05-05 14:30:22,651] INFO: Analyzing archive backup-2024-02-14T09:56:08 (1/13)
[2024-05-05 14:30:22,824] INFO: Analyzing archive backup-2024-02-29T10:00:01 (2/13)
[2024-05-05 14:30:23,431] INFO: backup-2024-02-29T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402200010.tar: Healed previously missing file chunk! (Byte 1976029534-1978130531, Chunk af520e43f88c7b9ddc8024502eb89ed660eccc1fe5c0b4cefeebd35bfc743067).
[2024-05-05 14:30:23,432] INFO: backup-2024-02-29T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402200010.tar: Healed previously missing file chunk! (Byte 1978130531-1980774674, Chunk 783a53b37aa783382ba04ea2c632e2a81aee16b455d6cf6652daab503823ccfa).
[2024-05-05 14:30:23,432] INFO: backup-2024-02-29T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402200010.tar: Healed previously missing file chunk! (Byte 1980774674-1986585568, Chunk 1a2bd9018186f8f834d206f3f73e4032db463cf45398e51cc654ae037e01ba90).
[2024-05-05 14:30:23,433] INFO: backup-2024-02-29T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402200010.tar: Healed previously missing file chunk! (Byte 1986585568-1988909591, Chunk 2ffd50f1321a6421758ceb78436afb8b59208dbb24387f75a93cf883ce5af413).
[2024-05-05 14:30:23,433] INFO: backup-2024-02-29T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402200010.tar: Healed previously missing file chunk! (Byte 1988909591-1990597466, Chunk 1591dc2252394e569efc3b40cd1c46603d87b77129e1f90cb3583018a42ed89c).
[2024-05-05 14:30:23,434] INFO: backup-2024-02-29T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402200010.tar: Healed previously missing file chunk! (Byte 1990597466-1998979191, Chunk 942a36d98909853d4d3a30415bd522785e695155a2734fe34e8ffb117974b3fb).
[2024-05-05 14:30:23,434] INFO: backup-2024-02-29T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402200010.tar: Healed previously missing file chunk! (Byte 1998979191-2003268953, Chunk 8a073293325aa884255f80d4409e3ac1fc2f67bd448ad36cbd7592586c6edb16).
[2024-05-05 14:30:23,434] INFO: backup-2024-02-29T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402200010.tar: Healed previously missing file chunk! (Byte 2003268953-2007123734, Chunk 98351073f05f4b2e9ba2931699f00c43c987f5e2ac528c88fbafabfb0f1c182d).
[2024-05-05 14:30:23,452] INFO: backup-2024-02-29T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402200010.tar: Completely healed previously damaged file!
[2024-05-05 14:30:24,988] INFO: Analyzing archive backup-2024-03-24T10:00:01 (3/13)
[2024-05-05 14:30:25,383] INFO: backup-2024-03-24T10:00:01: mnt/user/backup/plesk/mainjob/backup_2403050010.tar: New missing file chunk detected (Byte 5659927369-5668315977, Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74). Replacing with all-zero chunk.
[2024-05-05 14:30:26,762] INFO: backup-2024-03-24T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402270010_2403030010.tar: New missing file chunk detected (Byte 296432541-299015083, Chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214). Replacing with all-zero chunk.
[2024-05-05 14:30:27,132] INFO: Analyzing archive backup-2024-03-31T10:00:01 (4/13)
[2024-05-05 14:30:27,491] INFO: backup-2024-03-31T10:00:01: mnt/user/backup/plesk/mainjob/backup_2403050010.tar: New missing file chunk detected (Byte 5659927369-5668315977, Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74). Replacing with all-zero chunk.
[2024-05-05 14:30:28,793] INFO: backup-2024-03-31T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402270010_2403030010.tar: New missing file chunk detected (Byte 296432541-299015083, Chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214). Replacing with all-zero chunk.
[2024-05-05 14:30:29,175] INFO: Analyzing archive backup-2024-04-07T10:00:01 (5/13)
[2024-05-05 14:30:29,465] INFO: backup-2024-04-07T10:00:01: mnt/user/backup/plesk/mainjob/backup_2403050010.tar: New missing file chunk detected (Byte 5659927369-5668315977, Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74). Replacing with all-zero chunk.
[2024-05-05 14:30:30,850] INFO: backup-2024-04-07T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402270010_2403030010.tar: New missing file chunk detected (Byte 296432541-299015083, Chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214). Replacing with all-zero chunk.
[2024-05-05 14:30:31,237] INFO: Analyzing archive backup-2024-04-14T10:00:01 (6/13)
[2024-05-05 14:30:31,505] INFO: backup-2024-04-14T10:00:01: mnt/user/backup/plesk/mainjob/backup_2403050010.tar: New missing file chunk detected (Byte 5659927369-5668315977, Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74). Replacing with all-zero chunk.
[2024-05-05 14:30:32,912] INFO: backup-2024-04-14T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402270010_2403030010.tar: New missing file chunk detected (Byte 296432541-299015083, Chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214). Replacing with all-zero chunk.
[2024-05-05 14:30:33,321] INFO: Analyzing archive backup-2024-04-16T10:00:01 (7/13)
[2024-05-05 14:30:33,568] INFO: backup-2024-04-16T10:00:01: mnt/user/backup/plesk/mainjob/backup_2403050010.tar: New missing file chunk detected (Byte 5659927369-5668315977, Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74). Replacing with all-zero chunk.
[2024-05-05 14:30:34,951] INFO: backup-2024-04-16T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402270010_2403030010.tar: New missing file chunk detected (Byte 296432541-299015083, Chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214). Replacing with all-zero chunk.
[2024-05-05 14:30:35,367] INFO: Analyzing archive backup-2024-04-28T10:00:01 (8/13)
[2024-05-05 14:30:35,609] INFO: backup-2024-04-28T10:00:01: mnt/user/backup/plesk/mainjob/backup_2403050010.tar: New missing file chunk detected (Byte 5659927369-5668315977, Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74). Replacing with all-zero chunk.
[2024-05-05 14:30:37,001] INFO: backup-2024-04-28T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402270010_2403030010.tar: New missing file chunk detected (Byte 296432541-299015083, Chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214). Replacing with all-zero chunk.
[2024-05-05 14:30:37,418] INFO: Analyzing archive backup-2024-04-29T10:00:01 (9/13)
[2024-05-05 14:30:37,666] INFO: backup-2024-04-29T10:00:01: mnt/user/backup/plesk/mainjob/backup_2403050010.tar: New missing file chunk detected (Byte 5659927369-5668315977, Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74). Replacing with all-zero chunk.
[2024-05-05 14:30:38,977] INFO: backup-2024-04-29T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402270010_2403030010.tar: New missing file chunk detected (Byte 296432541-299015083, Chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214). Replacing with all-zero chunk.
[2024-05-05 14:30:39,389] INFO: Analyzing archive backup-2024-04-30T10:00:01 (10/13)
[2024-05-05 14:30:39,647] INFO: backup-2024-04-30T10:00:01: mnt/user/backup/plesk/mainjob/backup_2403050010.tar: New missing file chunk detected (Byte 5659927369-5668315977, Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74). Replacing with all-zero chunk.
[2024-05-05 14:30:40,954] INFO: backup-2024-04-30T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402270010_2403030010.tar: New missing file chunk detected (Byte 296432541-299015083, Chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214). Replacing with all-zero chunk.
[2024-05-05 14:30:41,351] INFO: Analyzing archive backup-2024-05-01T10:00:01 (11/13)
[2024-05-05 14:30:41,637] INFO: backup-2024-05-01T10:00:01: mnt/user/backup/plesk/mainjob/backup_2403050010.tar: New missing file chunk detected (Byte 5659927369-5668315977, Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74). Replacing with all-zero chunk.
[2024-05-05 14:30:42,947] INFO: backup-2024-05-01T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402270010_2403030010.tar: New missing file chunk detected (Byte 296432541-299015083, Chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214). Replacing with all-zero chunk.
[2024-05-05 14:30:43,345] INFO: Analyzing archive backup-2024-05-02T10:00:01 (12/13)
[2024-05-05 14:30:43,563] INFO: backup-2024-05-02T10:00:01: mnt/user/backup/plesk/mainjob/backup_2403050010.tar: New missing file chunk detected (Byte 5659927369-5668315977, Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74). Replacing with all-zero chunk.
[2024-05-05 14:30:44,865] INFO: backup-2024-05-02T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402270010_2403030010.tar: New missing file chunk detected (Byte 296432541-299015083, Chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214). Replacing with all-zero chunk.
[2024-05-05 14:30:45,284] INFO: Analyzing archive backup-2024-05-05T10:00:01 (13/13)
[2024-05-05 14:30:45,518] INFO: backup-2024-05-05T10:00:01: mnt/user/backup/plesk/mainjob/backup_2403050010.tar: New missing file chunk detected (Byte 5659927369-5668315977, Chunk 52d4fa32747f2ff8f9e329dcb9ba7032f02bed8f54029d0e9df36537aed74a74). Replacing with all-zero chunk.
[2024-05-05 14:30:46,974] INFO: backup-2024-05-05T10:00:01: mnt/user/backup/plesk/mainjob/backup_2402270010_2403030010.tar: New missing file chunk detected (Byte 296432541-299015083, Chunk 54373fe51872d3aaca3763ffd03bc32dc394e288702f97f3b50fdbab82607214). Replacing with all-zero chunk.
[2024-05-05 14:30:47,468] INFO: Orphaned objects check skipped (needs all archives checked).
[2024-05-05 14:30:47,469] INFO: Archive consistency check complete, problems found.
[2024-05-05 14:30:47,712] INFO: /etc/borgmatic.d/config.yaml: Pinging Healthchecks log
[2024-05-05 14:30:47,869] INFO: /etc/borgmatic.d/config.yaml: Pinging Healthchecks finish
[2024-05-05 14:30:48,023] INFO: 
[2024-05-05 14:30:48,023] INFO: summary:
[2024-05-05 14:30:48,023] INFO: /etc/borgmatic.d/config.yaml: Successfully ran configuration file

```