# NOIP - DNS and SSL provider
*Using https://www.noip.com/*
  Username: nkantartzopoulos@gmail.com
  Password: Dung&Dr@g_89
I have linked my WAN address to nklan.ddns.net
Because my ISP blocks the 80 port, I use 4444 and redirect it to port 80 using Port 80 redirect option.


# Router
*Forward the folowing ports to my PC* (Static IP 192.168.1.5)
WAN 80 Port to LAN 80 Port
WAN 443 Port to LAN 443 Port
WAN 4444 Port to LAN 4444 Port

# PC
*sudo ufw status verbose*
'''
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
'''
