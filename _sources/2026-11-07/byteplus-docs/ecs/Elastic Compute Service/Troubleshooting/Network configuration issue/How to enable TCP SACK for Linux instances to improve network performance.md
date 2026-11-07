---
title: "How to enable TCP SACK for Linux instances to improve network performance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Method_Linux_Configure_Static_IP_Address_for_Instance"
---

You can enable TCP SACK on a Linux instance to improve the network performance of the instance.

> This section uses the veLinux2.0 version system as an example. The procedure might vary slightly for other versions. Refer to your actual environment for details.


<span id="KJ9jbZtJ"></span>
### Procedure


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run the following command to access the `/etc/sysctl.conf` file.

   ```Shell
   vim /etc/sysctl.conf
   ```
   

3. Enable TCP SACK.

   
   |Does **net.ipv4.tcp_sack\-related configuration** exist? |Procedure |
   |---|---|
   |The configuration related to net.ipv4.tcp_sack exists. |1. Press "i" to enter edit mode.<br><br>2. Modify `net.ipv4.tcp_sack = X` to `net.ipv4.tcp_sack = 1`.<br><br>3. Press Esc to exit the editing mode.<br><br>4. Type `:wq`, and press Enter to save and exit. |
   |The configuration related to net.ipv4.tcp_sack does not exist. |1. Press the "i" key to enter the editing mode.<br><br>2. Add the following configuration at the bottom of the file.<br><br>   ```Bash```<br>```   net.ipv4.tcp_sack = 1```<br>```   ```<br>   <br><br>   The system displays information similar to the following.<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1f8f38cb6dcd09bda3337197d2bafee9.png) </span><br><br>3. Press Esc to exit the editing mode.<br><br>4. Type `:wq`, and press Enter to save and exit. |
   

4. Execute the following command to make the configuration take effect.

   ```Shell
   sysctl -p
   ```
   


<span id="BU9sRmRm"></span>
##
