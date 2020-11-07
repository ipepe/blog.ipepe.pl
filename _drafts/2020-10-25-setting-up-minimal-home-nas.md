---
tags: zfs zerotier docker ubuntu homelab nas
---

# Setting up minimal home NAS

This guide is brought to You my MicroSD card that always dreamed to become a brick and yesterday her dreams finally became a reality. 

## Researching mirror on Root partition solutions

Because I didn't want to go through that situation again I quickly researched how to setup mirrored root partition for system. I quickly found two new 32GB MicroSD cards. I put one into MicroSD slot on motherboard and second went through USB-MicroSD card adapter.
 
As a first cadidate I nomitated ZFS because I already have quite "advanced" setup (6x 2TB Patriot SSD) for my data. Up to this point I didn't bother for anything in regards system partition. I suspected that some mirroring solution would bring complexity to installation process and also could be problematic for my HP MicroServer to boot from.

After reading a bit about ZFS on Root and even trying it out in practice, I decided that setup is too complicated (as expected). As a second choice candidate went BTRFS but that also have similar complexity guides on setting up root partition on mirrored drives.

I noticed that You can setup LVM in mirror mode but as my time was running short I decided to go for old MDADM configuration with hopes that it will be enough.

The good news was also a fact that in Ubuntu 20.04 they added ability to setup SWAP as file on root partition and there was also something about boot parittion that allowed You to configure only 1 partition in "Custom storage layout" 

## Setting up MDADM for Root partition

- Select "Custom storage layout" when you reach the storage step of the installer
- If the disks have existing partitions, click on each disk under AVAILABLE DEVICES and then select REFORMAT. This will (temporarily) wipe out the partitions.
- Now select the 1st disk to add as "boot" disk (same menu that had REFORMAT in).
- Do the same with the 2nd disk.
- You should now see two 1.000M bios_grub partitions created under USED DEVICES. These small partitions will be used by GRUB for booting the server.
- Now, the trick to setup a softRAID array is to create partitions for / on each disk, but WITHOUT formatting them (an as such, there won't be a mount point for now).
- So go ahead and "Add GPT Partition" on the 1st disk, do not set a size (so it uses all available) and choose to `Leave it unformatted`. Do the same for the 2nd disk. Under each disk on AVAILABLE DEVICES you will now see "partition 2".
- Now click on "Create software RAID (md)" under AVAILABLE DEVICES. We'll create the first softRAID partition (md0) by selecting the two "partition 2" entries (one from each disk). Click "Save".
- We now have softRAID volume in AVAILABLE DEVICES which will now format as the actual softRAID partitions. So select md0 and then "Add GPT Partition", format as EXT4 and mount on /.
- now md0 softRAID partitions will now appear under USED DEVICES and you are ready to proceed with Ubuntu's installation.
- At the very bottom, you should now see "Done" enabled so hit it and proceed.

## Setting up services on system partition with Ubuntu 20.04

Next was bringing everything back up. As my system configuration basis I use:
 * openssh-server (already installed as basic package in ubuntu)
 * zfs
 * zerotier
 * docker (with docker-compose)

Following steps will be focusing on setting them up again but first we need to make sure our system is up to date with:

 * `sudo apt update`
 * `sudo apt upgrade`

### Installing ZFS

 * `sudo apt install zfsutils-linux`
 * `zfs --version`
    * as of writing for me it is `zfs-0.8.3-1ubuntu12.4` 
 * `systemctl enable zfs.target zfs-import.service zfs-mount.service`
 * `zpool import ZPOOL-NAME`
    * Because I have already existing ZFS pool. If You want 

### Installing docker
 * Install Docker Engine
     * `sudo apt install docker.io`
     * `sudo systemctl enable docker`
     * `sudo systemctl start docker`
     * `sudo usermod -aG docker $USER`
     * `sudo systemctl status docker`
 * Install Docker Compose
    * `sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`
    * `sudo chmod +x /usr/local/bin/docker-compose`
 * Reconfigure Docker for Overlay2
    * `sudo systemctl stop docker`
    * `sudo rm -rf /var/lib/docker`
    * `sudo sed -i -e '/^ExecStart=/ s/$/ --storage-driver=overlay2/' /lib/systemd/system/docker.service`
    * `sudo systemctl daemon-reload`
    * `sudo service docker restart`
    * `sudo systemctl restart docker`
    * `sudo docker info | grep Storage\ Driver`
        * Confirm that output says:` Storage Driver: overlay2`

### Installing zerotier
 * `curl -s https://install.zerotier.com | sudo bash`
 * `sudo cat /var/lib/zerotier-one/authtoken.secret >> ~/.zeroTierOneAuthToken`
 * `chmod 0600 ~/.zeroTierOneAuthToken`
 * `zerotier-cli join NETWORK-UUID`
    * `NETWORK-UUID` is Your network identifier
 * Confirm device in Zerotier web interface

