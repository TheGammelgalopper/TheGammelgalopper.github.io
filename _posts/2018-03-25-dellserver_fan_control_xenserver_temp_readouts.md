---
layout: post
title: Dell Server Fan Control and Xenserver Temperature readouts
---

So like everybody else I want to make my Dell servers quieter... I have found [this nice thread](https://www.reddit.com/r/homelab/comments/7xqb11/dell_fan_noise_control_silence_your_poweredge/) to do so!
You will first of all have to enable manual fan control. Then you can set your desired fan speed and also read out desired speeds and temps. Keep in mind, that you won't be able to control the PSU fans, those might still be loud...

To enable manual control connect to some linux machine and perform this command:

`ipmitool -I lanplus -H <iDRAC-IP> -U <iDRAC-USER> -P <iDRAC-PASSWORD> raw 0x30 0x30 0x01 0x00`

Disable with this command:

`ipmitool -I lanplus -H <iDRAC-IP> -U <iDRAC-USER> -P <iDRAC-PASSWORD> raw 0x30 0x30 0x01 0x01`

Changing the fan speed:

`ipmitool -I lanplus -H <iDRAC-IP> -U <iDRAC-USER> -P <iDRAC-PASSWORD> raw 0x30 0x30 0x02 0xff 0x<aa>`

(The <aa> stands vor the hex value of the decimal percent value. So 20% fan speed would be 14)

To get temperatures and fan speeds:

`ipmitool -I lanplus -H <iDRAC-IP> -U <iDRAC-USER> -P <iDRAC-PASSWORD> sensor reading "Ambient Temp" "FAN 1 RPM" "FAN 2 RPM" "FAN 3 RPM"`

Then I also wanted to be able to see CPU temperatures, this is sadly not possible with iDRAC6 of the 11th Gen Dell servers (with iDRAC 7 it is possible...)
As I am running XenServer, I had to perform these commands, to enable the CentOS repos and install lm-sensors:

```
vi /etc/yum.repos.d/CentOS-Base.repo
// i + uncomment all the repos and set enabled=1 + esc :wq
yum -v repolist all
yum install lm_sensors
sensors-detect
// say yes for everything
```

Then you can just type `sensors` to see the CPU temps!

