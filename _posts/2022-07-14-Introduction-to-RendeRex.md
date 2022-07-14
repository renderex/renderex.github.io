---
title: Introduction to RendeRex services in compute and GPU clusters
categories: [AI, servers]
tags: [renderex computers,servers, gpu server, ai, tutorial, ai tutorial, virtualization, virtual machine, pcie passthrough, gpu vm, gpu virtual machine] #TAG names should be lowercase
---

# How RendeRex adds value to server sales

## What do we do?

RendeRex takes the initial and ongoing DevOps & MLOps required to set up GPU and compute clusters out of the equation for end-users. This means that the data-science team can focus directly on their work, rather than spend countless hours wasted on Linux system administration and MLOps/DevOps.

Most large organizations today, especially in the ME, will hire a full-time DevOps/MLOps engineer or team of engineers depending on the scale of the project in order to set up and maintain the cluster. 

This adds a big layer of inefficiency due to the lack of MLOps/DevOps engineers in the region, as well as the fact that other than the initial setup and deployment, these expensive personnel are rarely required.

RendeRex does this automatically for the end-user with the purchase of a cluster, compute or storage node. So what exactly is MLOps/DevOps?

## MLOps / DevOps

Essentially, there are several options depending on whether the end-user has purchased a single compute node or cluster.

#### Single Node:
* Baremetal Linux
* OSS Virtualization environment (Proxmox / XCP-NG) + VFIO
* Kubernetes cluster built on top of virtualization + VFIO

#### Cluster:
* Vanilla Kubernetes with Docker + VFIO
* Kubernetes with KubeFlow + VFIO
* OpenStack with Kubernetes + KubeFlow + VFIO

## What is VFIO?

VFIO essentially means that the GPU is passed through entirely as a PCIe device to the virtual machine. The value of this is that the end-user does not have to pay for / maintain an NVIDIA licensing server to utilize vGPU, instead they can simply pass through the entire GPU to the virtual machine / pod / container at no additional cost. **This also means that consumer NVIDIA GPU's can be utilized in GPU-Comptue clusters.**

## What is an OSS Virtualization Environment, and why is it useful?

An OSS virtualization environment is essentially the same thing as VMWare, built on a free and open-source platform using Linux QEMU/KVM. We can split a server into multiple virtual machines and pass-through a GPU, or multiple GPU's to each of them. This is especially useful for small Data Science teams who are working off of a server node.

In essence, the server is split into several virtual workstations which can be accessed online, with permanent storage and dynamic resources (that are controlled manually by a system admin). From the data-scientists perspective, it is as if they are working on baremetal Linux.

## What is baremetal Linux?

A baremetal Linux solution is (usually) an Ubuntu 18.04LTS or Ubuntu 20.04LTS Linux machine that is optimized, out-of-the-box, for AI/ML.

#### This entails:
* Installing NVIDIA drivers
* Blacklisting the `nouveau` driver
* Further kernel optimizations
* Installation of Docker, CUDA, CuDNN, TFlow, etc. (specific AI/ML packages/frameworks upon request from the end-user)

## What is a Kubernetes cluster?

Kubernetes is an open-source orchestration platform for containerization developed primarily by Google. It was built to solve the problem of scalability of services, and has been widely adopted by the AI/ML community for its own use.

Traditionally, data scientists will run their applications as some sort of container (usually Docker), which will then run on top of a single compute node or inside a virtual machine. This works fine when there are 1-2 compute nodes, and we have a small team. However, problems arise when we start adding multiple compute nodes and adding team members to a project.

Simply put, Kubernetes allows end users to run their containerized applications on scalable **pods**, without caring about what node they're deployed on or which compute node they're pulling their resources from. 

The fact that these pods are scalable means that the application can pull resources from multiple **compute nodes**, creating a **cluster** of **pods**, which combine to form a **service**. This service is then granted a single IP address (even if it is running on several compute nodes) by a **load balancer**. 

From the end-user perspective, they could effectively log-into a **management** or **head-node**, deploy an application and utilize the entire resources of the cluster; hundreds or even thousands of GPU's at once.

## Kubernetes + KubeFlow

KubeFlow is a set of applications that run on top of Kubernetes and simplify the ML/AI development and production process for data scientists. It also makes the process portable to other platforms (AWS, Azure, GKE, etc.), as well as scalable.

#### KubeFlow includes:
* **JupyterHub** for creating Jupyter Notebooks (visualized, on-the-go, in-browser python programming)
* **TensorFlow Serving** for model serving
* **TensorFlow Training** for model training
* **Katib** for hyperparameter search and tuning
* **Model version control**
* **KubeFlow Pipelines**, an easy-to-use comprehensive UI for running experiments, etc.
* **MinIO server** for storing artifacts
* & more...


## What is OpenStack

OpenStack takes things one step further when utilizing a large amount of resources. This allows you to turn your datacenter hardware into an **on-prem private cloud**, and have your team use it exactly the same way as they would use Amazon AWS, Google GKE, etc.

From the end-user / data-science team's perspective, the UI will feel identical to familiar platforms (AWS, GKE, etc.). 

It also has the ability to integrate with public cloud providers so that you can essentially build a **hybrid-cloud**, utilizing both on-prem resources and, for example, Google GKE compute resources.

When combining OpenStack with Kubernetes running on top of it, running KubeFlow with VFIO enabled, essentially the end-user now has a full, enterprise-grade production environment which can be deployed with either consumer or enterprise-grade GPU's.

The main selling-point, as far as the end-user is concerned, is the **pay and forget** aspect, as there are **no licensing fees involved in the entire solution.** Everything is free, open-source, enterprise-grade and utilized in production by industry giants in the AI/ML space.

## High-Availability

When utilizing multiple nodes in a professional/enterprise environment, it is important that a single node's failure does not take down the entire cluster. RendeRex will usually deploy a cluster with **3 head/master nodes** and **n compute nodes**. This means that if a head/master node fails, or any of the compute nodes, the remainder of the cluster will continue functioning as normal. By definition, this is known as a **High Availability (HA) Cluster**.

For the compute nodes, Kubernetes itself is **self-healing**, meaning that if a compute node dies, it will simply migrate the **compute pod** to a different compute node and continue serving the **service**.

The principles of high-availability also applies to storage nodes, as well as databases. For example, for Kubernetes to function it utilizes **etcd databases**, which are also deployed in pairs of three, so that if one fails, the information about cluster health, status, etc. is not lost, and the service continues as normal while maintenance is performed.

## Storage

RendeRex will set up storage nodes for its clients and attach them to the compute cluster with either free, open-source (FOSS) software, or proprietary software. Our engineers are familiar with Lustre, WekaFS, TrueNAS Core, TrueNAS Scale, and more.

#### An example set-up using TrueNAS Scale would be:
* RAIDZ1 ZFS SSD Pool
* Attached to Kubernetes as an NFS share
* RAIDZ2 ZFS HDD Archive pool
* Automatic, periodic backups of SSD data
* Local compute node drives set as an NFS cache using **cachefilesd** in Linux

For single-node setups, TrueNAS can also easily spin up an **S3 MinIO** server for object-storage. 

## Additional DevOps / MLOps support packages

**Everything we've mentioned so far comes included at no additional cost** to the end-user and is included with the purchase of a compute node or compute cluster from RendeRex.

In addition, RendeRex also offers support packages, billed annually, for either phone/e-mail support or an on-prem engineer from RendeRex to be stationed at the end-users' datacenter.

## Conclusion

We hope you've enjoyed the brief summary of some of what RendeRex has to offer its clients in terms of added-value to server sales, specifically in the AI/ML or compute space. For specific enquiries, please contact [info@renderex.ae](mailto:info@renderex.ae).

Alternatively, for general information about RendeRex and it's services, please visit [www.renderex.ae](https://www.renderex.ae).

