---
title: Setting up a Workstation for AI
categories: [AI, workstations, tutorial]
tags: [renderex computers,servers,workstations, ai, tutorial, ai tutorial] #TAG names should be lowercase
---

# Getting Started

The first thing you'll want to do on your new Ubuntu installation is to **blacklist nouveau**. Nouveau is an open-source Linux graphics driver which is loaded at boot, but this has been known to interfere with certain functions of the NVidia driver, and can cause problems, especially when installing 'beta' versions of NVidia drivers.

First, open up a terminal and type:
```bash
sudo nano /etc/modprobe.d/blacklist-nouveau.conf
```
and insert the following:
```bash
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off
```
Save the file and exit out of nano.

Disable the nouveau in the Linux kernel:
```bash
echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/blacklist-nouveau.conf
```
Update the kernel's initramfs
```bash
sudo update-initramfs -u
```

## Install the NVidia drivers

```bash
sudo apt install nvidia-driver-510
```
_This will install NVidia driver version 510._

**Once the installation is complete, don't forget to reboot.**
```bash
sudo reboot
```
## Checking that the driver is correctly intalled
To ensure that the driver has loaded properly, open up a terminal and enter:
```bash
nvidia-smi
```
If successfukl, you should see your GPU(s) listed in the terminal.

_Tip: If you'd like to continuously watch your GPU's, you can use:_ 
```bash
watch nvidia-smi
``` 
_this will give you an overview of the sensor output on your GPU(s) at an interval of every 2 seconds_

That's it! you're now ready to install CUDA, etc., and begin building your training environment.

## Optional: Set CPU governor to 'performance mode'

If you'd like to set the CPU to 'performance mode', open up a terminal:
```bash
sudo apt-get install cpufrequtils
echo 'GOVERNOR="performance"' | sudo tee /etc/default/cpufrequtils
sudo systemctl disable ondemand
```

For pre-built, pre-configured AI workstations, be sure to visit:

[https://renderex.ae/workstations/data-science.html](https://renderex.ae/workstations/data-science.html)
