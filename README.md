#SECURE A SERVER

In this tutorial we will walk you through the best security practices to secure your server.



## Ubuntu
### Firewall . ufw
   - Enable ufw `sudo ufw enable`
   - Limit 22 so you won't lock out your self `sudo ufw limit 22/tcp`
   - Allow web server `sudo ufw allow 80/tcp`
   - Allow ssl `sudo ufw allow 443/tcp`
   - Check status `sudo ufw status`
   - Change default all incoming `sudo ufw default deny incoming`
   - Change default all outgoing `sudo ufw default allow outgoing`