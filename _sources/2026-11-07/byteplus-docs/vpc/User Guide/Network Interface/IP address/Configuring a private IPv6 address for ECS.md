---
title: "Configuring a private IPv6 address for ECS"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Configuring-private-IPv6-addresses-for-ECS-instances"
---

<span id="bjgK36LT"></span>
## Scenarios

After assigning an IPv6 address to the primary or secondary network interface of an Elastic Compute Service (ECS), the system image may not recognize the IPv6 address. You will need to log in to the ECS instance and manually configure it.

<span id="kSRT0dmm"></span>
## Prerequisites


* The primary or secondary network interface of Elastic Compute Service (ECS) has been assigned an IPv6 address. If not assigned, see [Allocate IPv6 address](https://docs.byteplus.com/en/docs/ecs/Assigning-or-releasing-a-private-IPv6-address).

* If it is the IPv6 address of a secondary network interface, refer to [ECS configure secondary network interface](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances) to determine if configuration is needed. If required, complete the configuration.

* ECS images cannot recognize the private IPv6 address of the secondary Network Interface. You can log in to the ECS and run the command to view IP addresses to check the private IPv6 address of the secondary network interface.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The command to view the IP address is as follows:   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Linux: Run <code>ip address show</code> command.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Windows: Run <code>ipconfig</code> command.   </div>
   


<span id="IGEcPQZ9"></span>
## Procedures


<Tabs>
<Tab zoneid="kV1PO8w5wy" title="CenOS">
<TabTitle>CenOS</TabTitle>

Taking CentOS 7.9 as an example, the procedure is as follows:


1. [Remote log in to ECS](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the following command to open the network interface configuration file.​​

   ```Plain Text
   vi /etc/sysconfig/network-scripts/ifcfg-eth1
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">eth1 is the newly configured Network Interface.   </div>
   

3. Press`i` to enter edit mode. Confirm whether the file contains the following content. If not, input the following content:

   ```Plain Text
   DHCPV6C=yes
   IPV6INIT=yes
   ```
   

4. Press `Esc `to exit the edit mode, input `:wq `and press Enter.

5. Reboot the ECS instance.

6. Run `ip address show `command to view the configuration updates.

   As shown below, the IPv6 address of secondary network interface has been successfully identified.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_29ba73c2239ec6d242219de9398ddd80.png) </span>


</Tab>
<Tab zoneid="qRxZhb8iFN" title="Ubuntu">
<TabTitle>Ubuntu</TabTitle>

**Ubuntu 16.04**


1. [Remote log in to ECS](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the following command to open the network interface configuration file.​​

   ```Plain Text
   vi /etc/network/interfaces
   ```
   

3. Press`i` to enter edit mode. Confirm whether the file contains the following content. If not, input the following content:

   ```Plain Text
   iface eth1 inet6 dhcp
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">eth1 is the newly configured Network Interface.   </div>
   

4. Press `Esc `to exit the edit mode, input `:wq `and press Enter.

5. Run `reboot` command to restart the ECS instance.

6. Run `ip address show `command to view the configuration updates.

   As shown below, the IPv6 address of secondary network interface has been successfully identified.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07468351e442f00ade8ba953efa5baff.png) </span>


**Ubuntu 18.04**


1. Log in to the ECS remotely. For details, see[Logging into an instance.](https://docs.byteplus.com/en/docs/ecs/Overview-1)

2. Run the following command to open the network interface configuration file.​​

   ```Plain Text
   vim /etc/netplan/eth1-multic-hotlog.yaml
   ```
   

3. Press `i` to enter edit mode. Confirm whether there is the following content in the file. If not, input the following content:

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
   

4. Press `Esc `to exit the edit mode, input `:wq `and press Enter.

5. Run `netplan apply` command to reconfigure the network and make the configuration effective.

6. Run `systemctl restart systemd-networkd.service` command to restart the network service.

7. Run `ip address show `command to view the configuration updates.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6cc34ba97a5b3683191b89f997ce8e48.png) </span>


</Tab>
<Tab zoneid="MSkv6lsNk6" title="Debian/veLinux">
<TabTitle>Debian/veLinux</TabTitle>

1. [Remote log in to ECS](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the following command to open the network interface configuration file.​​

   ```Plain Text
   vi /etc/network/interfaces
   ```
   

3. Press`i` to enter edit mode. Confirm whether the file contains the following content. If not, enter the following content:

   ```Plain Text
   iface eth1 inet6 dhcp
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">eth1 is the newly configured Network Interface.   </div>
   

4. Press `Esc `to exit the edit mode, input `:wq `and press Enter.

5. Execute reboot to restart the ECS instance.

6. Run `ip address show `command to view the configuration updates.

   As shown below, the IPv6 address of secondary network interface has been successfully identified.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c26d2d30f6efc009e2d723aa04debe5a.png) </span>





</Tab>
<Tab zoneid="V5Bv3YSOII" title="Windows">
<TabTitle>Windows</TabTitle>

Taking Windows Server 2019 as an example, the steps are as follows:


1. [Remote log in to ECS](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Choose **Start \> Control Panel** to open the Control Panel page.

3. Click **Network and Internet**, then click **Network and Sharing Center** to open the Network & Sharing Center.

4. In the left\-side navigation pane, select **Change adapter settings** to open the network connection window.

5. Double\-click the network connection (e.g., Ethernet 2) as needed. A status window will pop up.

6. Click **attribute**. In the pop\-up property window, double\-click **Internet Protocol Version 6 (TCP/IPv6)** . The Internet Protocol Version 6 (TCP/IPv6) property window pops up.

7. Select **Use the following IPv6 address(es)** , then click **Advanced**. The Advanced TCP/IP Settings window pops up.

8. Click **Add. ** The TCP/IP Address window pops up. Input the IPv6 address and subnet prefix length 64 (i.e., the subnet mask length). Click ** Add** to complete the action.

9. (Optional) Repeat step 8 to add multiple IPv6 addresses.

10. Click **Save** one by one to save the configuration in each window.

11. Click **Start \> Windows PowerShell**, run `ipconfig` command to view the updated IP configuration.


</Tab>
</Tabs>


&nbsp;
