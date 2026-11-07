---
title: "Disabling AppArmor service"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Disable-AppArmor-Services"
---

AppArmor is a security enhancement tool that confines applications by defining their access to files, directories, and network resources. Before migration, you need to disable the AppArmor service on your migration source server to prevent migration failures.

This topic uses an Ubuntu 20.04 LTS 64\-bit instance as an example to describe how to disable the AppArmor service.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target server.

2. Execute the following command to view the AppArmor running status.

   ```Plain Text
   sudo apparmor_status
   ```
   

   If the following output is displayed, it indicates that AppArmor is enabled. Proceed with the following steps to disable it. Otherwise, AppArmor is already disabled and no action is required.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c7ab5a76ce3bfc52ba9b135760006688.png) </span>

   1. Execute the following command to stop AppArmor.

      ```Plain Text
      sudo systemctl stop apparmor
      ```
      

   2. Execute the following command to prevent AppArmor from starting automatically at boot.

      ```Plain Text
      sudo systemctl disable apparmor 
      ```
      

   3. Execute the following command to completely remove the AppArmor security enhancement tool and related configurations.

      ```Plain Text
      sudo apt-get purge -y apparmor apparmor-utils && sudo rm -rf /etc/apparmor /etc/apparmor.d && sudo modprobe -r apparmor
      ```
      

3. Subsequently, you can continue to complete other [preparations](https://docs.byteplus.com/en/docs/smc/Preparations) or [perform migration pre-check](https://docs.byteplus.com/en/docs/smc/Perform-a-migration-precheck) again.
