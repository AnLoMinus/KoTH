#  Machine name: SHREK
    
This is first and relatively easy machine, But beaware this things have too many entries to keep an eye on, Best Idea for defending this is by just killing the shells. Again I am not posting the methods that are 'technically' better, I am posting methods that will be easiest to do and will get you win.
Target is to win while being inside the rules. This is not an exam, there are no wrong answers.
As the saying goes, *If it works, don't touch it.* 

1. Initial gobuster scan revealed that `robots.txt` file contains an abnormal entry, When we navigate to it, we find the entire RSA key.

![image](https://user-images.githubusercontent.com/54495695/81495768-495e6f80-92d0-11ea-8ab8-daab1abe3cf3.png)

2. Copy the key, paste it in a file, give the file necessary permissions.<br />
Assuming you made the RSA key file with the name `id_rsa`, follow these commands.<br />
`chmod 600 id_rsa`<br />
`ssh -i id_rsa shrek@<IP ADDRESS OF MACHINE>`<br />
This will give you a shell to shrek.<br />

3. After scanning the machine with linPEAS.sh, We found tha there is a gdb vulnerabilty in the box, using GTFObins, We use the following commands to do Privilage escalation.<br />
`gdb -nx -ex 'python import os; os.execl("/bin/sh", "sh", "-p")' -ex quit`<br />
  #### YOU ARE ROOT. NOW DEFEND YOUR TITILE.<br />
    
