---
layout: page
title: "Virtual Lab"
permalink: /compute_node/
---

## Setting up the Compute Node

October 29, 2020

The goal is to have one test machine with enough ram to run docker 
swarm, microk8s and openstack (slowly).  That is, the processing 
speed of each container or VM isn't important, but the ability to simulate
networks of them running at the same time is.

I've been having trouble getting an old desktop to boot from USB 
because it is a UEFI motherboard.
With this particular BIOS, the trick to booting from USB at all 
is to hit F2 at boot, then F8.  I don't seem to be able to configure
the boot order to pick up the USB stick otherwise.
Within the setup program, you can pick the drive to boot from and the USB stick appears twice, once without UEFI, the other with. 
I think I chose to boot from the UEFI version of the detected 2G USB drive.

This desktop had a not too old install of kubuntu running in desktop mode.
I'm more comfortable with a no-frills, server ubuntu install, and wanted
a procedure where I could periodically reformat the drive back to a base image
(cattle, not pets).  This is that procedure.

### Installing Ubuntu

The downloaded Ubuntu desktop ISO is larger than 2.5GB, and:

1. My free USB stick is 2GB
2. I don't really need a desktop on the compute server node.  I'll ssh in and run web services for any needed GUI.

So I downloaded the latest 20.04 Ubuntu server install.

The trick to creating a bootable USB drive for EFI is to simply 

    dd if=ubunto.iso of=/dev/sde bs=4096

That is, copy the iso image onto the root (/dev/sde not /dev/sde1 in my case) 
of where the USB drive mounted.
I used dmesg to find out which letter it mounted as and fdisk -l 
to verify it was the 2GB drive.
Note: after the dd, fdisk -l shows that there are two partitions, 
one on /dev/sde1 (empty) and the main EFI one is /dev/sde2.

On boot, from this USB stick, the compute server tells me a later 
updater is available, so I chose to download and run that.  
This is a good sign the built-in ethernet card is detected and working and
is on the network via DHCP.
Other than that I took the defaults, chose to overwrite the disk using 
their defaults.  One gotcha was that my caps-lock key got on and when 
it came time to choose a user name 'd' was 'D', etc., and
that's not allowed.  
Chose the user `user` and set the password for now.

After that, when given a list of default packages to install, I 
installed docker and microk8s.
Once the install is finished and rebooted, I plan to also try 
to install OpenStack.  This time I'll try microstack for an openstack flavor
as suggested on the ubuntu site.

## Next Steps

As usual, once the install is completed and you reboot and log in, I do.

{% highlight bash %}
sudo apt update
sudo apt dist-upgrade
{% endhighlight %}

### OpenStack Notes

Then on to installing Openstack using the [microstack](/microstack/) snap.

### Docker Notes

For some reason the docker group didn't get created as part of the base
install..
As root, I had to:

{% highlight bash %}
addgroup docker
usermode -G docker user
chgrp docker /var/run/docker.sock
{% endhighlight %}

So that the user `user` can run docker.  I'm noting it here because it may
be necessary to repeat these steps if I "re-pave" the compute node 
periodically as planned.
