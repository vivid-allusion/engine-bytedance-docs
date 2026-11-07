---
title: "How to modify the kernel argument kernel.unknown_nmi_panic for a Linux instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Linux_instance_how_to_adjust_the_kernel_parameter_kernel_unknown_nmi_panic"
---

You can set the kernel parameter `kernel.unknown_nmi_panic` of a Linux ECS instance system to `0` to resolve the instance restart issue caused by unexpected kernel panic.

<span id="RVVALYgS"></span>
### Causes

The kernel parameter `kernel.unknown_nmi_panic` controls the kernel's behavior when an unknown non\-maskable interrupt is encountered. On most Linux distributions, the default value of this parameter is `0`, which means unknown non\-maskable interrupts are ignored. If the value of `kernel.unknown_nmi_panic` is adjusted for any reason, the kernel may trigger a panic upon receiving an unknown non\-maskable interrupt, causing the instance to restart.


* kernel.unknown_nmi_panic = 1: The kernel will consider a system error when encountering unknown non\-maskable interrupts and will trigger a kernel panic, causing unexpected instance restarts or business interruptions.

* kernel.unknown_nmi_panic = 0: Ignore the issue without further processing, maintaining the current status of the instance to continue running.


<span id="vNnlsFfA"></span>
### Procedure


<Tabs>
<Tab zoneid="GyRY2INwdv" title="Configure the kernel.unknown_nmi_panic argument (permanent)">
<TabTitle>Configure the kernel.unknown_nmi_panic argument (permanent)</TabTitle>

1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to check whether the kernel configuration related to the kernel parameter `kernel.unknown_nmi_panic` exists.

   ```Plain Text
    grep 'kernel.unknown_nmi_panic' /etc/sysctl.conf /etc/sysctl.d/*.conf
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3b7cb894314b2f03ea96b27ebe320227.png) </span>

   * If there is a related kernel configuration, only retain `/etc/sysctl.conf` file's `kernel.unknown_nmi_panic = 0` entry.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the <code>/etc/sysctl.conf</code> file contains extra kernel configurations, it is recommended to use <code>#</code>to add comments.      </div>
      

   * If no such configuration exists, add kernel.unknown_nmi_panic = 0 to the end of the `/etc/sysctl.conf` file.

3. Execute the following command to make the configuration take effect.

   ```Plain Text
   sudo sysctl -p
   ```
   





</Tab>
<Tab zoneid="xOsFxXNGGk" title="Configure the kernel.unknown_nmi_panic argument (temporary)">
<TabTitle>Configure the kernel.unknown_nmi_panic argument (temporary)</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If you do not want to reload the kernel argument configuration file, you can temporarily configure the kernel argument.</div>


* <div data-tips="true" data-tips-type="default">The temporary settings take effect immediately but will become invalid after the instance restarts. The kernel parameter will revert to the value in the configuration file before the temporary settings are applied.</div>




&nbsp;

1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Run the following command to check if the kernel argument `kernel.unknown_nmi_panic` exists in the kernel configuration.

   ```Plain Text
    grep 'kernel.unknown_nmi_panic' /etc/sysctl.conf /etc/sysctl.d/*.conf
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3b7cb894314b2f03ea96b27ebe320227.png) </span>

3. Run the following command to change the value of the kernel argument `kernel.unknown_nmi_panic` to `0`.

   ```Bash
   sysctl -w kernel.unknown_nmi_panic=0
   ```
   





</Tab>
</Tabs>
