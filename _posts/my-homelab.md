---
layout: post
title: My homelab and why I have it
subtitle: Random and expensive Hobby
tags: [homelab]
comments: true
mathjax: true
author: Guille R
---

# Intro
When I started working as IT there was a certain anxiety of not knowing enough, and wanting to perform better on my day to day work. That's when I decided to put together a server with some spare parts and invest in some networking equipment. S

# Networking
## Mikrotik
Initially I wanted to learn about Mikrotik since in one of my initial jobs in IT they were the backbone of our networking. If you ever worked with Miktrotik and RouterOS you know it doesn't hold your hand, but it gives you a lot of freedom of what you can do.
In spite of the steep learning curve it was totally worth it, not only it forces you to learn fundamentals of networking but even if you are spending $ or $$$$ in their gear the feature set is the same.
The model I have is [RB750Gr3](https://mikrotik.com/product/RB750Gr3) it has worked great so far that enabled me to do multiple neat things like setting up notifications by telegram if a server does not respond a ping or setting up automatic backups of the instance and upgrades.
## Unifi
As AP I'm using a [U6+](https://techspecs.ui.com/unifi/wifi/u6-plus) switched mostly to get Wifi6, before I had a [TP-Link Archer C2](https://www.tp-link.com/en/home-networking/wifi-router/archer-c2/) Router with DHCP disabled since that was controlled by the Mikrotik

# Hypervisor and Docker (Compute)
After some time passed we needed to add a unifi controller for some AP's we had, and to save resources I wanted to set it up on a vm, that is when I ran into the option to deploy it with docker, and it was very practical and easy to deploy which opened up a new world. So for that I had an old machine laying around and wanted to use that to deploy them. But since it wasn't a very powerful machine and had only one I needed to look for a Hypervisor, at work we were using Hyper-V on Windows Server or eSXi. But those option wouldn't work for me since one required a license(Windows) and the other one had a free license at the time (esXi) but wasn't convinced that would last (time prove me right), for that I turned to open source and found xcpng which I ran for a while, but didn't convince me since it lacked a web interface and installing it was a lot of extra resources, so went to my second pick Proxmox and have been running it ever since. Not only had everything I needed but even more, specially when finding that there were some alpha providers (which you had to compile on your own) for my other requirement that came up during this entire research,terraform. So I had a good way to deploy VMs using just code and using templates or ansible scripts for setting up machines with docker or kubernetes see [my talos terraform module](2025-10-21-created-my-own-tf-module-for-k8s-deployment.md) 
That is the software side, as far as the "server" I started with a core i5-2500 and 24Gb of ram with a 500gb disk and a 120gb ssd boot disk with 3 1tb disks. My current build is a i5-8600k with 32gb and I added 3 additional 4tb disks with a 2.5gb ethernet card. As a secondary server I'm running an old laptop, also with proxmox and it is setup in a cluster with the other node, which has allowed me to migrate essential services to this node. 

# What I'm currently running on it
## Truenas
First I needed to be able to handle my disks so I passedtrough the 3 disks to the vm and set up the share. Initially I was using truenas core and then moved to truenas scale. So far it is mostly to set the ZFS pool and I've played around with the docker apps a bit.
## Containers
### Pihole
I'm running 2 instances of pihole as my dns server to provide adblocking and setting up local dns for other services
### Traefik
Running it as a reverse proxy, it allows me to point the dns records on pihole to the server I have the service running it also has https selfsigning certificates with cloudflare
### Immich
It is a service like google photos with face recognition but it is local, so it is a safe way to store my personal photos
### OpenSpeedTest
It is like speedtest.net but local, useful to due speedtest on any device without the need to install iperf3
### Unifi Controller
Selfhosting the unifi controller to configure and monitor my AP
### Uptime Kuma
A service that monitors the other services and sends a notification over Telegram if they go down
