# Få public IP
```
curl ifconfig.me
```

# Hurtig kommandoer
[Lagre i bash-profil?](https://unix.stackexchange.com/questions/26245/how-to-quickly-store-and-access-often-used-commands#26263)

# Filoverføring over SSH
```
scp root@192.168.0.10:/mnt/user/appdata/storj "C:\Users\kriss\Desktop\storj"
scp wordpress-backups-10.2024.zip root@192.168.2.31:/mnt/user/backup/plesk
```

WinSCP har mulighet til mange protokoller, deriblant FTP og WebDav.


# DirStats
Programmer: WinDirStat, 



# Diverse

## Databaser
### MariaDB med phpMyAdmin
Lage ny bruker OG database
```
# Create database query
CREATE DATABASE IF NOT EXISTS tabby_db;

# Create user query with restricted access
CREATE USER tabby_usr@"192.168.0.%" IDENTIFIED BY "sdakljl12+0140s";
GRANT ALL PRIVILEGES ON tabby_db.* TO tabby_usr@"192.168.0.%";
FLUSH PRIVILEGES;
```