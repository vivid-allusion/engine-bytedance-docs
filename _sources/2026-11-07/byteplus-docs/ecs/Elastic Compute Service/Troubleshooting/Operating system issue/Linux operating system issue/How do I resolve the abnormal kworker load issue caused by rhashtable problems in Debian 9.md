---
title: "How do I resolve the abnormal kworker load issue caused by rhashtable problems in Debian 9?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/kworker_workload_exception_in_Debian_9"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Problem description

In the Debian 9 (EOL) operating system, there is a probability that the kernel kworker process occupies nearly 100% of the CPU even under low\-load conditions.

**Problem description:** 

When I use the `top` command to view the CPU usage of the instance, the kernel kworker process occupies 100% of the CPU.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a0278d2969cb50eec5ba26c645acfc1f.png) </span>

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

This issue occurs because when the server runs workloads with a large number of bursty fragmented packets, it may get stuck in a state where the `rht_shrink()` function returns `-EEXIST`. This triggers continuous rescheduling of the delayed work of the hash table, thereby occupying the CPU core.


* [Learn more.](https://lkml.org/lkml/2019/1/23/789)

* [Fix Patch](https://github.com/torvalds/linux/commit/408f13ef358aa5ad56dc6230c2c7deb92cf462b1)


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions


* **Solution 1: Replace the operating system**

   We recommend that you [replace the operating system of the server](https://docs.byteplus.com/en/docs/ecs/Changing-OS) with a non\-EOL distribution, such as Debian 12.

* **Solution 2: Install a newer version of the kernel**

   In the Backports repository of Debian 9, this issue has been fixed in the kernel version `4.19+105+deb10u4~bpo9+1`. You can upgrade the kernel version based on your needs. [Learn more](https://docs.byteplus.com/en/docs/ecs/Replace_the_Linux_operating_system_kernel_version).
