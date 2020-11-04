---
layout: page
title: Installing MicroStack
permalink: microstack
---

## Base OS Install

October 29, 2020

First, I reinstalled ubuntu on the test machine.  Got the 20.04 server
ISO, burned to a free 2GB usb stick and
installed, update, dist-upgrade.  See [compute node](/compute_node) for more
details.

# Openstack Install

I'm trying the ubuntu-approved method of installing microstack on a single-node.
The first step is to install the snap

{% highlight bash %}
sudo snap install microstack --devmod --beta
{% endhighlight %}

Yikes, didn't work, but perhaps becuase the update/dist-ugprade were in progress?


{% highlight bash %}
020-10-29T17:44:18Z INFO snap "microstack" has bad plugs or slots:
hugepages-control (unknown interface "hugepages-control")
2020-10-29T17:45:40Z INFO snap "microstack" has bad plugs or slots:
hugepages-control (unknown interface "hugepages-control")
error: cannot perform the following tasks:
- Run install hook of "microstack" snap if present (run hook "install": 
-----
+ set-default-config.py
+ snapctl stop --disable microstack.nginx
+ snapctl stop --disable microstack.keystone-uwsgi
+ snapctl stop --disable microstack.placement-uwsgi
+ snapctl stop --disable microstack.nova-api
+ snapctl stop --disable microstack.nova-compute
+ snapctl stop --disable microstack.nova-conductor
+ snapctl stop --disable microstack.nova-api-metadata
+ snapctl stop --disable microstack.nova-spicehtml5proxy
+ snapctl stop --disable microstack.nova-scheduler
+ snapctl stop --disable microstack.neutron-api
+ snapctl stop --disable microstack.glance-api
+ snapctl stop --disable microstack.registry
+ snapctl stop --disable microstack.cinder-uwsgi
+ snapctl stop --disable microstack.ovsdb-server
+ snapctl stop --disable microstack.neutron-ovn-metadata-agent
+ snapctl stop --disable microstack.ovn-ovsdb-server-sb
+ snapctl stop --disable microstack.ovn-ovsdb-server-nb
+ snapctl stop --disable microstack.ovs-vswitchd

    <aborted>
    -----)
{% endhighlight %}

Second try...

{% highlight bash %}
sudo snap install microstack --devmode --beta
{% endhighlight %}

Yields:

{% highlight bash %}
microstack (beta) ussuri from Canonical✓ installed
WARNING: There is 1 new warning. See 'snap warnings'.
user@compute:~$ snap warnings
last-occurrence:  today at 17:45 UTC
warning: |
  snap "microstack" has bad plugs or slots: hugepages-control (unknown interface
  "hugepages-control")
{% endhighlight %}

I had tried to install devstack from Red Hat to get Openstack prior
to this.  It created a stack user in /opt/stack and had me run devstack.sh,
but that didn't ever work.

Let's see if this creates /opt/stack and the stack user for us.  Nope.

## Microstack init

Ignoring the above warning for now.

{% highlight bash %}
sudo microstack init --auto --control
{% endhighlight %}

This seems to have worked better.

{% highlight  bash %}
2020-10-29 17:57:34,518 - microstack_init - INFO - Configuring clustering ...
2020-10-29 17:57:34,811 - microstack_init - INFO - Setting up as a control node.
2020-10-29 17:57:40,345 - microstack_init - INFO - Configuring networking ...
2020-10-29 17:57:56,383 - microstack_init - INFO - Opening horizon dashboard up to *
2020-10-29 17:57:59,736 - microstack_init - INFO - Waiting for RabbitMQ to start ...
Waiting for 192.168.21.222:5672
2020-10-29 17:58:25,853 - microstack_init - INFO - RabbitMQ started!
2020-10-29 17:58:25,854 - microstack_init - INFO - Configuring RabbitMQ ...
2020-10-29 17:58:28,748 - microstack_init - INFO - RabbitMQ Configured!
2020-10-29 17:58:28,847 - microstack_init - INFO - Waiting for MySQL server to start ...
Waiting for 192.168.21.222:3306
2020-10-29 17:58:28,864 - microstack_init - INFO - Mysql server started! Creating databases ...
2020-10-29 17:58:37,477 - microstack_init - INFO - Configuring Keystone Fernet Keys ...
2020-10-29 18:03:55,932 - microstack_init - INFO - Bootstrapping Keystone ...
2020-10-29 18:04:25,470 - microstack_init - INFO - Creating service project ...
2020-10-29 18:04:36,411 - microstack_init - INFO - Keystone configured!
2020-10-29 18:04:36,578 - microstack_init - INFO - Configuring the Placement service...
2020-10-29 18:05:18,019 - microstack_init - INFO - Running Placement DB migrations...
2020-10-29 18:06:04,610 - microstack_init - INFO - Configuring nova control plane services ...
2020-10-29 18:06:35,144 - microstack_init - INFO - Running Nova API DB migrations (this may take a lot of time)...
2020-10-29 18:10:03,202 - microstack_init - INFO - Running Nova DB migrations (this may take a lot of time)...
2020-10-29 18:30:17,092 - microstack_init - INFO - Creating default flavors...
2020-10-29 18:31:07,421 - microstack_init - INFO - Configuring nova compute hypervisor ...
2020-10-29 18:31:08,930 - microstack_init - INFO - Configuring the Spice HTML5 console service...
2020-10-29 18:31:09,727 - microstack_init - INFO - Configuring Neutron
Waiting for 192.168.21.222:9696
2020-10-29 18:44:50,972 - microstack_init - INFO - Configuring Glance ...
Waiting for 192.168.21.222:9292
2020-10-29 18:47:48,590 - microstack_init - INFO - Adding cirros image ...
2020-10-29 18:47:56,906 - microstack_init - INFO - Creating security group rules ...
2020-10-29 18:48:18,528 - microstack_init - INFO - Configuring the Cinder services...
2020-10-29 18:50:17,244 - microstack_init - INFO - Running Cinder DB migrations...
2020-10-29 18:52:58,401 - microstack_init - INFO - restarting libvirt and virtlogd ...
2020-10-29 18:53:22,702 - microstack_init - INFO - Complete. Marked microstack as initialized!
{% endhighlight %}

## Microstack Usage

Unlike the devstack approach where the passwords are entered into 
a local.conf file before installation, microstack must be managing 
all of its own passwords.  So, to test the install
go to port 80 on the local IP and log in as 'admin'.  The password is:

{% highlight bash %}
sudo snap get microstack config.credentials.keystone-password
{% endhighlight %}

You can also use the CLI, but note that the entry point is 
`microstack.openstack`, try
`microstack.openstack --help` to start.  
Also, `microstack.openstack catalog list` gives internal, external and admin API endpoints for each OpenStack service.

## Microstack Testing

As always, the test is to get a VM running. Microstack has a shortcut for this:

{% highlight bash %}
microstack launch cirros --name test
{% endhighlight %}

Gives:

{% highlight bash %}
Creating local "microstack" ssh key at /home/user/snap/microstack/common/.ssh/id_microstack
Launching server ...
Allocating floating ip ...
Server test launched! (status is BUILD)

Access it with `ssh -i /home/user/snap/microstack/common/.ssh/id_microstack cirros@10.20.20.191`
You can also visit the OpenStack dashboard at http://10.20.20.1:80
{% endhighlight %}

And to stop it?  `microstack.openstack server delete test`.  
You can also pause or stop it without deleting it.

Verified you can't ssh into a paused or stopped server, which makes sense.  
Hangs, times out eventually.  
But filesystem changes persist through pause/unpause and stop/start, 
even reboot.  Which makes sense since these are VMs.

Note: may not be able to use the default GUI to launch instances, 
their m1.tiny may be too large to create quickly?  
The error I get is:

{% highlight bash %}
did not finish being created even after we waited 3 seconds or 2 attempts. And its status is error.
{% endhighlight %}

So, just use the command line to fire up VMs for now.

## Microstack Performance Overhead

If I'm using this server as a docker swarm host, or a microk8s host, 
there may be no point in running all of the openstack daemons too, 
using up resources.  
This is how to disable them temporarily.  From the documentation.

> You may wish to temporarily disable your MicroStack installation when not in use. To do so, run:
>
>> sudo snap disable microstack
>
> To re-enable it, run:
>
>> sudo snap enable microstack
