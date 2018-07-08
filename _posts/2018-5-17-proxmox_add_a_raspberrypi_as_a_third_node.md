---
layout: post
title: Proxmox: Add a Raspberry Pi as a third node
---

So in a home environment there often are not enough servers to run a full Proxmox cluster. I personally only have two servers which are being used as proxmox nodes. One is my production server where all those important services live and the other one is being used for testing. As I normally shutdown my test host when I don't need it, the cluster then moves in a less than ideal state... Why? Because Quorum!

Quorum is proxmox's way of determining the state of the cluster. Each cluster member (node) gets one vote. The cluster needs 51% percent of votes to work normally. With less than enough votes the cluster goes into a read-only state. So if you have two nodes and shut one down, the other one goes into the barely usable state... With three nodes and one going down your cluster continues to work normally.

To bypass that problem there is one very simple solution. You can use a raspberry pi to simulate a proxmox node to get a cluster of 3 nodes. You basically only install the service that manages the communication between the nodes. The other nodes then think that there is a third node available, although there is no real third node. There already is a wiki entry on the proxmox website for this. This entry however is somewhat outdated...

My personal configuration includes a corosync network (10.10.11.0/24) on a dedicated network interface as described and recommended here. I use a Raspberry Pi 3 B+ with Debian Stretch (9) and a USB to Ethernet adapter for the corosync network.

First do your general Pi configuration:
set correct hostname
change password for pi user
enable root login with raspi-config
set root password
permit ssh root login in /etc/ssh/sshd_config ("yes", then /etc/init.d/ssh restart)
update system
Then perform these 10 steps to "add" your Pi to the cluster:
connect second network interface and add ip in 10.10.11.0/24 range
make sure that the hosts config in /etc/hosts is equal between all proxmox hosts
Install corosync with apt-get install corosync
copy over one existing corosync config from another host via scp <ipofexistingnode>:/etc/corosync/* /etc/corosync
add the pi to the corosync config as a new node, set the config version to something higher
copy this new corosync config to the other hosts (you can use scp)
restart corosync on the first node in the config (ssh <ipOfFirstNode> systemctl restart corosync)
restart corosync on the other nodes in ascending order
start corosync on the pi with systemctl start corosync
run corosync-quorumtool to check Qourum! Shutdown one node to test functionality, you might need to restart corosync if it doesn't work on first try!
Et voilà, you should have three nodes showing up in the gui as well! Keep in mind that the Pi will always show a red "X", as there is nothing installed which would enable virtualization. I know that this solution is far from pretty and not recommended, but for home use it completely does its job...

WARNING
pve-manager (the virtualization manager) is missing so don't add the pi to /etc/pve/corosync.conf
If a new node is added the pve-manager will overwrite /etc/corosync/corosync.conf
I give no guarantee so everything above is at your own risk!
