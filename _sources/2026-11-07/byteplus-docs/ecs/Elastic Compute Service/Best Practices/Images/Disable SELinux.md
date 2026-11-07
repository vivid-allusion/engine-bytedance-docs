---
title: "Disable SELinux"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Close-SELinux"
---

This article uses CentOS 7.9 as an example to show how to turn off SELinux in an instance Linux CentOS 7 (including veLinux CentOS compatible) family.

<span id="what-is-selinux"></span>
## What is SELinux?

SELinux (Security Enhanced Linux) is a functional module integrated in the Linux kernel to enhance system security, which can restrict the permissions of user programs and system servers to access files and network resources through mandatory access control policies.

<span id="operation-scene"></span>
## Operation scene

Before using the Server Migration Center (SMC) to migrate the source of the Linux operating system, you need to turn off the SELinux function of the migration source server to avoid data migration failure.

<span id="operation-steps"></span>
## Operation steps


1. Log in to your migration source server instance with root privileges.

2. Execute the following command to view the current SELinux mode.

   ```Plain Text
   getenforce
   ```
   

   In this example, SELinux is in `Enforcing`mode.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c86e58d4442940156d8963467f9dee1b.png) </span>

   SELinux has the following three modes:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Enforcing:</strong> Enforcing mode, which means logging security warnings and blocking all suspicious behavior that violates security policies.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Permissive:</strong> Permissive mode that only logs security warnings but does not prevent suspicious behavior that violates security policies.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><strong>Disabled:</strong> Disable mode, which means disable SELinux.   </div>
   

> <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">This mode indicates that SELinux is turned off.</div>



3. Close SELinux.

   * Temporarily shut down SELinux and the instance will be restored to the mode set in the configuration file after restarting.

      1. Set SELinux to permissive mode by executing the following command.

         ```Plain Text
         setenforce 0
         ```
         

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">This command temporarily sets SELinux to <code>Permissive</code>mode, does not enforce security policy rules, and implements a temporary shutdown.         </div>
         

      2. Execute the following command to confirm that the `Current mode` parameter value is `permissive`, which means the modification is successful.

         ```Plain Text
         sestatus
         ```
         

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_573632cd78c87ce4cab9e6d0e28b6c2c.png) </span>

   * Permanently shut down SELinux, and the instance will remain in closed SELinux mode after restarting.

      1. Edit the SELinux configuration file by executing the following command.

         ```Plain Text
         vim /etc/selinux/config
         ```
         

      2. Press `i` to enter edit mode and change the `SELINUX`parameter value to `disabled`.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b638b6bdce7d0bb12967838772654e0a.png) </span>

      3. Press `esc` to exit editing mode, enter `: wq` to save and exit the file.

      4. Execute the following command to restart the instance.

         ```Plain Text
         reboot
         ```
         

      5. Execute the following command to confirm that the SELinux status is **disabled** , which means the modification is successful.

         ```Plain Text
         sestatus
         ```
         

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f3e74daea2bb91f502f7704df54442b9.png) </span>
