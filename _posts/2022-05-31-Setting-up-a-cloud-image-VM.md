---
title: Setting up a Cloud Image template and Cloud Init
categories: [AI, servers, tutorial]
tags: [renderex computers,servers, gpu server, ai, tutorial, ai tutorial, virtualization, virtual machine, pcie passthrough, gpu vm, gpu virtual machine, linux, proxmox] #TAG names should be lowercase
---
# What is a 'Cloud Image'?

Cloud Images are lightweight, faster, certified cloud-ready versions of operating systems. They have Cloud Init pre-installed, meaning they can be configured using 'Cloud Config'. 

This works great combination with [setting up a GPU server in Proxmox.](https://docs.renderex.ae/posts/Setting-up-a-server-for-AI/)

## Getting Started

First, you'll want to decide which *version* of Ubuntu you'd like. We generally recommend 18.04LTS or 20.04LTS for AI applications.

Once you've decided, copy one of the URL's from [here.](https://cloud-images.ubuntu.com/)

Next, login to your Proxmox server and download it, being sure to use the URL of the version of your choosing:
```bash
wget https://cloud-images.ubuntu.com/bionic/current/bionic-server-cloudimg-amd64.img
```
## Create a VM

Next, let's create a virtual machine
```bash
qm create 8000 --memory 4096 --core 4 --name ubuntu-cloud --net0 virtio,bridge=vmbr0
```
Import the new disk to `local-lvm` storage (or whichever disk you prefer)
```bash
qm importdisk 8000 focal-server-cloudimg-amd64.img local-lvm
```
Attach the new disk to the virtual machine as a scsi drive on the scsi controller
```bash
qm set 8000 --scsihw virtio-scsi-pci --scsi0 local-lvm:vm-8000-disk-0
```
Add a 'cloud init' drive:
```bash
qm set 8000 --ide2 local-lvm:cloudinit
```
Make the cloud init drive bootable and restrict BIOS to boot from disk only:
```bash
qm set 8000 --boot c --bootdisk scsi0
```
Add a serial console:
```bash
qm set 8000 --serial0 socket --vga serial0
```
## Setting up hardware

If you'd like to make any hardware changes at this point, you should do so in the GUI. However, **do not start the VM**. 

It's best to keep the minimum amount of resources possible, as this will serve as a template. So don't attach any GPU's yet, and we recommend you keep the storage capacity low, as we can always expand this later.

## Copy - Paste

Now let's create a template:
```bash
qm template 6000
```
and clone it:
```bash
qm clone 6000 135 --name noor1 --full
```
*(Replace `noor1` with any name you want to give the VM, and `6000` with any ID)*

For [pre-built, pre-configured GPU servers for AI](https://renderex.ae/servers/ml-server), be sure to visit:

[https://renderex.ae/servers/ml-server](https://renderex.ae/servers/ml-server)
