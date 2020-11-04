---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
---
This is the home page for my portfolio of interests and demonstrations
of technologies I don't get to use in my day job.

## Portfolio

### Family Picture Tagging Suite

Over the years the family has accumulated thousands of pictures from
various cameras and phones.  These have all been dutifully archived
to network attached storage, but are "hard" to access.
Each jpeg has some metadata, identifying "when" it was taken, assuming that
the camera was configured to the accurate date and time.

The "ask" is to be able to view the pictures in the order taken, after
optionally specifying start and end dates.  For each picture viewed, tag
it with one of 4 labels, or mark it for soft deletion.

The architecture of the [suite](https://github.com/davejenkins64/picture-tagger-demo) is to separate into client and server layers.
The [server](https://github.com/davejenkins64/picture-tagger-demo/tree/master/backend)
runs on the machine hosting the pictures via an Apache 
web server as a Dockerized Python/Flask RESTful service.
The [client](https://github.com/davejenkins64/picture-tagger-demo/tree/master/frontend) runs on the local laptop as a Typescript/Angular Material Design
front end.

### Javascript Canvas Layers

Given a tool for redacting areas of a document, where each redaction 
is marked witha non-transparent black rectangle, create an [un-redaction
tool](https://github.com/davejenkins64/un-redaction-demo) that can redact the whole page and then "un-redact" chosen rectangles.

The assignment was to "tile" the 2D canvas with 4 rectangles irising around a 
mouse selected rectangular area.  These rectangles are called "marks" and 
will appear non-transparent.
Once the original whole-canvas is tiled, the next mouse selection rectangle
must re-tile any "marks" that overlap the selection.

Used javascript, css, html5's 2D-canvas with tiered drawing layers.

### Apache Solr Demo

### Blacklight.org Demo

## Virtual Lab

Obviously, things that can be developed locally on a laptop don't require
and additional development/testing lab environment.  
For things that are traditionallly server-based, or where I'd like to simulate
a multi-node architecture on a single node, I've set up a surplus
[desktop PC](/compute_node/) with sufficient
ram to be the host of simulated networks of containers or VMs.

### Compute Node (ubuntu)

In case I forget, here is how I was able to make a bootable USB drive
to install ubuntu server 20.04 on the [compute node](/compute_node/)
that I use to simulate clouds of servers.

### Vagrant

I usually just use Virtualbox on laptops if I need virtual machines.
In the case of the compute node, I was hoping for better orchestration
control from something more command-line driven, like [Vagrant](/vagrant/).

### Docker/Docker Swarm

Docker does work on the compute node, once I add the docker group and
chown the socket, etc.  I've used it to containerize blacklight.org so
far, as well as experiment with containerizing Jekyll.

### Openstack (microstack)

After a failed attempt to install devstack, I took the ubuntu way and 
installed [microstack](/microstack/).  This worked well, and you can
disable the daemons when you don't need them.

### Kubernetes (microk8s)

## Blog

Here is a link to my 
[blog](/blog/).
