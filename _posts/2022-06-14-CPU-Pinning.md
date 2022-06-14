---
title: CPU Pinning in Proxmox
categories: [AI, tutorial, servers, proxmox]
tags: [renderex computers,servers,workstations, proxmox, virtualization, ai, tutorial, ai tutorial, linux] #TAG names should be lowercase
---

## What is CPU pinning?

Generally in virtualization, the host will spread the workload of a VM accross all of the available host cores. However, with CPU pinning, you can 'pin' the tasks of a VM to specific cores on the host, allowing it to fully utilize those cores and 'blocking' them from performing any other tasks.
This can greatly increase CPU performance on a VM and provide near-native CPU performance on thoe cores.

## Pinning the cores

SSH into the host (Proxmox) and run the command:

```bash
taskset --cpu-list --all-tasks --pid 0-7 $(< /run/qemu-server/103.pid)
```

In this case, replace `0-9` with the number of CPU cores you want to pin to this virtual machine. **note: CPU core count starts at 0, so in this example we are pinning 8 cores to the VM with ID 103**.
In addition, replace `103.pid` with the ID number of the VM you'd like to pin.

## Checking if the cores are pinned

You can easily check if the CPU pinning has been successful by running `htop` on the host machine and stressing the VM (e.g. `stress --cpu [number of cores]`)

## Automating the process


We can automate this process in Proxmox by creating a 'hookscript'. In this example, we create a hook script for VM 103, to permanently pin 8 CPU cores to it. 

```bash
nano /etc/pve/qemu-server/103.conf
```

to the bottom of the file, add:

```bash
hookscript: local:snippets/cpu-pinning-103.sh
```

Navigate to the local data store

```bash
cd /var/lib/vz
```

If there isn't a `snippets` directory, go ahead and create one, then create the hookscript inside it:

```bash
cd snippets && nano cpu-pinning-103.sh
```

```bash
#!/bin/bash

vmid="$1"
phase="$2"

cpuset="0-7"

if [[ "$phase" == "post-start" ]]; then
    main_pid="$(< /run/qemu-server/$vmid.pid)"
    taskset --cpu-list  --all-tasks --pid "$cpuset" "$main_pid"
fi
 ```
 
 Exit out of nano and make the script executable:
 
 ```bash
 chmod +x cpu-pinning-103.sh
 ```

You can also 'unhook' this script from the VM at anytime from the web GUI, as there should now be a "Hookscript" option at the bottom of the "Options" tab
in your VM's pane.

That's it, you're done! For [pre-built, pre-configured GPU servers for AI](https://renderex.ae/servers/ml-server), be sure to visit:

[www.renderex.ae](https://www.renderex.ae)
