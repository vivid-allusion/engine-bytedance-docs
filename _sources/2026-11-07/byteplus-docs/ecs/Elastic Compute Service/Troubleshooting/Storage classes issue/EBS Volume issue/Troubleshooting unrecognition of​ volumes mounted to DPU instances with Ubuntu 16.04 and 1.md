---
title: "Troubleshooting unrecognition of​ volumes mounted to DPU instances with Ubuntu 16.04 and 18.04"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/resolve_the_issue_of_being_unable_to_recognize_the_Volume_within_the_instance"
---

<span id="LZ2OMKhq"></span>
## Issue description​

After you mount a volume on a DPU ECS instance running Ubuntu 16.04 or 18.04 (for example,[ General-purpose g3i/g3a](https://docs.byteplus.com/en/docs/ecs/General-purpose),[ Compute-optimized c3i/c3a](https://docs.byteplus.com/en/docs/ecs/Computing-optimized), and [Memory-optimized r3i/r3a](https://docs.byteplus.com/en/docs/ecs/Memory-optimized)), the instance can not recognize the newly mounted volume.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a83d3bcfa6858cf5f940017d3d22d4ca.png) </span>

<span id="0zdqdZkj"></span>
## Causes

This may be because the /etc/udev/rules.d/72\-virtio.rules file and its configuration are missing from your operating system. As a result, the DPU\-architecture instance fails to recognize the newly mounted volume.

<span id="LnyhkFjK"></span>
## Solutions

You need to create the /etc/udev/rules.d/72\-virtio.rules file and configure it on the operating system.


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to confirm whether the /etc/udev/rules.d/72\-virtio.rules file exists.

   ```Plain Text
   find /etc/udev/rules.d/ -name "72-virtio.rules"
   ```
   

   If the output is displayed as follows, the /etc/udev/rules.d/72\-virtio.rules file is missing from your operating system. Follow the subsequent steps to resolve the issue. 

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0cd81e49b3579985fe5d2d540718345a.png) </span>

3. Create the /etc/udev/rules.d/72\-virtio.rules file.

   1. Execute the following command to create the /etc/udev/rules.d/72\-virtio.rules file.

      ```Plain Text
      touch /etc/udev/rules.d/72-virtio.rules
      ```
      

   2. Execute the following commands to modify the Virtio driver configurations.

      ```Plain Text
      cat <<EOF > /etc/udev/rules.d/72-virtio.rules
      ACTION=="add" \
      , ATTRS{device}=="0x1042" \
      , ATTRS{vendor}=="0x1af4" \
      , SUBSYSTEM=="virtio" \
      , RUN+="/etc/initramfs-tools/scripts/init-premount/rebind.sh"
      ACTION=="add" \
      , ATTRS{device}=="0x1041" \
      , ATTRS{vendor}=="0x1af4" \
      , SUBSYSTEM=="virtio" \
      , RUN+="/etc/initramfs-tools/scripts/init-premount/rebind.sh"
      ACTION=="add" \
      , ATTRS{device}=="0x1001" \
      , ATTRS{vendor}=="0x1af4" \
      , SUBSYSTEM=="virtio" \
      , RUN+="/etc/initramfs-tools/scripts/init-premount/rebind.sh"
      ACTION=="add" \
      , ATTRS{device}=="0x1000" \
      , ATTRS{vendor}=="0x1af4" \
      , SUBSYSTEM=="virtio" \
      , RUN+="/etc/initramfs-tools/scripts/init-premount/rebind.sh"
      EOF
      ```
      

4. [Dismount](https://docs.byteplus.com/en/docs/ecs/Detach-volume) the unrecognized volume in the console, and [mount](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume) it again.

5. Execute the `lsblk` command in the instance to verify whether the newly mounted volume is recognized as expected.

   If the following output is displayed, the newly mounted volume is recognized as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b311543233aa6140de0cf96303dd2b88.png) </span>
