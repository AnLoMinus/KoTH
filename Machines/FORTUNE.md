#  Machine name: FORTUNE

Now this is new machine, Released very recently, <br /> 
And made it hard for me to post direct commands, Why?<br /> 
Heres why, In this machine, there's a thing called autogen script, that regenrates everything at every reset. That means direct credentials doesn't work anymore. So you have to follow the instructions and do everything manually.<br /> 
Let's Hack:<br /> 


1. Initial nmap scans revealed that theres a netcat port open at 3333. <br /> 
    ![image](https://user-images.githubusercontent.com/54495695/81497074-b9252800-92d9-11ea-9e85-e727773fc41c.png)
##### UPDATE, you can skip next 2 steps and directly use the command in Shortcut Note.
2. When we connect to it, It gives out a weird base64 hash, After fiddling around, I found that it is base data of a zip file, so we use this [Site](https://base64.guru/converter/decode/file).<br /> 
    Copy the base64 hash to this site, and it will generate a file named application.zip.<br /> 
    
3. Now when we try to open the file, The file needs a password, Just crack this file using fcrackzip and wordlist rockyou.txt.<br /> 
    `fcrackzip -v -u -D -p ~/wordlists/rockyou.txt application.zip`<br /> 
   Once you have the password, unzip it.<br /> 
   `unzip application.zip`<br /> 
  ##### Shortcut Note:  MAKE SURE TO DO THE FOLLOWING EDITS: 
  $IP = IP of KoTH box  <br />
  $location = address of your rockyou wordlist <br />
  Copy the hash in a file, <br />
  
  `cat file.txt | base64 -d  > test.zip; unzip -P  (fcrackzip -v -u -D -p $location/rockyou.txt test.zip | grep "pw" |awk '{print $5}') test.zip; cat creds.txt`
  
   You get a file named creds.txt, Inside it we have the login details of user named `fortuna`. Lets GO.<br /> 
4. Using the creds, <br /> 
    `ssh fortuna@<BOX IP>`<br /> 
5. Now that we have the shell, We can work on Privilage escalation.<br /> 
    After linpeas and basic test, I found that:<br /> 
        5.1 We as fortuna are in sudoers list.<br /> 
        5.2 And we also have `pico` in the `sudo -l` list.<br /> 
        
6. We can simply edit the `/etc/sudoers/` file to give us ALL permissions to run sudo.<br /> 
7. Using this command:<br /> 
    `sudo pico /etc/sudoers`<br /> 
   Replace `pico` in sudoers file with `ALL`.<br /> 
8. Now you can just do, `sudo su` and you are root.<br /> 

#### You are ROOT, now defend your title.
   
