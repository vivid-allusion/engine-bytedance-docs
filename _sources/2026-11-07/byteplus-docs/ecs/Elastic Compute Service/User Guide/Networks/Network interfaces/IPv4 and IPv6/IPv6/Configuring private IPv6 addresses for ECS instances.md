---
title: "Configuring private IPv6 addresses for ECS instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configuring-private-IPv6-addresses-for-ECS-instances"
---

<span id="iPquUoPG"></span>
## Applicable scenarios

After you assign an IPv6 address to the primary or secondary network interface of an ECS instance, the ECS image may not be able to identify the IPv6 address. You need to log in to the ECS instance and configure the IPv6 address manually.

<span id="jqhOJYDK"></span>
## Prerequisites


* You have assigned IPv6 addresses to primary or secondary network interfaces associated with the ECS instance. Otherwise, assign an IPv6 address first. For more information, refer to [Assigning IPv6 addresses](https://docs.byteplus.com/en/docs/ecs/Assigning-or-releasing-a-private-IPv6-address).

* To assign IPv6 addresses to secondary network interfaces, refer to [Configuring secondary network interfaces for ECS instances](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances) to determine whether further configuration is required. If so, complete the configuration.

* If ECS images cannot recognize the secondary private IPv6 address,  log in to the ECS instance and execute the command for viewing IP addresses for the private IPv6 address of the secondary network interface.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Commands for viewing IP addresses:</div>



* <div data-tips="true" data-tips-type="default">Linux: Execute the ip address show command in the command line.</div>


* <div data-tips="true" data-tips-type="default">Windows: Execute the ipconfig command in the command line.</div>



<span id="pN0KWFhf"></span>
## Procedure


<Tabs>
<Tab zoneid="ofwVPHn46P" title="CentOS">
<TabTitle>CentOS</TabTitle>

Steps for CentOS 7.9:


1. Log in to an ECS instance via remote connection. For more information, refer to [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to open the configuration file for the network interface.

   ```Plain Text
   vi /etc/sysconfig/network-scripts/ifcfg-eth1
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">eth1 is the newly configured network interface.   </div>
   

   3. Press the i to enter edit mode. Confirm whether the file contains the following content. If not, input the following content:

   ```Plain Text
   DHCPV6C=yes
   IPV6INIT=yes
   ```
   

4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

5. Execute `reboot` command to restart the ECS instance.

6. Execute `ip address show` command to view the configuration updates.

   As shown in the following figure, the IPv6 address of the secondary network interface is identified.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9d2157a968732951accf51faa64011d.png) </span>


</Tab>
<Tab zoneid="vZdqB9CPTB" title="Ubuntu">
<TabTitle>Ubuntu</TabTitle>

<span id="oPamsupu"></span>
#### Ubuntu 16.04


1. Log in to an ECS instance via remote connection. For more information, refer to [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to open the configuration file for the network interface.

   ```Plain Text
   vi /etc/network/interfaces
   ```
   

3. Press the `i` to enter edit mode. Confirm whether the file contains the following content. If not, input the following content:

   ```Plain Text
   iface eth1 inet6 dhcp
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">eth1 is the newly configured network interface.   </div>
   

   4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

5. Execute `reboot` command to restart the ECS instance.

6. Execute `ip address show` command to view the configuration updates.

   As shown in the following figure, the IPv6 address of the secondary network interface is identified.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07468351e442f00ade8ba953efa5baff.png) </span>


<span id="cGJWcCTx"></span>
#### Ubuntu 18.04


1. Log in to an ECS instance via remote connection. For more information, refer to [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to open the configuration file for the network interface.

   ```Plain Text
   vim /etc/netplan/eth1-multic-hotlog.yaml
   ```
   

3. Press the `i` to enter edit mode. Confirm whether the file contains the following content. If not, input the following content:

   ```Plain Text
   network:
       ethernets:
           eth1:
               match:
                   macaddress: 00:16:3e:79:XX:XX
               set-name: eth1
               dhcp4: true
               dhcp6: true
               dhcp4-overrides:
                   route-metric: 200
               dhcp6-overrides:
                   route-metric: 200
   
       version: 2
   ```
   

4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

5. Execute `netplan apply` command to reconfigure the network and make the configuration effective.

6. Execute `systemctl restart systemd-networkd.service` command to restart the network service.

7. Execute `ip address show` command to view the configuration updates.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6cc34ba97a5b3683191b89f997ce8e48.png) </span>


</Tab>
<Tab zoneid="yGr37my5qB" title="Debian/veLinux">
<TabTitle>Debian/veLinux</TabTitle>

1. Log in to an ECS instance via remote connection. For more information, refer to [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to open the configuration file for the network interface.

   ```Plain Text
   vi /etc/network/interfaces
   ```
   

3. Press the `i` to enter edit mode. Confirm whether the file contains the following content. If not, input the following content:

   ```Plain Text
   iface eth1 inet6 dhcp
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">eth1 is the newly configured network interface.   </div>
   

   4. Press `Esc` to exit the edit mode, input `:wq` and press Enter.

5. Execute `reboot` command to restart the ECS instance.

6. Execute `ip address show` command to view the configuration updates.

   As shown in the following figure, the IPv6 address of the secondary network interface is identified.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c26d2d30f6efc009e2d723aa04debe5a.png) </span>


</Tab>
<Tab zoneid="h237U6WKEU" title="Windows">
<TabTitle>Windows</TabTitle>

Steps for Windows Server 2019:​


1. Log in to an ECS instance via remote connection. For more information, refer to [Logging in to instances](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Click "Start \> Control Panel" to enter the Control Panel page.

3. Click "Network and Internet" and the "Network and Sharing Center" to open Network and Sharing Center.

4. In the left\-side navigation pane, select "Change adapter settings" to open the network connections window.

5. Double\-click the network connection as needed, such as Ethernet 2. Then, the status window pops up.

6. Click "Properties" button, and then double\-click the "Internet Protocol Version 6(TCP/IPv6)" button to open the property configuration window.

7. Select "Use the following IPv6 address", and then click the "Advanced" button to open the advanced TCP/IP settings window.

8. Click "Add" button to open the TCP/IP address window, input the IPv6 address and subnet prefix length64 (that is, the subnet mask length), and then click "Add" button to complete the operation.

9. (Optional) Repeat step 8 to add multiple IPv6 addresses.


10. Click the "OK" button in each window to save the configuration.

11. Click "Start \> Windows PowerShell" and execute the ipconfig command to view the updated IP configuration.


As shown in the following figure, two IPv6 addresses have been configured.


</Tab>
</Tabs>
