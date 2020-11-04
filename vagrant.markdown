---
layout: page
title: Installing Vagrant
permalink: vagrant
---

## Vagrant Install/Configure

Vagrant can fire up VMs for us.  It needs a provider to do the actual
work, and the "default" one appears to be virtualbox.  

So, for now, I'm installing installing vagrant and virtualbox

{% highlight bash %}
sudo apt install virtualbox vagrant virtualbox-dkms linux-headers-generic
{% endhighlight %}

Note, when installing virtualbox on an EFI host, it made a password
for secure boot, I chose 'user_user' but not sure how this is really used.

But perhaps also install vagrant-libvirt as another provider.
Can be done from vagrant: `vagrant plugin install vagrant-libvirt`

This does not seem to work.  Skipping for now.
But `vagrant plugin list` does show libvirt:

{% highlight bash %}
vagrant-libvirt (0.0.45, system)
{% endhighlight %}

Try adding vagrant-lxc too to get another provider?  No, the plugin list
is still only vagrant-libvirt.
And it also seems that only `lxc` images can be started.

## Vagrant Tutorial

### Initializing

First, run vagrant init:

{% highlight bash %}
vagrant init
{% endhighlight %}

Says:

{% highlight bash %}
A `Vagrantfile` has been placed in this directory. You are now
ready to `vagrant up` your first virtual environment! Please read
the comments in the Vagrantfile as well as documentation on
`vagrantup.com` for more information on using Vagrant.
{% endhighlight %}

### Bringing up a VM

Edit the Vagrantfile.  I think it wants us to choose an image to boot,
and to edit "base" to be the name of the image.  Running with this unchanged
yields:

{% highlight bash %}
sudo vagrant up
{% endhighlight %}

Yields:

{% highlight bash %}
The `lxc` package does not seem to be installed or `lxc-create` is not accessible on the PATH.
{% endhighlight %}

So let's also install lxc-utils.

Now when we try `sudo vagrant up` we get:

{% highlight bash %}
$ sudo vagrant up
Bringing machine 'default' up with 'lxc' provider...
==> default: Box 'base' could not be found. Attempting to find and install...
    default: Box Provider: lxc
    default: Box Version: >= 0
==> default: Box file was not detected as metadata. Adding it directly...
==> default: Adding box 'base' (v0) for provider: lxc
    default: Downloading: base
An error occurred while downloading the remote file. The error
message, if any, is reproduced below. Please fix this error and try
again.

Couldn't open file /home/user/base
{% endhighlight %}

So, my provider appears to be `lxc` and https://vagrantcloud.com/search 
says a recently updated ubuntu 20.04 is `capensis/ubuntu20.04`, so I change
base to that and try again.

{% highlight bash %}
sudo vagrant up
{% endhighlight %}

Yields:

{% highlight bash %}
Bringing machine 'default' up with 'lxc' provider...
==> default: Box 'capensis/ubuntu20.04' could not be found. Attempting to find and install...
    default: Box Provider: lxc
    default: Box Version: >= 0
==> default: Loading metadata for box 'capensis/ubuntu20.04'
    default: URL: https://vagrantcloud.com/capensis/ubuntu20.04
==> default: Adding box 'capensis/ubuntu20.04' (v0.1) for provider: lxc
    default: Downloading: https://vagrantcloud.com/capensis/boxes/ubuntu20.04/versions/0.1/providers/lxc.box
    default: Download redirected to host: vagrantcloud-files-production.s3.amazonaws.com
==> default: Successfully added box 'capensis/ubuntu20.04' (v0.1) for 'lxc'!
==> default: Importing base box 'capensis/ubuntu20.04'...
==> default: Checking if box 'capensis/ubuntu20.04' version '0.1' is up to date...
==> default: Setting up mount entries for shared folders...
    default: /vagrant => /home/user
==> default: Starting container...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 10.0.3.165:22
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: 
    default: Vagrant insecure key detected. Vagrant will automatically replace
    default: this with a newly generated keypair for better security.
    default: 
    default: Inserting generated public key within guest...
    default: Removing insecure key from the guest if it's present...
    default: Key inserted! Disconnecting and reconnecting using new SSH key...
==> default: Machine booted and ready!
{% endhighlight %}

Hmm, but since I ran it with sudo, is it root's private key?

Did it really work?

{% highlight bash %}
sudo vagrant status
{% endhighlight %}

Yields:

{% highlight bash %}
Current machine states:

default                   running (lxc)

The VM is running. To stop this VM, you can run `vagrant halt` to
shut it down forcefully, or you can run `vagrant suspend` to simply
suspend the virtual machine. In either case, to restart it again,
simply run `vagrant up`.
{% endhighlight %}

So, let's get a keypair generated for root and user and see which one
vagrant is using for authentication?

### Cheat Sheet

`vagrant halt` seemed to work, but leaves the image halted. The command
`vagrant destroy` then cleans up the VM, but the image stays around and
is cached to be used as a template to make future VMs.

Note: once you can ssh into a container, you'll be the vagrant user in /home/vagrant and
all files in /vargrant will be sync'ed with the directory that holds the Vagrantfile.
So, one box per directory, multiple directories to make a swarm.

TODO: how to we attach a nework between VMs. First thing to try would be
to look in Vagrantfile for comments on public/private networks.
