---
title: "Disabling SELinux"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Disable_SELinux"
---

SELinux is a module built into the Linux kernel that is designed to enhance system security. The feature restricts the permissions for user applications and system servers to access files and network resources. Before migration, you need to disable the SELinux feature on your migration source server to prevent migration failures.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the instance as your migration source server using an account with root permissions.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This topic uses CentOS 7.9 as an example to describe how to disable SELinux on CentOS 7 series Linux instances (including veLinux CentOS Compatible).   </div>
   

2. Execute the following command to view the current SELinux mode.

   ```Plain Text
   getenforce
   ```
   

   In this example, SELinux is in `Enforcing` mode.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c86e58d4442940156d8963467f9dee1b.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">SELinux has the following three modes:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Enforcing: Enforcing mode. In this mode, SELinux logs security warnings and blocks all actions that violate the security policy.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Permissive: Permissive mode. In this mode, SELinux only logs security warnings but does not block actions that violate the security policy.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Disabled: Disabled mode, indicating SELinux is disabled.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This mode indicates that SELinux is disabled.   </div>
   

3. If SELinux is in `Disabled` (disabled) mode, there is no need to disable SELinux. Otherwise, follow the steps below to complete the disabling process.

   1. Execute the following command to set SELinux to the permissive mode.

      ```Plain Text
      setenforce 0
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">After you execute this command, SELinux will be temporarily set to <code>Permissive</code> mode. In this mode, the system does not enforce security policy rules.      </div>
      

   2. Execute the following command to verify that the change succeeded. A value of `permissive` for the `Current mode` parameter indicates SELinux is now in Permissive mode.

      ```Plain Text
      sestatus
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_573632cd78c87ce4cab9e6d0e28b6c2c.png) </span>

   3. Execute the following command to edit the SELinux configuration file.

      ```Plain Text
      vim /etc/selinux/config
      ```
      

   4. Press the `i` key to enter edit mode, and modify the `SELINUX` parameter value to `disabled`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b638b6bdce7d0bb12967838772654e0a.png) </span>

   5. Press `esc` to exit the edit mode, enter `:wq` to save and close the file.

4. Subsequently, you can continue to complete other [preparations](https://docs.byteplus.com/en/docs/smc/Preparations) or perform [migration pre-check](https://docs.byteplus.com/en/docs/smc/Perform-a-migration-precheck) again.
