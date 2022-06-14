---
title: Enabling Hugepages in Proxmox
categories: [AI, tutorial, servers, proxmox]
tags: [renderex computers,servers,workstations, proxmox, virtualization, ai, tutorial, ai tutorial, linux] #TAG names should be lowercase
---

## What are Hugepages?

>Memory is managed in blocks known as pages. On most systems, a page is 4Ki. 1Mi of memory is equal to 256 pages; 1Gi of memory is 256,000 pages, and so on. CPUs have a built-in memory management unit that manages a list of these pages in hardware. The Translation Lookaside Buffer (TLB) is a small hardware cache of virtual-to-physical page mappings. If the virtual address passed in a hardware instruction can be found in the TLB, the mapping can be determined quickly. If not, a TLB miss occurs, and the system falls back to slower, software-based address translation, resulting in performance issues. Since the size of the TLB is fixed, the only way to reduce the chance of a TLB miss is to increase the page size.

>A huge page is a memory page that is larger than 4Ki. On x86_64 architectures, there are two common huge page sizes: 2Mi and 1Gi. Sizes vary on other architectures. To use huge pages, code must be written so that applications are aware of them. Transparent Huge Pages (THP) attempt to automate the management of huge pages without application knowledge, but they have limitations. In particular, they are limited to 2Mi page sizes. THP can lead to performance degradation on nodes with high memory utilization or fragmentation due to defragmenting efforts of THP, which can lock memory pages. For this reason, some applications may be designed to (or recommend) usage of pre-allocated huge pages instead of THP.

## Why and when to use Hugepages

Anytime you want to create a VM with more than 64GB of RAM, you'll want to use Hugepages.


## Enable Hugepages

To enable Hugepages in Proxmox, in the "hardware tab", under "CPU", you want to enable the hugepages flag, which is titled `pdpe1gb`.

![Proxmox hugepages](https://www.renderex.ae/docs/hugepages/1.png)

Next, SSH into Proxmox itself and enable hugepages in GRUB:

```bash
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on hugepagesz=1G default_hugepagesz=2M"
```

That's it, you're done! For [pre-built, pre-configured GPU servers for AI](https://renderex.ae/servers/ml-server), be sure to visit:

[www.renderex.ae](https://www.renderex.ae)
