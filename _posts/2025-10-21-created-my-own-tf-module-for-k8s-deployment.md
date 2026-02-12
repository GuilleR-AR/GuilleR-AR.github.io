---
layout: post
title: Created my own tf-module for k8s deployment
subtitle: From 0 to k8s on proxmox with talos and terraform 
gh-repo: GuilleR-AR/terraform-proxmox-talos-cluster
gh-badge: [star, fork, follow]
tags: [terraform, proxmox, homelab]
comments: true
mathjax: true
author: Guille R
---

# Why I created this module
I wanted a fast, simple way to create a near-production Kubernetes cluster — primarily to test new features and to experiment with Kubernetes.

# Project foundations
I already knew Terraform was the right tool for provisioning, and that Proxmox can be managed like a cloud provider using Terraform. That made Terraform + Proxmox a natural starting point.

# Why Talos?
There are multiple ways to deploy Kubernetes on-prem (k3s, kubeadm, RKE, kops, Talos, etc.). I chose Talos OS because it is simple, secure, and requires minimal maintenance, which lets me focus on Kubernetes itself. Talos uses an API for node management (no SSH) and provides its own CLI, talosctl.

Part of my inspiration was [this post](https://olav.ninja/talos-cluster-on-proxmox-with-terraform). I followed it and it worked well, but I saw opportunities to simplify and iterate.

# The result
## Module repository
URL: [https://github.com/GuilleR-AR/terraform-proxmox-talos-cluster](https://github.com/GuilleR-AR/terraform-proxmox-talos-cluster)

## Terraform Registry
URL: [https://registry.terraform.io/modules/GuilleR-AR/talos-cluster/proxmox/latest](https://registry.terraform.io/modules/GuilleR-AR/talos-cluster/proxmox/latest)

# Conclusion
The module still needs work, but it already lets me spin up Kubernetes clusters easily and iterate on improvements.