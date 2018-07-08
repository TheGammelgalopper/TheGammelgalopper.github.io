---
layout: post
title: testpost
---

If you have an odroid XU4 and don't care about noise or you use another fan, it might be wise to set the fan speed to a 100%. This way you always have optimal cooling!

This guide works for `Ubuntu 16.04.4`. Make sure to update the kernel first!
```
apt update
apt upgrade
apt dist-upgrade
apt install linux-image-xu3 # be sure to answer "NO" in popup menu!!!
reboot
```

Then edit `/etc/rc.local` and add these two lines:
Get Temps via:
echo 0 > /sys/devices/platform/pwm-fan/hwmon/hwmon0/automatic # sets fan to manual
echo 255 > /sys/devices/platform/pwm-fan/hwmon/hwmon0/pwm1 # sets speed to 100%
```

You can get the temps via:
```
cat /sys/devices/virtual/thermal/thermal_zone0/temp
```
