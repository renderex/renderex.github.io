---
title: Adding a new ISO to Proxmox
categories: [AI, tutorial, servers, proxmox]
tags: [renderex computers,servers, gpu server, ai, tutorial, ai tutorial, virtualization, virtual machine, pcie passthrough, gpu vm, gpu virtual machine] #TAG names should be lowercase
---

## 1. Navigate to your storage

Navigate to the storage dedicated to your ISO images and click the "ISO Images" tab on the left hand side.

![Proxmox storage](https://www.renderex.ae/docs/new-iso/1.png)

## 2. Download the ISO

Above the ISO images, you have two options, either to upload your own or to download from URL. For the sake of this example, we'll be downloading Ubuntu 20.04LTS directly from Canonical.

![Downloading Ubuntu in Proxmox](https://www.renderex.ae/docs/new-iso/2.png)

## 3. Get the download URL

Navigate to the website of the ISO you'd like to download and copy the download link.

![Download Ubuntu 20.04](https://www.renderex.ae/docs/new-iso/3.png)

## 4. Paste the download link back into the Proxmox GUI

![Proxmox storage](https://www.renderex.ae/docs/new-iso/4.png)

## 5. (Optional) Checksum

If you're downloading an obscure ISO and you're unsure of the source, you can always open the advanced tab and Proxmox will compare the checksum of the downloaded ISO for you.

![Proxmox checksum](https://www.renderex.ae/docs/new-iso/5.png)
