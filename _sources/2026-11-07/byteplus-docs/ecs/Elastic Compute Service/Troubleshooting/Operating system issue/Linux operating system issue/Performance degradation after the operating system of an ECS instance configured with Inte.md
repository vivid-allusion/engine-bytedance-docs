---
title: "Performance degradation after the operating system of an ECS instance configured with Intel CPU is updated to a Linux public image"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/performance_degradation_after_the_os_updated_to_public"
---

<span id="YmYF9pEg"></span>
## **Cause**

To avoid potential security issues caused by the [Spectre Variant 2](https://www.kernel.org/doc/html/latest/admin-guide/hw-vuln/spectre.html#spectre-variant-2) and [Spectre Variant 4 (Speculative Store Bypass)](https://www.intel.com/content/www/us/en/developer/topic-technology/software-security-guidance/overview.html) vulnerabilities, some Linux public images provided by BytePlus have the CPU vulnerability fixing feature enabled by default. When you use an image with this feature enabled, it may result in performance degradation of the instance.

<span id="glnj3hU9"></span>
## **Solution**

When using Ubuntu, Debian, veLinux, CentOS, RHEL, veLinux CentOS Compatible, or Fedora images, you can refer to the guide to enable or disable the CPU vulnerability fixing feature based on your needs.


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to query the current boot mode of the operating system.

   ```Bash
   if [ -d /sys/firmware/efi ]; then
       echo "UEFI"
   else
       echo "BIOS"
   fi
   ```
   

3. Execute the following commands to enable or disable the CPU vulnerability fixing feature.

   * Enable

      ```Bash
      sed -i "s/ nospectre_v2 nospec_store_bypass_disable//g" /etc/default/grub
      ```
      

   * Disable

      ```Bash
      sed -i "/GRUB_CMDLINE_LINUX=\"/s/\"$/ nospectre_v2 nospec_store_bypass_disable\"/" /etc/default/grub
      ```
      

4. Execute the following command to regenerate the grub file.

   
   <Tabs>
   <Tab zoneid="gjCNB0S0Pw" title="Ubuntu/Debian/veLinux">
   <TabTitle>Ubuntu/Debian/veLinux</TabTitle>
   
   &nbsp;
   
   ```Bash
   update-grub
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="YfEL5bpi9V" title="CentOS/RHEL/veLinux CentOS Compatible">
   <TabTitle>CentOS/RHEL/veLinux CentOS Compatible</TabTitle>
   
   * UEFI boot mode
   
      ```Bash
      grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
      ```
      
   
   * BIOS boot mode
   
      ```Bash
      grub2-mkconfig -o /boot/grub2/grub.cfg
      ```
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="v3fK8uqHhz" title="Fedora">
   <TabTitle>Fedora</TabTitle>
   
   * UEFI boot mode
   
      ```Bash
      grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
      ```
      
   
   * BIOS boot mode
   
      ```Bash
      grub2-mkconfig -o /boot/grub2/grub.cfg
      ```
      
   
   
   
   
   
   </Tab>
   </Tabs>
   

5. Execute the following command to restart the instance for the configuration to take effect.

   ```Bash
   reboot
   ```
   

6. Execute the following command to view the vulnerability status file and check whether the CPU vulnerability fixing feature is enabled.

   ```Bash
   cd /sys/devices/system/cpu/vulnerabilities/
   for i in `ls`;do echo -n $i": ";cat $i;done
   ```
   

   If the output information contains `spectre_v2: Vulnerable` and `spec_store_bypass: Vulnerable`, it indicates that the feature of fixing Spectre Variant 2 and Spectre Variant 4 vulnerabilities on the current CPU is disabled. Otherwise, it is enabled.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a32b9951be1c8439b34e20de9709d0d9.png) </span>
