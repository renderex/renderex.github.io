---
title: GPU Compute Servers
categories: [AI, servers]
tags: [renderex computers,servers, gpu server, ai, virtualization, virtual machine, pcie passthrough, gpu vm, gpu virtual machine] #TAG names should be lowercase
---

# GPU Compute Servers

## Training Server
Training servers for AI come in a variety of flavors and configurations.

### Form Factors

| Form Factor | # of GPU's |
| ---| -----|
| 4U | 8 |
| 2U | 8 |
| 2U | 4 |

### GPU's


These can be configured for you by **RendeRex** with a wide variety of both consumer-grade and enterprise GPU's.



| GPU | Class |
|---|---|
| RTX3090 | Consumer |
| RTX3080Ti | Consumer |
| Quadro RTX A5000 | Enterprise |
| Quadro RTX A6000 | Enterprise |
| NVIDIA A10 | Enterprise |
| NVIDIA A30 | Enterprise |
| NVIDIA A100 40GB PCIe | Enterprise |
| NVIDIA A100 80GB PCIe | Enterprise |

For the NVIDIA A100 80GB SXM4 variant, the SKU is limited in form-factor to a 4U chassis.

### Consumer-grade GPU's

Consumer GPU's can be useful for smaller research teams with a limited budget, or in early stages of development. These draw significantly more power
than their enterprise counter-parts, but provide enough performance that they make sense financially as a one-off, or in a small cluster. It should be
noted however, that there are some functions in Deep Learning applications that are unsupported on consumer-grade NVIDIA cards, and these should be
researched independently.

### Enterprise-grade GPU's

NVIDIA's enterprise selection of cards for AI is vast, and almost all cards will be supported on our platforms, and can be upgraded / swapped out in
the future. The complete list of cards supported in our servers extends beyonds the cards mentioned here (as **RendeRex** is an approved **NVIDIA NPN Partner**), however we have included these cards as a
reference of the (currently) most popular GPU's for AI training.

### Memory

In terms of RAM, for training NVIDIA recommends at least 1,5 times the available VRAM, so this will depend highly on your GPU configuration. For example,
for an 8x GPU configuration of a GPU with 24GB of VRAM, the recommended value is a minimum of 288GB of RAM.

### Storage

This will vary depending on your use-case. For a single-team, one-off server, it makes more sense to have a single boot drive, and either an array of
SSD's (which can either be consumer-grade or enterprise-grade SSD's), or a single, larger HDD. Especially with large datasets, we understand that storage
can be exhausted very quickly.

For larger, more complex configurations, we can configure an additional, central storage server (easily expandable in the future to multiple storage
nodes). This can be configured with a variety of proprietary and OSS software (depending on your needs), to provide NFS storage, or S3, depending
on your requirements.

Some examples:

| Software | Storage type | Type |
| --- | --- | --- |
| TrueNAS | NFS | OSS |
| OpenZFS | NFS | OSS |
| MinIO | S3 | Both |
| WekaFS | S3 | Proprietary |

### Networking
Depending on your chosen SKU, your server will, by default, come with an oboard IPMI, as well as 2 ports of either 1Gbps or 10Gbps networking.
Additionally, we can provision for 25Gbps, 100Gbps Ethernet, as well as 200Gbps InfiniBand.

### Environment / OS

Depending on how much involvement you'd like from **RendeRex**, we generally provide three different types of configurations for servers:

| Configuration | Description |
| --- | --- |
| Ubuntu 18.04/20.04 LTS | Your preferred version of Ubuntu, running bare-metal, pre-configured for AI |
| Virtualization Environment | A series of pre-configured Ubuntu-based VM's with GPU pass-through, running in an OSS virtualization environment using QEMU/KVM |
| Kubernetes | An OSS Kubernetes environment using Docker or Singularity |

## Contact Us
To get in touch with **RendeRex** about purchasing one of our GPU-Compute solutions for your team/project, e-mail us at: [info@renderex.ae](mailto:info@renderex.ae)
