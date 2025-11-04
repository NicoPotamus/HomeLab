# ENVIRONMENT VARIABLES

### manage env varaibles on bash host

Run `env` to get things going 

```
nicod@nicod-Standard-PC-Q35-ICH9-2009:~$ env
SHELL=/bin/bash
SESSION_MANAGER=local/nicod-Standard-PC-Q35-ICH9-2009:@/tmp/.ICE-unix/2759,unix/nicod-Standard-PC-Q35-ICH9-2009:/tmp/.ICE-unix/2759
QT_ACCESSIBILITY=1
COLORTERM=truecolor
XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
XDG_MENU_PREFIX=gnome-
GNOME_DESKTOP_SESSION_ID=this-is-deprecated
GNOME_SHELL_SESSION_MODE=ubuntu
SSH_AUTH_SOCK=/run/user/1000/keyring/ssh
MEMORY_PRESSURE_WRITE=c29tZSAyMDAwMDAgMjAwMDAwMAA=
XMODIFIERS=@im=ibus
DESKTOP_SESSION=ubuntu
GTK_MODULES=gail:atk-bridge
PWD=/home/nicod
LOGNAME=nicod
XDG_SESSION_DESKTOP=ubuntu
XDG_SESSION_TYPE=wayland
SYSTEMD_EXEC_PID=2790
XAUTHORITY=/run/user/1000/.mutter-Xwaylandauth.L5QMF3
HOME=/home/nicod
USERNAME=nicod
IM_CONFIG_PHASE=1
LANG=en_US.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=00:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.avif=01;35:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:*~=00;90:*#=00;90:*.bak=00;90:*.crdownload=00;90:*.dpkg-dist=00;90:*.dpkg-new=00;90:*.dpkg-old=00;90:*.dpkg-tmp=00;90:*.old=00;90:*.orig=00;90:*.part=00;90:*.rej=00;90:*.rpmnew=00;90:*.rpmorig=00;90:*.rpmsave=00;90:*.swp=00;90:*.tmp=00;90:*.ucf-dist=00;90:*.ucf-new=00;90:*.ucf-old=00;90:
XDG_CURRENT_DESKTOP=ubuntu:GNOME
MEMORY_PRESSURE_WATCH=/sys/fs/cgroup/user.slice/user-1000.slice/user@1000.service/session.slice/org.gnome.Shell@wayland.service/memory.pressure
VTE_VERSION=7800
WAYLAND_DISPLAY=wayland-0
GNOME_TERMINAL_SCREEN=/org/gnome/Terminal/screen/a0d7a018_d635_4b55_b792_cb7291d9bab1
GNOME_SETUP_DISPLAY=:1
LESSCLOSE=/usr/bin/lesspipe %s %s
XDG_SESSION_CLASS=user
TERM=xterm-256color
LESSOPEN=| /usr/bin/lesspipe %s
USER=nicod
GNOME_TERMINAL_SERVICE=:1.135
DISPLAY=:0
SHLVL=1
GSM_SKIP_SSH_AGENT_WORKAROUND=true
QT_IM_MODULE=ibus
XDG_RUNTIME_DIR=/run/user/1000
DEBUGINFOD_URLS=https://debuginfod.ubuntu.com 
XDG_DATA_DIRS=/usr/share/ubuntu:/usr/share/gnome:/usr/local/share/:/usr/share/:/var/lib/snapd/desktop
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
GDMSESSION=ubuntu
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus
_=/usr/bin/env
```


`export` sets a temp env var while `unset` does the oppsosite in bash; they're built in 

lets set an environment vatiable valled hello, then unset validating each step taking with echo
```
nicod@nicod-Standard-PC-Q35-ICH9-2009:~$ echo $HELLO

nicod@nicod-Standard-PC-Q35-ICH9-2009:~$ export HELLO=12
nicod@nicod-Standard-PC-Q35-ICH9-2009:~$ echo $HELLO
12
nicod@nicod-Standard-PC-Q35-ICH9-2009:~$ unset HELLO
nicod@nicod-Standard-PC-Q35-ICH9-2009:~$ echo $HELLO

nicod@nicod-Standard-PC-Q35-ICH9-2009:~$ 
```
---
### Environment varaible inheritance

Lets' compare the the env variables of a parent and child process off of fork

```
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ ls
cap_leak.c  catall.c  myenv.c  myprintenv.c
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ gcc myprintenv.c 
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ ls
a.out  cap_leak.c  catall.c  myenv.c  myprintenv.c
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ a.out > file
a.out: command not found
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ ./a.out > file
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ ls
a.out  cap_leak.c  catall.c  file  myenv.c  myprintenv.c
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ cat file 
SHELL=/bin/bash
SESSION_MANAGER=local/nicod-Standard-PC-Q35-ICH9-2009:@/tmp/.ICE-unix/2759,unix/nicod-Standard-PC-Q35-ICH9-2009:/tmp/.ICE-unix/2759
QT_ACCESSIBILITY=1
COLORTERM=truecolor
XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
XDG_MENU_PREFIX=gnome-
GNOME_DESKTOP_SESSION_ID=this-is-deprecated
GNOME_SHELL_SESSION_MODE=ubuntu
SSH_AUTH_SOCK=/run/user/1000/keyring/ssh
MEMORY_PRESSURE_WRITE=c29tZSAyMDAwMDAgMjAwMDAwMAA=
XMODIFIERS=@im=ibus
DESKTOP_SESSION=ubuntu
GTK_MODULES=gail:atk-bridge
PWD=/home/nicod/Downloads/Labsetup
LOGNAME=nicod
XDG_SESSION_DESKTOP=ubuntu
XDG_SESSION_TYPE=wayland
SYSTEMD_EXEC_PID=2790
XAUTHORITY=/run/user/1000/.mutter-Xwaylandauth.L5QMF3
HOME=/home/nicod
USERNAME=nicod
IM_CONFIG_PHASE=1
LANG=en_US.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=00:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.avif=01;35:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:*~=00;90:*#=00;90:*.bak=00;90:*.crdownload=00;90:*.dpkg-dist=00;90:*.dpkg-new=00;90:*.dpkg-old=00;90:*.dpkg-tmp=00;90:*.old=00;90:*.orig=00;90:*.part=00;90:*.rej=00;90:*.rpmnew=00;90:*.rpmorig=00;90:*.rpmsave=00;90:*.swp=00;90:*.tmp=00;90:*.ucf-dist=00;90:*.ucf-new=00;90:*.ucf-old=00;90:
XDG_CURRENT_DESKTOP=ubuntu:GNOME
MEMORY_PRESSURE_WATCH=/sys/fs/cgroup/user.slice/user-1000.slice/user@1000.service/session.slice/org.gnome.Shell@wayland.service/memory.pressure
VTE_VERSION=7800
WAYLAND_DISPLAY=wayland-0
GNOME_TERMINAL_SCREEN=/org/gnome/Terminal/screen/a0d7a018_d635_4b55_b792_cb7291d9bab1
GNOME_SETUP_DISPLAY=:1
LESSCLOSE=/usr/bin/lesspipe %s %s
XDG_SESSION_CLASS=user
TERM=xterm-256color
LESSOPEN=| /usr/bin/lesspipe %s
USER=nicod
GNOME_TERMINAL_SERVICE=:1.135
DISPLAY=:0
SHLVL=1
GSM_SKIP_SSH_AGENT_WORKAROUND=true
QT_IM_MODULE=ibus
XDG_RUNTIME_DIR=/run/user/1000
DEBUGINFOD_URLS=https://debuginfod.ubuntu.com 
XDG_DATA_DIRS=/usr/share/ubuntu:/usr/share/gnome:/usr/local/share/:/usr/share/:/var/lib/snapd/desktop
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
GDMSESSION=ubuntu
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus
_=./a.out
OLDPWD=/home/nicod/Downloads
```
the output is actually identical meaning that both parent and child processes have the same environment variables

---
### execve()
- Calls and executes a system command

when comparing the difference between 

`execve("/usr/bin/env", argv, environ);` and `execve("/usr/bin/env", argv, null);` we see that the null value ensures that the program doesn't get access to any of the actual environment variables beside the path specified, however if you subsitute the `null` for `environ` you get the following:
```
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ ./myenv
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ ./myenv2 
SHELL=/bin/bash
SESSION_MANAGER=local/nicod-Standard-PC-Q35-ICH9-2009:@/tmp/.ICE-unix/2759,unix/nicod-Standard-PC-Q35-ICH9-2009:/tmp/.ICE-unix/2759
QT_ACCESSIBILITY=1
COLORTERM=truecolor
XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
XDG_MENU_PREFIX=gnome-
GNOME_DESKTOP_SESSION_ID=this-is-deprecated
GNOME_SHELL_SESSION_MODE=ubuntu
SSH_AUTH_SOCK=/run/user/1000/keyring/ssh
MEMORY_PRESSURE_WRITE=c29tZSAyMDAwMDAgMjAwMDAwMAA=
XMODIFIERS=@im=ibus
DESKTOP_SESSION=ubuntu
GTK_MODULES=gail:atk-bridge
PWD=/home/nicod/Downloads/Labsetup
LOGNAME=nicod
XDG_SESSION_DESKTOP=ubuntu
XDG_SESSION_TYPE=wayland
SYSTEMD_EXEC_PID=2790
XAUTHORITY=/run/user/1000/.mutter-Xwaylandauth.L5QMF3
HOME=/home/nicod
USERNAME=nicod
IM_CONFIG_PHASE=1
LANG=en_US.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=00:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.avif=01;35:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:*~=00;90:*#=00;90:*.bak=00;90:*.crdownload=00;90:*.dpkg-dist=00;90:*.dpkg-new=00;90:*.dpkg-old=00;90:*.dpkg-tmp=00;90:*.old=00;90:*.orig=00;90:*.part=00;90:*.rej=00;90:*.rpmnew=00;90:*.rpmorig=00;90:*.rpmsave=00;90:*.swp=00;90:*.tmp=00;90:*.ucf-dist=00;90:*.ucf-new=00;90:*.ucf-old=00;90:
XDG_CURRENT_DESKTOP=ubuntu:GNOME
MEMORY_PRESSURE_WATCH=/sys/fs/cgroup/user.slice/user-1000.slice/user@1000.service/session.slice/org.gnome.Shell@wayland.service/memory.pressure
VTE_VERSION=7800
WAYLAND_DISPLAY=wayland-0
GNOME_TERMINAL_SCREEN=/org/gnome/Terminal/screen/a0d7a018_d635_4b55_b792_cb7291d9bab1
GNOME_SETUP_DISPLAY=:1
LESSCLOSE=/usr/bin/lesspipe %s %s
XDG_SESSION_CLASS=user
TERM=xterm-256color
LESSOPEN=| /usr/bin/lesspipe %s
USER=nicod
GNOME_TERMINAL_SERVICE=:1.135
DISPLAY=:0
SHLVL=1
GSM_SKIP_SSH_AGENT_WORKAROUND=true
QT_IM_MODULE=ibus
XDG_RUNTIME_DIR=/run/user/1000
DEBUGINFOD_URLS=https://debuginfod.ubuntu.com 
XDG_DATA_DIRS=/usr/share/ubuntu:/usr/share/gnome:/usr/local/share/:/usr/share/:/var/lib/snapd/desktop
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
GDMSESSION=ubuntu
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus
_=./myenv2
OLDPWD=/home/nicod/Downloads
```

---
### system()
- calls '/bin/sh' to execute a system call
- very vulnerable

### Set-UID with environment Variables
when we work with set uid programs we have to be aware of the environment varaibles that get passed down into the child processes as seen below:

```
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ vi envVar.c
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ gcc envVar.c -o envVarSetUID
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ chmod 4755 envVarSetUID 
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ sudo chown root envVarSetUID 
[sudo] password for nicod: 
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ echo $ANY_NAME

nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ echo $LD LIBRARY PATH
LIBRARY PATH
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ export ANY_NAME="Nico D is my name"
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ echo $ANY_NAME
Nico D is my name
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ ./envVarSetUID 
SHELL=/bin/bash
SESSION_MANAGER=local/nicod-Standard-PC-Q35-ICH9-2009:@/tmp/.ICE-unix/2759,unix/nicod-Standard-PC-Q35-ICH9-2009:/tmp/.ICE-unix/2759
QT_ACCESSIBILITY=1
COLORTERM=truecolor
XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
XDG_MENU_PREFIX=gnome-
GNOME_DESKTOP_SESSION_ID=this-is-deprecated
ANY_NAME=Nico D is my name
GNOME_SHELL_SESSION_MODE=ubuntu
SSH_AUTH_SOCK=/run/user/1000/keyring/ssh
MEMORY_PRESSURE_WRITE=c29tZSAyMDAwMDAgMjAwMDAwMAA=
XMODIFIERS=@im=ibus
DESKTOP_SESSION=ubuntu
GTK_MODULES=gail:atk-bridge
PWD=/home/nicod/Downloads/Labsetup
LOGNAME=nicod
XDG_SESSION_DESKTOP=ubuntu
XDG_SESSION_TYPE=wayland
SYSTEMD_EXEC_PID=2790
XAUTHORITY=/run/user/1000/.mutter-Xwaylandauth.L5QMF3
HOME=/home/nicod
USERNAME=nicod
IM_CONFIG_PHASE=1
LANG=en_US.UTF-8
LS_COLORS=rs=0:di=01;34:ln=01;36:mh=00:pi=40;33:so=01;35:do=01;35:bd=40;33;01:cd=40;33;01:or=40;31;01:mi=00:su=37;41:sg=30;43:ca=00:tw=30;42:ow=34;42:st=37;44:ex=01;32:*.tar=01;31:*.tgz=01;31:*.arc=01;31:*.arj=01;31:*.taz=01;31:*.lha=01;31:*.lz4=01;31:*.lzh=01;31:*.lzma=01;31:*.tlz=01;31:*.txz=01;31:*.tzo=01;31:*.t7z=01;31:*.zip=01;31:*.z=01;31:*.dz=01;31:*.gz=01;31:*.lrz=01;31:*.lz=01;31:*.lzo=01;31:*.xz=01;31:*.zst=01;31:*.tzst=01;31:*.bz2=01;31:*.bz=01;31:*.tbz=01;31:*.tbz2=01;31:*.tz=01;31:*.deb=01;31:*.rpm=01;31:*.jar=01;31:*.war=01;31:*.ear=01;31:*.sar=01;31:*.rar=01;31:*.alz=01;31:*.ace=01;31:*.zoo=01;31:*.cpio=01;31:*.7z=01;31:*.rz=01;31:*.cab=01;31:*.wim=01;31:*.swm=01;31:*.dwm=01;31:*.esd=01;31:*.avif=01;35:*.jpg=01;35:*.jpeg=01;35:*.mjpg=01;35:*.mjpeg=01;35:*.gif=01;35:*.bmp=01;35:*.pbm=01;35:*.pgm=01;35:*.ppm=01;35:*.tga=01;35:*.xbm=01;35:*.xpm=01;35:*.tif=01;35:*.tiff=01;35:*.png=01;35:*.svg=01;35:*.svgz=01;35:*.mng=01;35:*.pcx=01;35:*.mov=01;35:*.mpg=01;35:*.mpeg=01;35:*.m2v=01;35:*.mkv=01;35:*.webm=01;35:*.webp=01;35:*.ogm=01;35:*.mp4=01;35:*.m4v=01;35:*.mp4v=01;35:*.vob=01;35:*.qt=01;35:*.nuv=01;35:*.wmv=01;35:*.asf=01;35:*.rm=01;35:*.rmvb=01;35:*.flc=01;35:*.avi=01;35:*.fli=01;35:*.flv=01;35:*.gl=01;35:*.dl=01;35:*.xcf=01;35:*.xwd=01;35:*.yuv=01;35:*.cgm=01;35:*.emf=01;35:*.ogv=01;35:*.ogx=01;35:*.aac=00;36:*.au=00;36:*.flac=00;36:*.m4a=00;36:*.mid=00;36:*.midi=00;36:*.mka=00;36:*.mp3=00;36:*.mpc=00;36:*.ogg=00;36:*.ra=00;36:*.wav=00;36:*.oga=00;36:*.opus=00;36:*.spx=00;36:*.xspf=00;36:*~=00;90:*#=00;90:*.bak=00;90:*.crdownload=00;90:*.dpkg-dist=00;90:*.dpkg-new=00;90:*.dpkg-old=00;90:*.dpkg-tmp=00;90:*.old=00;90:*.orig=00;90:*.part=00;90:*.rej=00;90:*.rpmnew=00;90:*.rpmorig=00;90:*.rpmsave=00;90:*.swp=00;90:*.tmp=00;90:*.ucf-dist=00;90:*.ucf-new=00;90:*.ucf-old=00;90:
XDG_CURRENT_DESKTOP=ubuntu:GNOME
MEMORY_PRESSURE_WATCH=/sys/fs/cgroup/user.slice/user-1000.slice/user@1000.service/session.slice/org.gnome.Shell@wayland.service/memory.pressure
VTE_VERSION=7800
WAYLAND_DISPLAY=wayland-0
GNOME_TERMINAL_SCREEN=/org/gnome/Terminal/screen/a0d7a018_d635_4b55_b792_cb7291d9bab1
GNOME_SETUP_DISPLAY=:1
LESSCLOSE=/usr/bin/lesspipe %s %s
XDG_SESSION_CLASS=user
TERM=xterm-256color
LESSOPEN=| /usr/bin/lesspipe %s
USER=nicod
GNOME_TERMINAL_SERVICE=:1.135
DISPLAY=:0
SHLVL=1
GSM_SKIP_SSH_AGENT_WORKAROUND=true
QT_IM_MODULE=ibus
XDG_RUNTIME_DIR=/run/user/1000
DEBUGINFOD_URLS=https://debuginfod.ubuntu.com 
XDG_DATA_DIRS=/usr/share/ubuntu:/usr/share/gnome:/usr/local/share/:/usr/share/:/var/lib/snapd/desktop
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
GDMSESSION=ubuntu
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus
OLDPWD=/home/nicod/Downloads
_=./envVarSetUID
```

---

### Path environment and set uid 

we can capitalize on a set uid's weakness with passing down environment variables to child processes with the vulnerability of `system()` to make a root shell call a malicious program 
```
nicod@nicod-Standard-PC-Q35-ICH9-2009:~$ sudo mv seed /home/seed
nicod@nicod-Standard-PC-Q35-ICH9-2009:~$ cd /home
nicod@nicod-Standard-PC-Q35-ICH9-2009:/home$ ls
nicod  sally  seed
nicod@nicod-Standard-PC-Q35-ICH9-2009:/home$ cd seed
nicod@nicod-Standard-PC-Q35-ICH9-2009:/home/seed$ ls
ls  malicous.c
nicod@nicod-Standard-PC-Q35-ICH9-2009:/home/seed$ cd ~/Downloads/Labsetup/
nicod@nicod-Standard-PC-Q35-ICH9-2009:~/Downloads/Labsetup$ ./malIThink 
my Malicious softwareLESSOPEN=| /usr/bin/lesspipe %s
USER=nicod
XDG_SESSION_TYPE=wayland
SHLVL=1
HOME=/home/nicod
OLDPWD=/home/seed
DESKTOP_SESSION=ubuntu
GNOME_SHELL_SESSION_MODE=ubuntu
GTK_MODULES=gail:atk-bridge
SYSTEMD_EXEC_PID=2790
GSM_SKIP_SSH_AGENT_WORKAROUND=true
DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus
COLORTERM=truecolor
DEBUGINFOD_URLS=https://debuginfod.ubuntu.com 
IM_CONFIG_PHASE=1
WAYLAND_DISPLAY=wayland-0
LOGNAME=nicod
_=./malIThink
MEMORY_PRESSURE_WATCH=/sys/fs/cgroup/user.slice/user-1000.slice/user@1000.service/session.slice/org.gnome.Shell@wayland.service/memory.pressure
XDG_SESSION_CLASS=user
ANY_NAME=Nico D is my name
USERNAME=nicod
TERM=xterm-256color
GNOME_DESKTOP_SESSION_ID=this-is-deprecated
PATH=/home/seed:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin:/snap/bin
SESSION_MANAGER=local/nicod-Standard-PC-Q35-ICH9-2009:@/tmp/.ICE-unix/2759,unix/nicod-Standard-PC-Q35-ICH9-2009:/tmp/.ICE-unix/2759
XDG_MENU_PREFIX=gnome-
GNOME_TERMINAL_SCREEN=/org/gnome/Terminal/screen/a0d7a018_d635_4b55_b792_cb7291d9bab1
GNOME_SETUP_DISPLAY=:1
XDG_RUNTIME_DIR=/run/user/1000
DISPLAY=:0
LANG=en_US.UTF-8
XDG_CURRENT_DESKTOP=ubuntu:GNOME
XMODIFIERS=@im=ibus
XDG_SESSION_DESKTOP=ubuntu
XAUTHORITY=/run/user/1000/.mutter-Xwaylandauth.L5QMF3
LS_COLORS=rs=0:di=01
GNOME_TERMINAL_SERVICE=:1.135
SSH_AUTH_SOCK=/run/user/1000/keyring/ssh
SHELL=/bin/bash
QT_ACCESSIBILITY=1
GDMSESSION=ubuntu
LESSCLOSE=/usr/bin/lesspipe %s %s
QT_IM_MODULE=ibus
PWD=/home/nicod/Downloads/Labsetup
XDG_CONFIG_DIRS=/etc/xdg/xdg-ubuntu:/etc/xdg
XDG_DATA_DIRS=/usr/share/ubuntu:/usr/share/gnome:/usr/local/share/:/usr/share/:/var/lib/snapd/desktop
MEMORY_PRESSURE_WRITE=c29tZSAyMDAwMDAgMjAwMDAwMAA=
VTE_VERSION=7800
```
what we did to get this output was place an executable in /home/seed/ called 'ls' that just prints the environment variables there. since the set uid program is owned by root the effective id is also 0 giving the first ls program found on the path, which will be in /home/seed because we manually prepeneded it.