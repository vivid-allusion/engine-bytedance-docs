---
title: "Configuring static IP address (Static mode) for Linux instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Linux_how_to_enable_TCP_SACK_to_improve_network_performance"
---

This topic mainly describes how to change the default network configuration (DHCP mode) of the Linux operating system to Static mode.


> * Operating system: In this example, the ECS instance runs CentOS 8. The procedure may vary slightly depending on the operating system version. Please refer to the actual version.

> * Static mode refers to manually configuring certain network parameters for network devices instead of obtaining them automatically through dynamic protocols.


<span id="VSepkiUA"></span>
## Procedure

<span id="vO85M1rj"></span>
### **Step 1: View and record the network parameters of the instance**


1. Log in to the target instance. For operation details, refer to [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Obtain the instance's IP address, subnet mask, and gateway information to use in "**Step 2: Modify the network type of the ECS instance**."

   1. Run the following command to view the instance's IP address and subnet mask.

      ```Shell
      ifconfig
      ```
      

      The system displays information similar to the following:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cfa64d06f3774c17b4fe64e02ad72869.png) </span>

   2. Run the following command to view the instance's gateway information.

      ```Shell
      route -n
      ```
      

      The system displays information similar to the following:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9bc3842b03f57f9118edeac44a917811.png) </span>


<span id="jLFOfVQi"></span>
### **Step 2: Modify the network configuration mode of the ECS instance**


1. Run the following command to modify the configuration file.

   ```Shell
   vim /etc/sysconfig/network-scripts/ifcfg-eth0
   ```
   

2. In the response message, please change the value of BOOTPROTO to **`static`**, and input the IP address, gateway information, and subnet mask obtained in **Step 1: View and record the network arguments of the instance** into this configuration file.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_52e7e202188c580ee74b6c87107ac1e7.png) </span>

3. Type `:wq` and press Enter to save and exit.

4. Run the following command to restart the network service and apply the configuration.

   ```Shell
   systemctl restart network
   ```
