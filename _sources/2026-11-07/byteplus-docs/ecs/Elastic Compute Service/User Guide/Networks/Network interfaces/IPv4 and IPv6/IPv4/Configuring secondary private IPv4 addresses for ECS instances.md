---
title: "Configuring secondary private IPv4 addresses for ECS instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configuring-secondary-private-IPv4-addresses-for-ECS-instances"
---

<span id="unbcPRjz"></span>
## Applicable scenarios

After you assign a secondary private IPv4 address to the primary or secondary network interface of an ECS instance, the ECS image cannot identify the secondary private IPv4 address. You need to log in to the ECS instance and configure the secondary private IPv4 address manually.

<span id="pQNk9XPV"></span>
## Prerequisites


* A secondary private IPv4 address is assigned to the primary or secondary Network Interface of the ECS instance. Otherwise, assign a secondary private IPv4 address. For more information, see [Assigning IPv4 addresses](https://docs.byteplus.com/en/docs/ecs/Assigning-or-releasing-a-private-IPv4-address).

* If a secondary private IPv4 address has been assigned to the secondary network interface, refer to [Configuring secondary network interfaces for ECS instances](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances) to determine whether configuration is needed. If so, complete the configuration.

* ECS images cannot recognize the private IPv4 address of the secondary network interface. You can log in to the ECS instance and execute the command to view the private IP address of the secondary network interface.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Commands for viewing IP addresses:</div>



* <div data-tips="true" data-tips-type="default">Linux: Execute the ip address show command in the command line.</div>


* <div data-tips="true" data-tips-type="default">Windows: Execute the ipconfig command in the command line.</div>



<span id="gBX4wxCd"></span>
## Procedure


<Tabs>
<Tab zoneid="nQPOlznsOz" title="Windows">
<TabTitle>Windows</TabTitle>

1. Log in to the ECS instance. For more information, see [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. View the subnet mask and default gateway of the instance.

   1. On the Windows desktop, click "Start \> Windows PowerShell" to open the Windows PowerShell tool.

   2. Execute the `ipconfig` command to view the subnet mask and default gateway.

3. On the Windows desktop, open Network and Sharing Center.

4. Click "Change adapter settings" to open the Network Connections window.

5. Double\-click the network connection name, such as **Ethernet 3**. In the pop\-up network connection status window, click "Properties".

6. In the properties dialog box, double\-click "Internet Protocol Version 4 (TCP/IPv4)".

7. In the Internet Protocol Version 4 (TCP/IPv4) Properties dialog box, select "Use the following IP address", and then click "Advanced".

8. In the Advanced TCP/IP Settings dialog box, configure the IP address.

   1. In the IP addresses field, click "Add". In the pop\-up window, enter the assigned IP address and the subnet mask retrieved from the query. You can add multiple IP addresses to the same network interface.

   2. In the Default gateways field, click "Add". In the pop\-up window, enter the default gateway obtained from the query.

9. Click "OK" in each window to save the configuration.

10. In Windows PowerShell, execute the ipconfig command to view the updated IP configuration.


</Tab>
<Tab zoneid="m7FJnosf1Y" title="CentOS">
<TabTitle>CentOS</TabTitle>

<span id="sKmCffBx"></span>
#### CentOS 7.x


1. Log in to the ECS instance. For more information, see [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the `ip address` command to view the subnet mask of the ECS instance.

   As shown in the following figure, the number following the primary private IP address of the eth0 network interface indicates the prefix length, which needs to be converted to the corresponding subnet mask. For example, if the prefix length is 24, the subnet mask is 255.255.255.0.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81b3e0d409e0644f3ea242ab1a881a63.png) </span>

3. Modify the network configuration file and configure the IPv4 address. In the example provided in this section, the network configuration file of the eth0 network interface is modified.

   * Configure a single private IPv4 address

      1. Execute the `vim /etc/sysconfig/network-scripts/ifcfg-eth0:0` command to open the network configuration file.

      2. Press the `i` key to enter the edit mode and enter the following content:

         ```Plain Text
         DEVICE=eth0:0
         TYPE=Ethernet
         BOOTPROTO=static
         ONBOOT=yes
         IPADDR=<Assigned secondary private IPv4 address. Example: 192.168.1.22>
         NETMASK=<IPv4 subnet mask. Example: 255.255.255.0>
         ARPCHECK=no                   # This configuration is required only for CentOS 7 images. If you use other images, ignore this configuration.
         ```
         

      3. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   * To add more private IPv4 addresses, increment the DEVICE number and configure private IPv4 addresses accordingly.

      4. Execute the `vim /etc/sysconfig/network-scripts/ifcfg-eth0:1` command to open the network configuration file.

      5. Press the `i` key to enter the edit mode and enter the following content:

         ```Plain Text
         DEVICE=eth0:1
         TYPE=Ethernet
         BOOTPROTO=static
         ONBOOT=yes
         IPADDR=<Assigned secondary private IPv4 address. Example: 192.168.1.33>
         NETMASK=<IPv4 subnet mask. Example: 255.255.255.0>
         ARPCHECK=no                  # This configuration is required for CentOS 7 images. If you use other images, ignore this configuration.
         ```
         

      6. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

4. Execute the serv`ice network res`tart command to restart the network service.

5. Execute the `ip address show` command to view the configuration updates.

   As shown in the following figure, two secondary private IPv4 addresses have been configured.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f3e2fd38d341c363e3846715866be99.png) </span>


<span id="vMGVEshq"></span>
#### CentOS 8.x/Stream


1. Log in to the ECS instance. For more information, see [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the `ip address` command to view the subnet mask of the ECS instance.

   As shown in the following figure, the number following the primary private IP address of the eth1 network interface indicates the prefix length, which needs to be converted to the corresponding subnet mask. For example, if the prefix length is 24, the subnet mask is 255.255.255.0.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_028350ca87afe9407d7a8a3edf6de8fb.png) </span>

3. Execute the following command to open the configuration file for the eth1 network interface.

   ```Plain Text
   vi /etc/sysconfig/network-scripts/ifcfg-eth1
   ```
   

4. Press `i` to enter the edit mode, and add configuration information to the configuration file for the eth1 network interface.

   After you complete the configuration, press the `Esc` key, enter `:wq`, and then press Enter to save the changes and exit the file.

   ```Plain Text
   DEVICE=eth1  # Newly mounted network interface.
   BOOTPROTO=dhcp
   ONBOOT=yes
   TYPE=Ethernet
   USERCTL=yes
   PEERDNS=no
   IPV6INIT=no
   PERSISTENT_DHCLIENT=yes
   HWADDR=00:16:3e:63:19:**  # Replace the value with the actual MAC address of the configured network interface.
   DEFROUTE=no  # Specify that the network interface is not the default route. Do not specify eth1 as the default route to ensure that the default route of the ECS instance remains unchanged when the secondary network interface is started by executing the ifup command.
   ```
   

5. Modify the network configuration file and configure the IPv4 address.

   * Configure a single private IPv4 address

      1. Execute the `vim /etc/sysconfig/network-scripts/ifcfg-eth1:0` command to open the network configuration file.

      2. Press the `i` key to enter the edit mode and enter the following content:

         ```Plain Text
         DEVICE=eth1:0
         TYPE=Ethernet
         BOOTPROTO=static
         ONBOOT=yes
         IPADDR=<Assigned secondary private IPv4 address. Example: 172.16.1.22>
         NETMASK=<IPv4 subnet mask. Example: 255.255.255.0>
         ```
         

      3. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

   * To add more private IPv4 addresses, increment the DEVICE number and configure private IPv4 addresses accordingly.

      4. Execute the `vim /etc/sysconfig/network-scripts/ifcfg-eth1:1` command to open the network configuration file.

      5. Press the `i` key to enter the edit mode and enter the following content:

         ```Plain Text
         DEVICE=eth1:1
         TYPE=Ethernet
         BOOTPROTO=static
         ONBOOT=yes
         IPADDR=<Assigned secondary private IPv4 address. Example: 172.16.1.33>
         NETMASK=<IPv4 subnet mask. Example: 255.255.255.0>
         ```
         

      6. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

6. Execute the `reboot` command to restart the ECS instance.

7. Execute the `ip address show` command to view the configuration updates.

   As shown in the following figure, two secondary private IPv4 addresses have been configured.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a34e688058c0a71f43d7eaeac9a757a.png) </span>


</Tab>
<Tab zoneid="YFafcGxsRh" title="Ubuntu/Debian/veLinux">
<TabTitle>Ubuntu/Debian/veLinux</TabTitle>

1. Log in to the ECS instance. For more information, see [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to view the subnet mask and default gateway of the instance.

   ```Plain Text
   ip address
   ip route
   ```
   

   > If default gateway information is not required in the network configuration, you can skip the default gateway query step.   
   

   As shown in the following figure, the number following the primary private IP address of the eth0 network interface indicates the prefix length, which needs to be converted to the corresponding subnet mask. For example, if the prefix length is `24`, the subnet mask is `255.255.255.0`. The IP address following "default" is the default gateway address for the eth0 network interface.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_def565dcd053dcccf1e5fc6936981e4b.png) </span>

3. Select the method for configuring a secondary private IP address based on the instance operating system. In the example provided in this section, a secondary private IP address is configured for the eth0 network interface.

   * Ubuntu 18.04.6 LTS, Ubuntu 20.04.5 LTS, and Ubuntu 22.04.1 LTS are used as examples:

      1. Disable Cloud\-init network configuration. Execute the `vim /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg` command, press i to enter the edit mode, enter the following configuration content, press `Esc` to exit the edit mode, and then enter `:wq` and press Enter.

         ```Plain Text
         network: {config: disabled}
         ```
         

      2. Modify the network configuration. Execute the `vim /etc/netplan/50-cloud-init.yaml` command, press i to enter the edit mode, enter the following configuration content, press `Esc` to exit the edit mode, and then enter `:wq` and press Enter.

         Ubuntu 18.04.6 LTS and Ubuntu 20.04.5 LTS are used as examples:

         ```Plain Text
         network:
             version: 2
             ethernets:
                 eth0:
                     dhcp4: false                        # Set dhcp4 to false.
                     match:
                         macaddress: 00:16:3e:5e:**:**
                     mtu: 0
                     set-name: eth0
                     addresses:
         - <Primary private IPv4 address/prefix length. Example: 192.168.1.11/24>
         - <Assigned secondary private IPv4 address 1/prefix length. Example: 192.168.1.22/24>
         - <Assigned secondary private IPv4 address 2/prefix length. Example: 192.168.1.33/24>
         gateway4: <Default gateway. Example: 192.168.1.1>
                     nameservers:
                        addresses: [100.96.0.2,100.96.0.3] #100.96.0.2 and 100.96.0.3 are the IP addresses of the default DNS servers. You can modify the IP addresses based on your business requirements.
         ```
         

         > In the above configuration, the `<prefix length>` is converted from the subnet mask. For example, the mask bits for the subnet mask 255.255.255.0 is 24.         
         

         Ubuntu 22.04.1 LTS is used as an example:

         ```Plain Text
         network:
             version: 2
             ethernets:
                 eth0:
                     dhcp4: false                        # Set dhcp4 to false.
                     match:
                         macaddress: 00:16:3e:5e:**:**
                     mtu: 0
                     set-name: eth0
                     addresses:
         - <Primary private IPv4 address/prefix length. Example: 192.168.1.11/24>
         - <Assigned secondary private IPv4 address 1/prefix length. Example: 192.168.1.22/24>
         - <Assigned secondary private IPv4 address 2/prefix length. Example: 192.168.1.33/24>
                     routes:
                       - to: default
         via:  <Default gateway. Example: 192.168.1.1>
                     nameservers:
         addresses: [100.96.0.2,100.96.0.3] # 100.96.0.2 and 100.96.0.3 are the IP addresses of the default DNS servers. You can modify the IP addresses based on your business requirements.
         ```
         

         > In the above configuration, the <prefix length\> is converted from the subnet mask. For example, the mask bits for the subnet mask 255.255.255.0 is 24.         
         

      3. Execute the netplan apply command to restart the network service for the configuration to take effect.

      4. Execute the ip address show command to view the configuration updates.

         As shown in the following figure, two secondary private IPv4 addresses have been configured.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2dbb55f2839642d9c98c43700cc60619.png) </span>

   * Ubuntu 16.04.7 LTS, Debian 9/10/11, and veLinux are used as examples:

      5. Modify the network configuration. Execute the `vim /etc/network/interfaces` command, press `i` to enter the edit mode, enter the following configuration content, press `Esc` to exit the edit mode, and then enter `:wq` and press Enter.

         ```Plain Text
         auto eth0:0
         iface eth0:0 inet static
         address <Assigned secondary private IPv4 address 1. Example: 192.168.1.22/24>
         netmask <IPv4 mask. Example: 255.255.255.0>
         
         auto eth0:1
         iface eth0:1 inet static
         address <Assigned secondary private IPv4 address 2. Example: 192.168.1.33/24>
         netmask <IPv4 mask. Example: 255.255.255.0>
         ```
         

      6. Execute the `reboot` command to restart the ECS instance.

      7. Execute the `ip address` command to view the configuration updates.

         As shown in the following figure, two secondary private IPv4 addresses have been configured.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b690bd576d5fa3cae93c345386f7b257.png) </span>


</Tab>
<Tab zoneid="UOdNrf9DnL" title="OpenSUSE">
<TabTitle>OpenSUSE</TabTitle>

1. Log in to the ECS instance. For more information, see [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the `ip address` command to view the subnet mask of the ECS instance.

   As shown in the following figure, the number following the primary private IP address of the eth0 network interface indicates the prefix length, which needs to be converted to the corresponding subnet mask. For example, if the prefix length is `24`, the subnet mask is `255.255.255.0`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e08472ef6d8cc3771cedffcc3f600e8c.png) </span>

3. Modify the network configuration. In the example provided in this section, the network configuration of the eht0 network interface is modified.

   1. Execute the `vim /etc/sysconfig/network/ifcfg-eth0` command to open the network configuration file.

   2. Press the i key to enter the edit mode and enter the following content:

      ```Plain Text
      IPADDR_0=<Assigned secondary private IPv4 address 1>
      NETMASK_0=<IPv4 subnet mask>
      LABEL_0='0'
      
      IPADDR_1=<Assigned secondary private IPv4 address 2>
      NETMASK_1=<IPv4 subnet mask>
      LABEL_1='1'
      ```
      

   3. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

4. Execute the `service network restart` command to restart the network service to apply the configuration.

5. Execute the `ip address show` command to view the configuration updates.

   As shown in the following figure, two secondary private IPv4 addresses have been configured.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4a898cf5f0ac457532493a3c46bf3400.png) </span>


</Tab>
</Tabs>
