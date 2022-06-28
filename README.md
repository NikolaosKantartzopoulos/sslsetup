### NOIP - DNS and SSL provider
*Using https://www.noip.com/*<br>
  Username: nkantartzopoulos@gmail.com<br>
  Password: Dung&Dr@g_89<br>
I have linked my WAN address to nklan.ddns.net<br>
Because my ISP blocks the 80 port, I use 4444 and redirect it to port 80 using Port 80 redirect option.<br>


### Router
*Forward the folowing ports to my PC* (Static IP 192.168.1.5)<br>
WAN 80 Port to LAN 80 Port<br>
WAN 443 Port to LAN 443 Port<br>
WAN 4444 Port to LAN 4444 Port<br>

### PC
*sudo ufw status verbose*
```
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
80                         ALLOW IN    Anywhere                  
4444                       ALLOW IN    Anywhere                  
443                        ALLOW IN    Anywhere                  
22                         ALLOW IN    Anywhere                  
80 (v6)                    ALLOW IN    Anywhere (v6)             
4444 (v6)                  ALLOW IN    Anywhere (v6)             
443 (v6)                   ALLOW IN    Anywhere (v6)             
22 (v6)                    ALLOW IN    Anywhere (v6) 
```

### Apache Server

Used *a2ensite nklan.conf*
Enabled *a2enmod ssl*

#### nklan.conf
```
<VirtualHost *:80> 
      ServerName nklan.ddns.net
      Redirect permanent / https://nklan.ddns.net/
</VirtualHost>

<VirtualHost *:4444> 
      ServerName nklan.ddns.net
      Redirect permanent / https://nklan.ddns.net/
</VirtualHost>

<VirtualHost *:443>
    ServerName nklan.ddns.net
    DocumentRoot /var/www/nklan
    <Directory /var/www/nklan>
        Options -Indexes +FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    SSLEngine on 

      SSLCertificateFile /etc/ssl/certs/nikey.pem
      SSLCertificateKeyFile /etc/ssl/private/nikey.key

		<FilesMatch "\.(cgi|shtml|phtml|php)$">
				SSLOptions +StdEnvVars
		</FilesMatch>
    
		<Directory /usr/lib/cgi-bin>
				SSLOptions +StdEnvVars
		</Directory>

</VirtualHost>
```

#### ports.conf
```
Listen 80
Listen 443
Listen 4444
```

#### apache2.conf
Posted as a different file in main directory of repository
