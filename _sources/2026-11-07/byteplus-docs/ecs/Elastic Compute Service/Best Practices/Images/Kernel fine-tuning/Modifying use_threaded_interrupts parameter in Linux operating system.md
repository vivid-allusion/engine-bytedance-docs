---
title: "Modifying use_threaded_interrupts parameter in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/use_threaded_interrupts"
---

This topic describes how to modify the `use_threaded_interrupts` parameter in the Linux operating system.

<span id=".5YWz5LqOdXNlX3RocmVhZGVkX2ludGVycnVwdHPlj4LmlbA="></span>
## About the use_threaded_interrupts parameter

This parameter is a kernel module parameter of type `int` (integer). It controls whether threaded interrupt handling is enabled. Enabling Threaded IRQs can improve real\-time performance and responsiveness.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

When you use [an ECS instance with NVMe SSD local storage](https://docs.byteplus.com/en/docs/ecs/Local-volumes#.5pys5Zyw55uY57G75Z6L), all I/O interrupts may be routed to a single CPU. If the software interrupt (SI) load on that CPU reaches 100%, failures may occur. You can enable threaded interrupts through the `use_threaded_interrupts` parameter to improve real\-time performance and responsiveness.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In this solution, a new irq process is added, which increases the CPU overhead of the instance and occupies part of the CPU resources.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to enable threaded interrupts by modifying the `use_threaded_interrupts` parameter.

   ```Plain Text
   rmmod nvme nvme_core
   modprobe nvme use_threaded_interrupts=1
   ```
   

3. After you modify the parameter, you can use the FIO command to test the volume performance by following instructions provided in [Testing local volume performance](https://docs.byteplus.com/en/docs/ecs/Testing-local-volume-performance).
