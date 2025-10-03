# Command Line Practice
`sudo apt update` - get available updates

`sudo apt upgrade` - apply updates to pc

`sudo reboot` - reboot pc to set changes

`sudo su -` - switch user to root
- you can verify by seeing the `#` instead of `$`
- it is bad to stay logged in as root bc there are no warnings saying do you want to do this
- since it doesn't require a passwd to run commands another user can pick up where you left off

`sudo useradd bobby` - makes new user bobby with no password and no home dir
- `-m` flag adds the home dir for the user
- `-p` flag allows for xtra argument of passwd

`sudo adduser sally` - more a TUI to make a user, Prompts:
- contact info
- set password
- Automatically makes a home Dir

`su sally` - switch user to sally
- requires sally's passwd
- my current home dir isn't `~` but is now `/home/nicod`
- the user is now sally on the right: **sally** `@nicod-Standard-PC-Q35-ICH9-2009:/home/nicod`

---
When logged in as Sally if I run `sudo useradd bob` I get hit w/ sally isn't in the sudoers group. Therefore I cannot make a new user as Sally (This Good security)

`exit` - quit the current shell
- logs you out of the user you `su` into if thats the case

`sudo passwd sally`- allows a sudoer to change the passwd of another user

`id` - get current user's id
- can run `id <userName>` to get another users id
- my id is 1000


## Group
`groups  nicod` - get groups nicod belongs to

- belongs to group called: nicod adm cdrom sudo dip plugdev users lpadmin


`sudo usermod -aG sudo sally` - give sally sudo power; now she can add new users

`sudo useradd mike` - add user mike no password; no home dir

`sudo groupadd cybersec` - create new group called cybersec

`sudo usermod -aG cybersec sally`- add sally to cybersec groups

`groups sally` - check sally's groups shes a part of
- part of groups sally ,sudo, and cybersec

## Permission ACL's

`mkdir lab1` - make new directory called lab1

`ls -dl lab1` - list the permissions of directory "lab1"
- `-d` get permissions of a directory
- `-l` get all permissions

`drwxrwxr-x 2 nicod nicod 4096 Oct  1 20:30 lab1`

the owner and group owner for this directory is nicod. User has read write and execute permissions. Group has read write and execute. Others hace only read and execute

`nano helloWorld.sh` - create and start typing a file called helloWorld.sh; this is a shell script
-  contents of file =>`#!/bin/bash \n echo "Hello World"`

`chmod 744 helloWorld.sh` - user can rwx, group and others can only read; making file executable

`./helloWorld.sh` - execute script for output of "Hello World"

`chmod g+wx helloWorld.sh` - give group write and execute permissions

`ls -la` - get permissions for all items in current directory 

`getfacl helloWorld.sh` - view ACL of this file

Output:
```
# file: helloWorld.sh
# owner: nicod
# group: nicod
user::rwx
group::rwx
other::r--
```

`setfacl -m u:sally:rw helloWorld.sh` - Give sally permission to read and write to this file.

New output from `getfacl helloWorld.sh`
```
# file: helloWorld.sh
# owner: nicod
# group: nicod
user::rwx
user:sally:rw-
group::rwx
mask::rwx
other::r--
```
