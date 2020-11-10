#SECURE A SERVER

In this tutorial we will walk you through the best security practices to secure your server.


| OS                                                                                                   | Android                                                                                                       |
| ----------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| ![RedHat](https://github.com/iloveyii/secure-a-server/blob/master/redhat.jpg) |  |



## Ubuntu
### Firewall . ufw
   - Enable ufw `sudo ufw enable`
   - Limit 22 so you won't lock out your self `sudo ufw limit 22/tcp`
   - Allow web server `sudo ufw allow 80/tcp`
   - Allow ssl `sudo ufw allow 443/tcp`
   - Check status `sudo ufw status`
   - Change default all incoming `sudo ufw default deny incoming`
   - Change default all outgoing `sudo ufw default allow outgoing`
   
### Login using ssh keys
   - `ssh-keygen -t rsa`
   - `cd ~/.ssh `
   - Copy public key to server `ssh-copy-id -i id_rsa.pub user@ip`
   - Login `ssh user@ip`
   - Disable login using password `nano /etc/ssh/sshd_config` .
   ```bash
    ChallengeResponseAuthentication no
    PasswordAuthentication no
    UsePAM no
    PermitRootLogin no
```


### System level
   - `sudo nano /etc/sysctl.conf`
   - Block ip spoofing attack, uncomment 
   ```bash
      net.ipv4.conf.default.rp_filter=1
      net.ipv4.conf.all.rp_filter=1
```
   - Block ICMP ping
   ```bash
   net.ipv4.conf.all.accept_redirects=0
   net.ipv6.conf.all.accept_redirects=0

```
   - We are not a router `net.ipv4.conf.all.send_redirects=0`
   `net.ipv4.conf.all.accept_source_route=0`
   `net.ipv6.conf.all.accept_source_route=0`
   - Logon martians packets
   `net.ipv4.conf.all.log_martians=1`
   - Check status `sudo sysctl -p`
   - Spoof file `nano /etc/host.conf` and paste
   ```bash
    order bind,hosts
    nospoof on
```
### Ban
   - Ban a malicious user `sudo apt install fail2ban`
   - Enable it `sudo systemctl enable fail2ban`
   - Start it `sudo systemctl start fail2ban`
   - Check status `sudo systemctl status fail2ban`
   - Open ports `sudo netstat -tunlp`
   