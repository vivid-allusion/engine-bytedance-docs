---
title: "Enabling DHCP service in Linux image"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Start-SHCP-Service-in-Linux-image"
---

This topic describes how to enable the DHCP service on the Linux operating system.

<span id=".5YWz5LqOREhDUA=="></span>
## About DHCP

Dynamic Host Configuration Protocol (DHCP) is a network protocol used to automatically assign IP addresses, subnet masks, default gateways, and other network configuration information to network devices.

When a device connects to a network, it sends a request to a DHCP server to obtain the IP address and other configuration information. The DHCP server then assigns an appropriate IP address and other configuration information to the device based on its configured policies and available IP address pool.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

If your ECS instance or locally stored image uses a static IP address, you must enable DHCP in the image before creating a custom image from the ECS instance or by importing the image. Otherwise, the custom image created may fail to obtain a dynamic IP address.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Enable the DHCP service.

   * CentOS Stream 8/9, CentOS 6.x/7.x/8.x, Fedora 33/34/35, Rocky Linux, and AlmaLinux

      1. Execute the following command in the instance to view the network interface alias.

         ```Plain Text
         ifconfig
         ```
         

         Sample output

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_723086f8866138bed0fba1a0054838a5.png) </span>

      2. Execute the following command in the instance to open the network configuration file.

         > Replace `eth0` in the command with the name of the actual network interface. In the example provided in this topic, `eth0` is used.         
         

         ```Plain Text
         vim /etc/sysconfig/network-scripts/ifcfg-eth0 
         ```
         

      3. Press `i` to enter edit mode, and change the value of the `BOOTPROTO` parameter to `dhcp`.

         > Replace `eth0` with the name of the actual network interface. In the example provided in this topic, `eth0` is used.         
         

         ```Plain Text
         BOOTPROTO=dhcp
         ```
         

      4. Press the `Esc` key, enter `:wq`, and press Enter to save and exit the file.

      5. Execute the following command to restart the network service.

         * CentOS 8.x and Fedora 33/34/35

            ```Plain Text
            nmcli c reload
            nmcli d connect eth0
            ```
            

         * CentOS 7.x, CentOS Stream 8/9, Rocky Linux, and AlmaLinux

            ```Plain Text
            systemctl restart network
            ```
            

         * CentOS 6.x

            ```Plain Text
            service network restart
            ```
            

   * Ubuntu 16 and Debian 9/10/11

      1. Execute the following command in the instance to view the network interface alias.

         ```Plain Text
         ip addr
         ```
         

         Sample output

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dde9de9ad920d0c19bd092f55f867867.png) </span>

      2. Execute the following command to open the network configuration file.

         ```Plain Text
         vim /etc/network/interfaces
         ```
         

         Sample output

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8c12668b633b3eeb0c1847d4935ba837.png) </span>

      3. Press `i` to enter edit mode, and modify the target network interface configuration to the following content.

         > In the example provided in this topic, `eth0` is used. Replace `eth0` in the command with the name of the actual network interface.         
         

         ```Plain Text
         auto eth0
         iface eth0 inet dhcp 
         ```
         

         Example after modification

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_27e951f8fb21991e6f9bf41cca476f33.png) </span>

      4. Press the `Esc` key, enter `:wq`, and press Enter to save and exit the file.

      5. Execute the following command to restart the network service.

         ```Plain Text
         systemctl restart networking
         ```
         

   * Ubuntu 18/20/22

      1. Execute the following command in the instance to view the network interface alias.

         ```Plain Text
         ifconfig
         ```
         

         Sample output

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_723086f8866138bed0fba1a0054838a5.png) </span>

      2. Execute the following command to open the network configuration file.

         > Replace `01-netcfg.yaml` in the command with the actual configuration file.         
         

         ```Plain Text
         vim  /etc/netplan/01-netcfg.yaml
         ```
         

         Sample output

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_be7b273c8ff498721051919e4d6f19ab.png) </span>

      3. Press `i` to enter edit mode, and modify the following configuration items.

         > In the example provided in this topic, the `eth0` network interface is used. Modify the configuration of your actual network interface.         
         

         ```Plain Text
         eth0:
           dhcp4: yes
           dhcp6: no
         ```
         

         Example after modification

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_63ef97cc197168f2d0e84506afa9b76f.png) </span>

      4. Press the `Esc` key, enter `:wq`, and press Enter to save and exit the file.

      5. Execute the following command to restart the network service.

         ```Plain Text
         netplan apply
         systemctl restart systemd-networkd
         ```
         

   * OpenSUSE 15.4

      1. Execute the following command in the instance to view the network interface alias.

         ```Plain Text
         ip addr
         ```
         

         Sample output

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe007eb0cab5ff93c941528d836997a0.png) </span>

      2. Execute the following command to open the network configuration file.

         > Replace `eth0` in the command with the actual name of the network interface.         
         

         ```Plain Text
         vim /etc/sysconfig/network/ifcfg-eth0
         ```
         

         Sample output

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0a81249911ad475292aa385a3df4f181.png) </span>

      3. Press the `i` key to enter edit mode, and modify the values of the `BOOTPROTO` and `STARTMODE` parameters.

         ```Plain Text
         BOOTPROTO='dhcp'
         STARTMODE='auto'
         ```
         

         Example after modification

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e0369d03bc949c1daabbd899c871c324.png) </span>

      4. Press the `Esc` key, enter `:wq`, and press Enter to save and exit the file.

      5. Execute the following command to restart the network service.

         ```Plain Text
         systemctl restart wicked
         ```
         

3. At this point, you have enabled the DHCP service in the Linux image. Then, you can [create a custom image (Linux) from the instance](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance) or [import the custom image](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1).
