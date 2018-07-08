---
layout: post
title: PiHole - Adding your own DNS entries
---

So I use piHole as my DNS server and pfSense does all the DHCP stuff. I use a Domain I bought purely internally! Even for oustide access, I use a different domain. Now I want to make sure, that going to my domain `example.com` will lead me to my main dashboard in the network. To do this I changed some dnsmasq stuff. Keep in mind that this will only work, as long as piHole uses dnsmasq... But I will hopefully update this post accordingly, if there is a change!

First of all, add a new dnsmasq file. You can not edit the original one, as that one will be overwritten on each reboot!
```
sudo nano /etc/dnsmasq.d/01-mydns.conf
```

In that file add this line:
```
address=/example.com/IP-of-said-service
# ctrl+x, j and enter to save
```

Then run the following commands to activate your changes:
```
pihole restartdns
sudo reboot
```

That is all! Have fun doing your DNS entries.
