---
title: "Methods to adjust large-page memory for Linux instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Method_to_adjust_large_page_memory_for_Linux_instances"
---

This topic describes how to resolve the issue of Linux instance inaccessibility caused by excessively large huge page memory settings by lowering the value of the `vm.nr_hugepages` parameter.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

To improve fault tolerance and ensure data security, we recommend that you [create a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot) for the instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to back up the `/etc/sysctl.conf` file.

   ```Plain Text
   cp /etc/sysctl.conf /etc/sysctl.conf_bak
   ```
   

3. Execute the following command and edit the `/etc/sysctl.conf` file.

   ```Plain Text
   vim /etc/sysctl.conf
   ```
   

4. Press the "A" key to enter edit mode, locate the vm.nr_hugepages configuration item, and lower its value to a reasonable level based on your actual business needs.

5. Press "Shift + :" and then enter `wq`.

6. Press the "Enter" key to save and exit the file.

7. Execute the following command to make the configuration take effect.

   ```Plain Text
   sysctl -p
   ```
