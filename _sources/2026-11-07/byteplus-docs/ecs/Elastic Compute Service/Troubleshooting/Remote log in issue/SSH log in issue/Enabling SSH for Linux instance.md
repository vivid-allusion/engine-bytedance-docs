---
title: "Enabling SSH for Linux instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Enable-SSH-on-Linux-instance"
---

When you log in to a Linux ECS instance, you need to first log in via VNC to enable SSH. Otherwise, you will not be able to establish a remote connection using the ECS Terminal or third\-party tools.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">ECS instances that you purchase by using BytePlus public images have SSH enabled by default.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. [Log in to the Linux instance in the console](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to enable SSH.

   ```Plain Text
   sudo systemctl start sshd
   ```
   

3. Execute the following command to view SSH status.

   ```Plain Text
   sudo systemctl status sshd
   ```
   

4. If the following output is displayed, SSH is enabled.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_502c95564cf1f2bdfe88b347d5e31a66.png) </span>
