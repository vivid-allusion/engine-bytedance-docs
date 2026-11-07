---
title: "Why does prolonged high I/O or unresponsiveness occur before OOM in veLinux 1.0 CentOS Compatible Edition image compared to a community-version CentOS image?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/experience_a_prolonged_period_of_high_I_O_or_unresponsiveness_before_OOM"
---

<span id="7CcqlKo9"></span>
## **Causes**

The kernel version of the veLinux 1.0 CentOS Compatible Edition image is 5.x, which is higher than that of the community CentOS image. Kernels of higher versions have more aggressive memory reclamation policies.

In scenarios involving high performance, availability, and throughput (for example, high\-concurrency web servers, big data processing, and virtualized environments), a more aggressive memory reclamation policy can help you utilize memory, reduce memory fragmentation, and avoid OOM events more effectively. However, when memory usage reaches the limit, the kernel of a higher version typically spends more time reclaiming memory. At the same time, binary files of system services are frequently swapped in and out, causing increased system I/O load. This may cause degraded system performance or even an unresponsive system.

<span id="TyteYRU4"></span>
## **Solutions**

Given the mentioned reasons, you can set a memory upper limit for services to prevent memory usage from reaching the limit, or use a CentOS image with a lower kernel version to avoid this issue.

Reference solutions are as follows:


* Limit the memory of a process

   1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

   2. Execute the following command to set the memory limit for the target service.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code>xx.service</code> with the target service.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code>100M</code> with the memory limit you need. Unit: <code>MB</code>.      </div>
      

      ```Plain Text
      systemctl set-property xxx.service MemoryLimit=100M
      ```
      

   3. Execute the following command to confirm whether the memory limit of the target service is successfully modified.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace <code>xxx.service</code> with the target service.      </div>
      

      ```Plain Text
      systemctl status xxx.service
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fa8aca59175966b3b4b00d33548d523a.png) </span>

* Use a CentOS image with kernel version 3.x. For more information, see [Changing operating systems](https://docs.byteplus.com/en/docs/ecs/Changing-OS).
