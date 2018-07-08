---
layout: post
title: Proxmox - Remount NFS shares when storage server comes back up
---

I don't exactly know the problem, but it either is Proxmox or NFS. Somehow Proxmox has problems when a NFS share goes offline and then comes back online again. You often still can't see it in the Web UI then.

There is a simple solution though! Just remount the shares!

One way might be to create a simple bash script in the root dir of each proxmox node with the following content:

```
#!/bin/bash
list=$(ls /mnt/pve)

for i in $list
do
        status=$(ls /mnt/pve/$i 2>&1)

        if [[ $status =~ .*Stale.* ]]
                then
                umount /mnt/pve/$i
        fi
done
```
