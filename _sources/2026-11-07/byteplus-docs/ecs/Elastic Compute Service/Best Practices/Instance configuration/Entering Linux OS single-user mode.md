---
title: "Entering Linux OS single-user mode"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Booting-in-single-user-mode"
---

This topic describes how to enter single\-user mode on Linux instances via the system bootloader (GRUB).

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

Single\-user mode is a runlevel (also called a system state) of Linux systems. In this mode, the system starts only the most basic services and processes, and the operator has administrator privileges to modify all system configurations. You can use this mode to troubleshoot and maintain the system, such as diagnosing system faults, changing usernames or passwords, and managing disk partitions.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Because single\-user mode grants full access to the underlying system layers, operations performed in this mode may have a significant impact on the system. We recommend that you enter this mode only when necessary, and proceed with extreme caution to avoid accidental damage to system files or data.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="vQYnXqTCuO" title="veLinux OS">
<TabTitle>veLinux OS</TabTitle>

In the example provided in this section, veLinux 1.0 64 bit is used.


1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) via VNC.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you log in to the instance via ECS Terminal, you cannot access the system startup page directly when you restart the instance using a command. Therefore, we recommend that you do not use this login method.   </div>
   

2. On the left side of the login page, click buttons to restart the instance as instructed in the following picture.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8510f093467510646b3c11832096b6f.png) </span>

3. When the kernel option page appears, quickly press the `↑` key to enter the page to select the kernel.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f2843091036c73313a98230a496ac0e6.png) </span>

4. After you position the cursor on the target kernel, press E to enter the kernel editing page.

5. Use the arrow keys to move the cursor to the line starting with linux, and then replace `ro` and everything after it on that line with `rw quiet init=/bin/bash`.

   Before change:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_79114925d33d4794e84e376f2444de11.png) </span>

   After change:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a532eb602867b46cb6c6d729b0a38bed.png) </span>

6. Press `F10` , or press `Ctrl`+ `X` to enter single\-user mode.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ba5e6a5a7f80b735defd02d39579bdf9.png) </span>


</Tab>
<Tab zoneid="AgfNj6z1kW" title="CentOS OS">
<TabTitle>CentOS OS</TabTitle>

In the example provided in this section, CentOS 7.6 64 bit is used.


1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) via VNC.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In instances logged in via ECS Terminal, you can not access the system startup page directly when restarting them via command. Therefore, we <strong>do not recommend</strong> using this login method.   </div>
   

2. On the left side of the login page, click buttons to restart the instance as instructed in the following picture.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8510f093467510646b3c11832096b6f.png) </span>

3. When the kernel option page appears, quickly press the `↑` key to enter the page to select the kernel.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2124958eca2867fb83ae08e6ff7d5d58.png) </span>

4. After you position the cursor on the target kernel, press the `e` key to enter the page to edit the kernel.

5. On this page, use the keyboard arrow keys to move the cursor to the line starting with "`linuxefi`". After this, replace `ro` in this line and the content following it to the end with `rw init=/bin/bash`.

   Before change:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_31476a00f3a4c9a5b5d3a079cac49660.png) </span>

   After change:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c91710c624166d13794b6611c347650.png) </span>

6. Press `F10`, or press `Ctrl+X` to enter single\-user mode.

   <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_87f6c889efd805b99db6b47d94bab94c) </span>


</Tab>
<Tab zoneid="eDydNW059r" title="Ubuntu OS">
<TabTitle>Ubuntu OS</TabTitle>

In the example provided in this section, Ubuntu 20.04 64 bit is used.


1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) via VNC.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In instances logged in via ECS Terminal, you can not access the system startup page directly when restarting them via command. Therefore, we <strong>do not recommend</strong> using this login method.   </div>
   

2. On the left side of the login page, click buttons to restart the instance as instructed in the following picture.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8510f093467510646b3c11832096b6f.png) </span>

3. During restart, press and hold the `shift` key to enter the GRUB interface.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">On some computers, you can also press <code>Esc</code> to enter the GRUB interface.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2bb09fc1334bc270596711e42b66d7cb.png) </span>

4. Use the keyboard arrow keys to navigate to "Advanced options for Ubuntu", and then press the `enter` key.

5. Press the `e` key to enter the page to edit the kernel.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a71eac296e5d1486b8c85ea91731cf48.jpeg) </span>

6. Use the keyboard arrow keys to move the cursor to the "linux" line. After this, replace `ro` in this line and the content following it to the end with `rw single init=/bin/bash`.

   Before change:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ae99ad9cb6664b8919fa46dd80f49572.png) </span>

   After change:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_492a7afad7c88286e838b9dc99bae6ae.jpeg) </span>

7. Press the `F10` key or the `ctrl`+`x` key combination to enter the system single\-user mode.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c826c02084cff547b2f74711edf544d5.png) </span>


</Tab>
<Tab zoneid="aKyYwHlLR8" title="Debian OS">
<TabTitle>Debian OS</TabTitle>

In the example provided in this section, Debian 10 64 bit is used.


1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) via VNC.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In instances logged in via ECS Terminal, you can not access the system startup page directly when restarting them via command. Therefore, we <strong>do not recommend</strong> using this login method.   </div>
   

2. On the left side of the login page, click buttons to restart the instance as instructed in the following picture.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8510f093467510646b3c11832096b6f.png) </span>

3. After you enter the system selection page, quickly press the `↑` key to enter the page to select the kernel.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_336b91ecabb015343a9bdd6abe59dbc1.png) </span>

4. After you position the cursor on the target kernel, press the `e` key to enter the page to edit the kernel.

5. Use the keyboard arrow keys to move the cursor to the "`linux`" line. After this, replace `ro` in this line and the content following it with `rw quiet init=/bin/bash`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1a9e94c2e239372e1f16038add0324a.png) </span>

6. Press the `F10` key or the `ctrl`+`x` key combination to start the system and enter single\-user mode.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_47cef92c4f7efa2b5460e66fbdb8a884.png) </span>


</Tab>
<Tab zoneid="wyoT9ibtWh" title="OpenSUSE OS">
<TabTitle>OpenSUSE OS</TabTitle>

In the example provided in this section, OpenSUSE 15.4 64 bit is used.


1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) via VNC.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In instances logged in via ECS Terminal, you can not access the system startup page directly when restarting them via command. Therefore, we <strong>do not recommend</strong> using this login method.   </div>
   

2. On the left side of the login page, click buttons to restart the instance as instructed in the following picture.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8510f093467510646b3c11832096b6f.png) </span>

3. During the instance restart, enter the system selection page, and then quickly press the `e` key to enter the page to edit the kernel.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9be205f40497b251b98f3009e04d2f0b.png) </span>

4. Use the keyboard arrow keys to move the cursor to the kernel boot line, and then replace the content after `UUID=root=*****` with `init=/bin/bash`.

   Before change:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6c7d3496224ed43219f2d887c4fac198.png) </span>

   After change:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_309c8d5cbae8c4de7a8bd8045d2df41a.png) </span>

5. Press the `F10` key or the `ctrl`+`x` key combination to start the system and enter single\-user mode.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a34b2db28969a5ccafdfdab25edf8f40.png) </span>


</Tab>
<Tab zoneid="vI5Wi9E7FO" title="Fedora OS">
<TabTitle>Fedora OS</TabTitle>

In the example provided in this section, Fedora 33 64 bit is used.


1. [Log in to the ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance) via VNC.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In instances logged in via ECS Terminal, you can not access the system startup page directly when restarting them via command. Therefore, we <strong>do not recommend</strong> using this login method.   </div>
   

2. On the left side of the login page, click buttons to restart the instance as instructed in the following picture.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d8510f093467510646b3c11832096b6f.png) </span>

3. After you enter the system selection page, quickly press the `↑` key to enter the page to select the kernel.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_967f150779159b182dc5b21658e00168.jpeg) </span>

4. After you position the cursor on the target kernel, press the `e` key to enter the page to edit the kernel.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1fdc0dc4ca0189826abaadd514361e0c.png) </span>

5. Use the keyboard arrow keys to move the cursor to the "linux" line. After this, replace `ro` in this line and the content following it to the end with `rw single init=/bin/bash`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d77ea602d4e7e188d9b1e45f3dd5c953.png) </span>

6. Press the `F10` key or the `ctrl`+`x` key combination to start the system and enter single\-user mode.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f3e604b95cad9d267961b2a5c4faa63f.png) </span>


</Tab>
</Tabs>
