---
title: "Configuring panic-induced crash restart feature in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/kernel-panic"
---

When a server crashes due to a kernel panic, the applications running on the server are also interrupted. If your applications can be restored by restarting the server, you can configure the panic\-induced crash restart feature for the server by following the instructions provided in this topic.

## Terms

### About kernel panic

A kernel panic refers to a fatal internal error detected within an operating system, such as a hardware failure or a memory access error. When a kernel panic is triggered, the kernel prints as much log information as possible to assist with troubleshooting. Without special configuration, once log printing is finished, the system enters the crashed state: no input response, no new logs, and interrupted user applications.

### Startup parameter panic

The Linux kernel provides the `panic` parameter to specify the behavior of the server when a panic\-induced crash is triggered.

* `panic=0`: The server is in the crashed state and does not restart. This is the default behavior.

* `panic=n (n > 0)`: The server restarts `n` seconds after a panic\-induced crash.

* `panic=n (n < 0)`: The server restarts immediately when a panic\-induced crash occurs.

## Procedure

### Step 1: Configure panic\-induced crash restart

#### Method 1: Configuration by using the proc interface

Execute the following command on the target Linux instance to configure the `panic` parameter by using the proc interface.

> **tip**

* > This method allows configuration changes to be made and applied while the system is running. However, the configuration will reset after an operating system restart and must be reconfigured.

* > Replace `5` in the command with your desired restart time (in seconds) for a panic\-induced crash. For example, you can execute the following command to specify that the server restarts 5 seconds after a panic\-induced crash.

```Plain Text
echo 5 > /proc/sys/kernel/panic
```

#### Method 2: Configuration by using the grub file

> **tip**

* > This method requires an operating system restart for the configuration to take effect. Once restarted, the configuration persists and does not need to be reconfigured.

* > Replace `5` in the command with your desired restart time (in seconds) for a panic\-induced crash. For example, you can execute the following command to specify that the server restarts 5 seconds after a panic\-induced crash.

1. Execute the following command on the target Linux instance to add the panic\-induced crash restart parameter to the grub file.

   ```Plain Text
   sed -i "/GRUB_CMDLINE_LINUX=/s/\"$/ panic=5 \"/" /etc/default/grub
   ```

2. Execute the following command to persist the parameter configuration to the grub file. After the command is executed, restart the operating system. The configuration takes effect after the operating system is restarted and you do not need to configure the parameter again.

   * Centos

      * Legacy boot mode

         ```Plain Text
         grub2-mkconfig -o /boot/grub2/grub.cfg
         ```

      * UEFI boot mode

         ```Plain Text
         grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
         ```

   * Debian

      * Legacy boot mode

         ```Plain Text
         grub-mkconfig -o /boot/grub2/grub.cfg
         ```

      * UEFI boot mode

         ```Bash
         grub-mkconfig -o /boot/efi/EFI/debian/grub.cfg
         ```

   * Ubuntu

      * Legacy boot mode

         ```Plain Text
         grub-mkconfig -o /boot/grub2/grub.cfg
         ```

      * UEFI boot mode

         ```Plain Text
         grub-mkconfig -o /boot/efi/EFI/ubuntu/grub.cfg
         ```

3. Execute the following command to restart the instance for the configuration to take effect.

   ```Plain Text
   reboot
   ```

### Step 2: Verify configuration

> **warning**

> When the operating system is configured with the kdump service, the server does not remain in the crashed state when a panic occurs. Instead, the server executes the kdump process. In this case, the restart behavior is not controlled by the `panic` parameter.

#### Verify configuration specified by using the proc interface

1. Execute the following command on the target Linux instance to trigger a panic\-induced crash.

   ```Plain Text
   echo c > /proc/sysrq-trigger
   ```

2. Check whether the server automatically restarts when it crashes.

#### Verify configuration specified by using the grub file

1. Execute the following command on the target Linux instance, and view the output to check whether it contains the panic parameter.

   ```Plain Text
     cat /proc/cmdline | grep 'panic'
   ```

   Sample output of configuration success

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_937fb78868b7ac215e66850193567cbf.png)

2. Execute the following command to trigger a panic\-induced crash.

   ```Plain Text
   echo c > /proc/sysrq-trigger
   ```

3. Check whether the server automatically restarts when it crashes.
