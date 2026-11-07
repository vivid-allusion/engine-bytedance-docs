---
title: "When starting a service in the Linux instance, the prompt appears: task: Cannot allocate memory"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/When_Linux_instance_starts_the_service_it_prompts_task_Cannot_allocate_memory"
---

You can resolve the error of `task: Cannot allocate memory` that occurs when an ECS instance starts a certain service process by increasing the value of `kernel.pid_max`.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This operation is only applicable to kernel versions earlier than v4.1. For kernel versions v4.1 and later, you can  contact your account manager to obtain technical support.</div>


<span id="oe5oCyY8"></span>
### Causes

It may be caused by the operating system exceeding the limit on the number of processes.

The Linux kernel limits the number of processes through the kernel configuration argument `kernel.pid_max`. When the total number of processes running services exceeds the value of `kernel.pid_max`, creating new processes will result in the system prompting the error `task: Cannot allocate memory`.

<span id="i5mmVPpX"></span>
### Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. View whether the number of processes currently running in the system exceeds the maximum number of processes.

   1. Run the following command to view the number of processes currently running in the system.

      ```Plain Text
      ps -eLf | wc -l
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_145cfd2754a1a5912d243587e2ccab16.png) </span>

   2. Execute the following command to view the maximum number of processes in the system.

      ```Plain Text
      sysctl kernel.pid_max
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9ad40617032b5790ba6124ec4ecc394c.png) </span>

3. If the current number of running processes in the system exceeds the maximum number of processes, please adjust the `kernel.pid_max` configuration item to a reasonable value according to the actual business situation. Once the adjustment is complete, it will take effect immediately.

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the <code>kernel.pid_max</code> value adjustment, it will take effect immediately.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the current number of running processes in the operating system exceeds two\-thirds of the maximum number of processes (<code>kernel.pid_max</code>), it is also recommended to immediately increase the value of kernel.pid_max to avoid affecting subsequent business operations.   </div>
   

   * **Temporary Settings**: Execute any one of the following commands to temporarily increase the value of`kernel.pid_max`. However, it will become invalid after restarting the instance.

      ```Plain Text
      sysctl -w kernel.pid_max=expectedPidMaxValue
      echo expectedPidMaxValue > /proc/sys/kernel/pid_max
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Please replace <code>expectedPidMaxValue</code> in the command with the actual value that <code>kernel.pid_max</code> needs to be raised to.      </div>
      

   * **Permanent Settings**: Execute the following command to permanently increase the value of`kernel.pid_max` regardless of the instance status.

      ```Plain Text
      echo "kernel.pid_max=expectedPidMaxValue" >> /etc/sysctl.conf
      sysctl -p
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Please replace <code>expectedPidMaxValue</code> in the command with the actual value that <code>kernel.pid_max</code> needs to be increased to.      </div>
