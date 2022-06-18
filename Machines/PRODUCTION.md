# Machine name: PRODUCTION

 This machine is one of the easist ones.<br /> 
 ![image](https://user-images.githubusercontent.com/54495695/82766838-ff34cc80-9e3f-11ea-88e9-bfe5ed4e48c6.png)
 1. Basic enumeration will get you the password/ssh id_rsa key of user Ashu.<br /> 
 2. Once you are in machine with user as Ashu.<br /> 
    Check the `sudo -l`, you will see that you can run `su` on for user skiddy without password.<br /> 
 3. After, `sudo su skiddy` , You are in the skiddy shell.<br /> 
 4. We don't need to enumerate this machine anymore. The `sudo -l` can show that we can run `git` as sudo.<br /> 
 5. Using GTFObins, we see that the following commands can be used to give us root shell.<br /> 
    `sudo git -p help config`<br /> 
    `!/bin/sh`<br /> 
  Now, `id`, Voila, You are root.<br /> 
  
  P.S. Food for thought, there are two interesting ports open on machine, see if you can setup backdoors for you ;)

#### You are ROOT, now defend your title.<br /> 
