---
title: Creating a new VM in Proxmox
categories: [AI, tutorial, servers, proxmox]
tags: [renderex computers,servers, gpu server, ai, tutorial, ai tutorial, virtualization, virtual machine, pcie passthrough, gpu vm, gpu virtual machine, training server] #TAG names should be lowercase
---

## 1. Start the creation wizard

In the top-right, start the creation wizard by opening up a "New VM". Give your VM a name, and change the VM ID to whatever you want, or let Proxmox choose an ID for you.

![Proxmox create new VM](https://www.renderex.ae/docs/new-vm/1.png)

## 2. Add the ISO image

Navigate to the OS tab and select the ISO image you'd like to create the VM with. Proxmox should automatically choose the Kernel version and the OS type for you, but double-check just to make sure.

![Adding ISO to Proxmox](https://www.renderex.ae/docs/new-vm/2.png)

## 3. System Tab

Next, move to the 'System' tab, you can either leave everything as the default here, or you can switch to OVMF for UEFI support. For this tutorial we'll leave everything as default.

![Proxmox system tab](https://www.renderex.ae/docs/new-vm/3.png)

## 4. Setting up storage disks

Move to the disks tab and make sure to select "VirtIO" block for best performance. Set the disk size in GiB, you can leave the rest of the settings to their defaults.

![Proxmox disks setup](https://www.renderex.ae/docs/new-vm/4.png)

## 5. CPU setup

Choose how many CPU cores you'd like to assign the VM, and for 'type', we recommend setting the CPU to 'host', to allow use of the AVX-512 instruction set. This is necessary for some applications in TensorFlow.

![Proxmox CPU setup](https://www.renderex.ae/docs/new-vm/5.png)

## 6. Memory (RAM)

In the memory tab, you can select how much RAM you'd like to assign to the VM, **note: this must be set in Megabytes**. In this example, we are assigning 32GB of memory to the VM.

A ballooning device means that the VM can be assigned an amount of RAM, but will not utilize the full amount until necessary. This allows for RAM to be shared across VM's - think of this as a maximum allocated RAM option. For values larger than 64GB of RAM, we recommend you turn on "hugepages". We will add documentation on how to do this elsewhere.

![Proxmox RAM setup](https://www.renderex.ae/docs/new-vm/6.png)


## 7. Network

For the best performance, set the network model to "VirtIO (paravirtualized)". In this tab you can also assign the VM to a VLAN if you decide.

![Proxmox Network setup](https://www.renderex.ae/docs/new-vm/7.png)


## 8. Review and confirm

The final tab is a summary of your inputs, review the information and click "Finish". You can also check the box "Start after created" if you'd like.

![Proxmox final setup](https://www.renderex.ae/docs/new-vm/8.png)

## 9. Start your VM

If you haven't already, find your VM in the left pane, right click and "Start" the VM.

![Proxmox Start VM](https://www.renderex.ae/docs/new-vm/9.png)


## 10. Install the OS

In the "Console" tab, proceed to install the VM as normal.

![Proxmox VM Install](https://www.renderex.ae/docs/new-vm/10.png)


## 11. Adding/Removing Hardware

The "Hardware" tab allows you to control the hardware attached to your VM. This includes CD/DVD-ROM drives, PCIe devices, etc. From here you can "detach" the CD/DVD drive after the installation is complete.

![Proxmox hardware tab](https://www.renderex.ae/docs/new-vm/11.png)


## 12. Final Setup

Go ahead and use the console to set-up your networking inside the VM, and update. Optionally, you can also setup a guest agent in your VM so that you can control and manage things like the IP address from the host itself (Proxmox).

On Linux this is very easy to achieve. On Ubunutu:

```bash
sudo apt-get install qemu-guest-agent

```

If it doesn't start automatically:

```bash
systemctl start qemu-guest-agent

```

That's it! Your new VM is set up and ready to go. For [pre-built, pre-configured GPU servers for AI](https://renderex.ae/servers/ml-server), be sure to visit:

[https://renderex.ae/servers/ml-server](https://renderex.ae/servers/ml-server)
