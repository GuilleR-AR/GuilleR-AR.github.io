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
When I started working in IT there was a certain anxiety about not knowing enough and wanting to perform better in my day-to-day work. That's when I decided to put together a server with some spare parts and invest in some networking gear.

<details markdown="1">
<summary>Homelab Diagram</summary>
!["Selfhosted services"](https://raw.githubusercontent.com/GuilleR-AR/diagram-as-code/refs/heads/main/src/homelab.png)
</details>



# Networking

<details markdown="1">
<summary>Network Diagram</summary>
!["Selfhosted services"](https://raw.githubusercontent.com/GuilleR-AR/diagram-as-code/refs/heads/main/src/network.png)
</details>

## MikroTik
Initially I wanted to learn about MikroTik since in one of my first IT jobs they were the backbone of our networking. If you ever worked with RouterOS you know it doesn't hold your hand, but it gives you a lot of freedom. In spite of the steep learning curve, it was totally worth it — not only did it force me to learn networking fundamentals, but even if you're spending 💲 or 💲💲💲💲 on their gear the feature set is the same.

The model I have is [RB750Gr3](https://mikrotik.com/product/RB750Gr3). It has worked well and enabled me to do multiple neat things, like sending Telegram notifications if a server stops responding to ping, and setting up automatic backups and upgrades.

## UniFi
For APs I'm using a [U6+](https://techspecs.ui.com/unifi/wifi/u6-plus), chosen mostly to get Wi‑Fi 6. Previously I used a [TP-Link Archer C2](https://www.tp-link.com/en/home-networking/wifi-router/archer-c2/) router with DHCP disabled because DHCP was controlled by the MikroTik.

# Hypervisor and Docker (Compute)
After some time we needed to add a UniFi Controller for some APs, and to save resources I wanted to run it in a VM. I discovered deploying with Docker was practical and easy, which opened a new world. I had an old machine for this, but since it wasn't very powerful and had only one CPU, I looked for a hypervisor. At work we used Hyper‑V on Windows Server or ESXi. Those options weren't ideal for me (Windows requires a license, and ESXi's free option felt uncertain), so I turned to open source and tried XCP‑ng for a while. It lacked a web interface and felt heavy to install, so I moved to my second pick, Proxmox, and have been running it ever since. Proxmox gave me everything I needed, and I found Terraform providers (some alpha at the time) that made it easy to deploy VMs from code.

For provisioning I use templates, Ansible scripts and Terraform; see my Talos Terraform module for Kubernetes deployment: [Created my own tf-module for k8s deployment](../2025-10-21-created-my-own-tf-module-for-k8s-deployment).

On the hardware side, I started with an Intel Core i5‑2500, 24 GB of RAM, a 500 GB disk and a 120 GB SSD boot disk, plus three 1 TB disks. My current build is an Intel Core i5‑8600K with 32 GB of RAM; I added three additional 4 TB disks and a 2.5 Gb Ethernet card. As a secondary node I'm running an old laptop also with Proxmox, set up in a cluster with the main node, which has allowed me to migrate essential services between nodes.

# What I'm currently running on it

<details markdown="1">
<summary>Self Hosted Services Diagram</summary>
!["Selfhosted services"](https://raw.githubusercontent.com/GuilleR-AR/diagram-as-code/refs/heads/main/src/apps.png)
</details>

## TrueNAS
First I needed a way to manage disks, so I passed through the three disks to a VM and set up the share. I initially used TrueNAS Core and later moved to TrueNAS Scale. Mostly I use it for ZFS pools and I've experimented with the Docker apps.

## Containers

### Pi‑hole
I run two instances of Pi‑hole as my DNS servers to provide ad blocking and local DNS for other services.

### Traefik
I run Traefik as a reverse proxy. It lets me point DNS records (set via Pi‑hole) to the server hosting each service. I use self‑signed HTTPS certificates in conjunction with Cloudflare.

### Immich
Immich is a self‑hosted alternative to Google Photos (with face recognition), so it's a private way to store my personal photos.

### OpenSpeedTest
A local alternative to speedtest.net, useful for testing connection speed on any device without installing iperf3.

### UniFi Controller
Self‑hosting the UniFi Controller to configure and monitor my access points.

### Uptime Kuma
Monitors the other services and sends Telegram notifications if they go down.

