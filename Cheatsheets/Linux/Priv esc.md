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

#### Sudo privs
```bash
sudo -l
```

#### Kernal

```
linuxexploitsuggester.sh
```