---
title: "EBM FAQs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/EBM-FAQs"
---

<span id="can-i-create-an-ecs-instance-in-an-ebm-instance"></span>
## Can I create an ECS instance in an EBM instance?

Yes. EBM has the full processor features of a physical machine, but it is not recommended to create a virtual machine in an EBM instance, because the performance of the virtual machine will decrease significantly. It is recommended to create an ECS instance directly through the console.

<span id="why-can-t-i-log-in-to-vnc-after-the-ebm-instance-is-created"></span>
## Why can't I log in to VNC after the EBM instance is created?

After the EBM instance is started, that is, after the status changes to **Running**, it takes about 1 minute to start the operating system. At this time, logging in with VNC will prompt an error.

<span id="why-does-the-volume-or-network-interface-fail-to-be-unmounted-and-remains-in-the-unmounting-state-after-the-ebm-instance-is-created"></span>
## Why does the volume or network interface fail to be unmounted and remains in the unmounting state after the EBM instance is created?

After the EBM instance is started, that is, after the status changes to **Running**, it takes about 1 minute to start the operating system. At this time, unmounting the volume or network interface will report an error. It is recommended to run for a few minutes before performing the unmount operation.

If you perform the unmount operation immediately after the instance status changes to **Running**, it is recommended that you first stop the instance, and then restart it to restore the mounted state.
