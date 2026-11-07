---
title: "What do I do if performance degradation occurs on ECS instances using AMD CPUs after I update the operating system or kernel?"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/AMD_CPUs_update_the_operating_system_or_upgrade_the_kernel"
---

<span id="VbukMDBN"></span>
## **Causes**

The latest version of the operating system has the AMD SRSO vulnerability patches integrated and enabled by default. Enabling such patches may cause a significant performance degradation of the instance.

<span id="pmKmGqkO"></span>
## **Solutions**


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to check the currently active security mitigations.

   ```Plain Text
   grep . /sys/devices/system/cpu/vulnerabilities/*
   ```
   

3. If "Safe RET" exists in the security mitigations for `spec_rstack_overflow`, the kernel has enabled security mitigations for SRSO. However, this may cause a significant performance degradation in some applications.

   If you trust user\-space applications and want to avoid performance issues, follow these steps to add the `spec_rstack_overflow=off` kernel parameter to the kernel command line and restart the instance to forcefully disable SRSO security mitigations.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">AMD believes that the overall security risk associated with SRSO is low in common cloud environments. Therefore, AMD considers it reasonable for ECS users to disable SafeRET. <a href="https://www.amd.com/content/dam/amd/en/documents/epyc-technical-docs/white-papers/amd-epyc-9004-wp-srso.pdf">Learn more</a>.   </div>
   

   
   <Tabs>
   <Tab zoneid="Xti4fQZTPW" title="RHEL, CentOS, AlmaLinux, Rocky Linux, and Fedora operating systems">
   <TabTitle>RHEL, CentOS, AlmaLinux, Rocky Linux, and Fedora operating systems</TabTitle>
   
   1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).
   
   2. Execute the following command to add the parameter for disabling SRSO to the grub file.
   
      ```Plain Text
      sudo sed -i "/GRUB_CMDLINE_LINUX=\"/s/\"$/ 
      spec_rstack_overflow=off\"/" /etc/default/grub
      ```
      
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To enable SRSO, execute the <code>sudo sed -i "s/ spec_rstack_overflow=off//g" /etc/default/grub</code> command.   </div>
      
   
   3. Execute the following command to generate a new grub file.
   
      ```Plain Text
        sudo grub2-mkconfig -o /boot/grub2/grub.cfg
      ```
      
   
   4. Execute the following command to restart the instance for the configuration to take effect.
   
      ```Plain Text
      sudo reboot
      ```
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="OJneyeH4qJ" title="veLinux, Debian, and Ubuntu operating systems">
   <TabTitle>veLinux, Debian, and Ubuntu operating systems</TabTitle>
   
   1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).
   
   2. Execute the following command to add the parameter for disabling SRSO to the grub file.
   
      ```Plain Text
      sudo sed -i "/GRUB_CMDLINE_LINUX=\"/s/\"$/ 
      spec_rstack_overflow=off\"/" /etc/default/grub 
      ```
      
   
      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
      
   
      <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To enable SRSO, execute the <code>sudo sed -i "s/ spec_rstack_overflow=off//g" /etc/default/grub</code> command.   </div>
      
   
   3. Execute the following command to generate a new grub file.
   
      ```Plain Text
      sudo update-grub2
      ```
      
   
   4. Execute the following command to restart the instance for the configuration to take effect.
   
      ```Plain Text
      sudo reboot
      ```
      
   
   
   
   
   </Tab>
   </Tabs>
   

&nbsp;


&nbsp;
