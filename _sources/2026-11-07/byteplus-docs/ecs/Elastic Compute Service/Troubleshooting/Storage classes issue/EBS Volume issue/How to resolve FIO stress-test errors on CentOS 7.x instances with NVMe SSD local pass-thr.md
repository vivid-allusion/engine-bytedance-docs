---
title: "How to resolve FIO stress-test errors on CentOS 7.x instances with NVMe SSD local pass-through disks?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/fio-command"
---

<span id=".6Zeu6aKY5o-P6L-w"></span>
## Issue description

When the `fio` command is executed to stress test a local volume on a [Local SSD](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based) instance running with CentOS 7, the error `NMI watchdog: BUG: soft lockup - xxx` occurs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1633d94693aaeeac4aa125b2526b19a3.png) </span>

<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

Due to a kernel bug in the CentOS 7.x operating system, all I/O interrupts of the NVMe SSD local pass\-through disk are sent to one CPU. As a result, a failure occurs when the software interrupt (SI) of this CPU reaches `100`.

<span id=".6Kej5Yaz5pa55qGI"></span>
## Solutions

Execute the following commands in the faulty instance.

```Plain Text
rmmod nvme nvme_core
modprobe nvme use_threaded_interrupts=1
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In this solution, a new irq process is added, which increases the CPU overhead of the instance and occupies part of the CPU resources.</div>
