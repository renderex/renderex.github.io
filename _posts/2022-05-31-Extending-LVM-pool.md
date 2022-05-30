---
title: Extending an LVM storage pool in Proxmox
categories: [AI, servers, proxmox]
tags: [renderex computers,servers, gpu server, ai, tutorial, ai tutorial, virtualization, virtual machine, pcie passthrough, gpu vm, gpu virtual machine, linux, proxmox] #TAG names should be lowercase
---
## Format the drive

First, list the available disks:
```bash
fdisk -l
```
Format the disk you want to add, creating a partition, in this case we will create `sdf1` on the disk `sdf`:
```bash
cfdisk /dev/sdf
```

## Create a physical volume

```bash
pvcreate /dev/sdf1
```
Extend it:
```bash
vgextend pve /dev/sdf1
```
```bash
lvextend /dev/pve/data -L +7.3T
```
*(Replace `+7.3T` with the size of the disk space being added)*

Done!


For [pre-built, pre-configured GPU servers for AI](https://renderex.ae/servers/ml-server), be sure to visit:

[https://renderex.ae/servers/ml-server](https://renderex.ae/servers/ml-server)
