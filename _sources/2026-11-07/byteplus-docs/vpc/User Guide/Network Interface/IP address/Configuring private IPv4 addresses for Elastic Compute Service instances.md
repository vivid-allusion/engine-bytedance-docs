---
title: "Configuring private IPv4 addresses for Elastic Compute Service instances"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Configuring-private-IPv4-addresses-for-Elastic-Compute-Service-instances"
---

## Scenarios

After assigning a secondary private IPv4 address to the primary or secondary network interface of an ECS, the ECS image may not recognize the secondary private IPv4 address. You need to log in to the ECS instance and manually configure it.

## Prerequisites

* A secondary private IPv4 address is assigned to the primary or secondary Network Interface of the ECS instance. If not assigned, see [Assigning an IPv4 Address](https://docs.byteplus.com/en/docs/ecs/Assigning-or-releasing-a-private-IPv4-address).

* If a secondary private IPv4 address is assigned to the secondary Network Interface, you need to refer to [Configuring a secondary network interface for ECS](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances) to determine whether further configuration is required. If needed, complete the configuration accordingly.

* ECS images cannot recognize the private IPv4 address of the secondary Network Interface. You can log in to the ECS and run the command to view IP addresses to check the private IP address of the secondary network interface.

   > **tip**

   > The command to view the IP address is as follows:

   * > Linux: `Run ip address show`command.

   * > Windows: Run `ipconfig`command.

## Procedures

**Windows**

1. [Remote log in to ECS](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. View instance subnet mask and default gateway.

   1. On the Windows desktop, click **Start \> Windows PowerShell** to open Windows PowerShell.

   2. Run `ipconfig `command to view the subnet mask and default gateway.

3. On the Windows desktop, open the Network and Sharing Center.

4. Click **Change adapter settings** to open the Network Connections window.

5. Double\-click the network connection name, such as **Ethernet 3**, and in the pop\-up Network Connection status window, click **attribute**.

6. In the Properties dialog box, double\-click **Internet Protocol Version 4 (TCP/IPv4)** .

7. In the Internet Protocol Version 4 (TCP/IPv4) Properties dialog box, select **Use the following IP address**, and then click **Advanced**.

8. In the Advanced TCP/IP Settings dialog box, configure the IP addresses.

   1. In the IP address (R) field, click **Add**, and in the pop\-up window, input the assigned IP address and query the obtained subnet mask. You can add multiple IP addresses to the same Network Interface.

   2. In the gateway field, click **Add**. In the pop\-up window, type the default gateway using the query.

9. Click **Save** in each window sequentially to save the configurations.

10. In Windows PowerShell, run `ipconfig `command to view the updated IP configuration.

**CentOS**

**CentOS 7.x**

1. [Remote log in to ECS](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run `ip address `command to view the subnet mask of the ECS instance.

   The output indicates that the mask length follows the primary private IPv4 address of the Network Interface eth0. Convert the mask length to the subnet mask. If the mask length is `/24`, the corresponding subnet mask is `255.255.255.0`.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_81b3e0d409e0644f3ea242ab1a881a63.png)

3. Modify the network configuration file to configure the IPv4 address. This topic uses modifying network interface eth0 as an example for illustration.

   * Configure a single private IPv4 address

      1. Run `vim /etc/sysconfig/network-scripts/ifcfg-eth0:0` to open the network configuration file.

      2. Press i to enter edit mode and add the following content:

         ```Plain Text
         DEVICE=eth0:0        
         TYPE=Ethernet
         BOOTPROTO=static
         ONBOOT=yes
         IPADDR=<Assigned secondary private IPv4 address, e.g., 192.168.1.22> 
         NETMASK=<IPv4 subnet mask, e.g., 255.255.255.0>           
         ARPCHECK=no                   #Only add this configuration for CentOS 7 images. Skip if using other images.
         ```

      3. Press `Esc `to exit the edit mode, input `:wq `and press Enter.

   * If you need to add more private IPv4 addresses, simply increment the DEVICE sequence number and append the configuration.

      4. Run` vim /etc/sysconfig/network-scripts/ifcfg-eth0:1` to open the network configuration file.

      5. Press i to enter edit mode and add the following content:

         ```Plain Text
         DEVICE=eth0:1        
         TYPE=Ethernet
         BOOTPROTO=static
         ONBOOT=yes
         IPADDR=<Assigned secondary private IPv4 address, e.g., 192.168.1.33> 
         NETMASK=<IPv4 Subnet Mask, e.g., 255.255.255.0>       
         ARPCHECK=no                  #Only add this configuration for CentOS 7 images. Skip if using other images.
         ```

      6. Press `Esc `to exit the edit mode, input `:wq `and press Enter.

4. Run `service network restart `command to restart the network service.

5. Run `ip address show `command to view the configuration updates.

   As shown below, two secondary private IPv4 addresses have been successfully configured.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f3e2fd38d341c363e3846715866be99.png)

#### CentOS 8.x/Stream

1. [Remote log in to ECS](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run `ip address `command to view the subnet mask of the ECS instance.

   The output indicates that the mask length follows the primary private IPv4 address of the Network Interface eth1. Convert the mask length to the subnet mask. If the mask length is `/24`, the corresponding subnet mask is `255.255.255.0`.![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_028350ca87afe9407d7a8a3edf6de8fb.png)

3. Execute the following command to open the configuration file of the network interface eth1.

   ```Plain Text
   vi /etc/sysconfig/network-scripts/ifcfg-eth1 
   ```

4. Press`i` on the keyboard to enter edit mode, then add configuration information to the eth1 configuration file.

   After completing the configuration, press Esc, type :wq and press Enter to save the changes and exit.

   ```Plain Text
   DEVICE=eth1  # Newly mounted network interface
   BOOTPROTO=dhcp
   ONBOOT=yes
   TYPE=Ethernet
   USERCTL=yes
   PEERDNS=no
   IPV6INIT=no
   PERSISTENT_DHCLIENT=yes
   HWADDR=00:16:3e:63:19:**  # Modify this to the actual MAC address of the configured network adapter.
   DEFROUTE=no  # Indicates that the network interface is not the default route. Do not set eth1 as the default route to prevent the default route of the cloud server instance from being altered when bringing up the secondary NIC via ifup.
   ```

5. Modify the network configuration file to configure the IPv4 address.

   * Configure a single private IPv4 address

      1. Run `vim /etc/sysconfig/network-scripts/ifcfg-eth1:0 `to open the network configuration file.

      2. Press i` to enter edit mode and add the following content:`

         ```Plain Text
         DEVICE=eth1:0        
         TYPE=Ethernet
         BOOTPROTO=static
         ONBOOT=yes
         IPADDR=<Assigned secondary private IPv4 address, e.g., 172.16.1.22>   
         NETMASK=<IPv4 Subnet Mask, e.g., 255.255.255.0>     
         ```

      3. Press `Esc `to exit the edit mode, input `:wq `and press Enter.

   * If you need to add more private IPv4 addresses, simply increment the DEVICE sequence number and append the configuration.

      4. Run `vim /etc/sysconfig/network-scripts/ifcfg-eth1:1` command to open the network configuration file.

      5. Press i` to enter edit mode and add the following content:`

         ```Plain Text
         DEVICE=eth1:1        
         TYPE=Ethernet
         BOOTPROTO=static
         ONBOOT=yes
         IPADDR=<Assigned secondary private IPv4 address, e.g., 172.16.1.33>  
         NETMASK=<IPv4 Subnet Mask, e.g., 255.255.255.0>       
         ```

      6. Press `Esc `to exit the edit mode, input `:wq `and press Enter.

6. Run `reboot `command to restart the ECS instance.

7. Run `ip address show `command to view the configuration updates.

   As shown below, two secondary private IPv4 addresses have been successfully configured.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_46a7f572c7a6a797a59c6fe0acd58bbc.png)

**Ubuntu/Debian/veLinux**

1. [Remote log in to ECS](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the following command to view the instance subnet mask and default gateway.

   ```Plain Text
   ip address
   ip route 
   ```

   > If the default gateway information is not required in the network configuration, you may skip the step of querying the default gateway.

   The output indicates that the mask length follows the primary private IPv4 address of the Network Interface eth0. Convert the mask length to the subnet mask. If the mask length is `/24`, the corresponding subnet mask is `255.255.255.0`. The value after default for network interface eth0 represents the default gateway.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_def565dcd053dcccf1e5fc6936981e4b.png)

3. Select the method to configure the secondary private IP address based on the instance's operating system. This topic uses modifying network interface eth0 as an example for illustration.

   * Taking Ubuntu 18.04.6 LTS, Ubuntu 20.04.5 LTS, and Ubuntu 22.04.1 LTS as examples:

      1. Disable the cloud\-init network configuration. Run `vim /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg` command, press `i` to enter edit mode, then enter the following configuration. After finishing, press `Esc` to exit edit mode, then type `:wq` and press Enter.

         ```Plain Text
         network: {config: disabled}
         ```

      2. Modify network configuration. Run `vim /etc/netplan/50-cloud-init.yaml` command, press `i` to enter edit mode, then input the following configuration. After finishing, press `Esc` to exit edit mode, then type `:wq` and press Enter.

         Taking Ubuntu 18.04.6 LTS and Ubuntu 20.04.5 LTS as examples:

         ```Bash
         network:
             version: 2
             ethernets:
                 eth0:
                     dhcp4: false                    # set dhcp4 to false
                     match:
                         macaddress: 00:16:3e:5e:**:**
                     mtu: 0
                     set-name: eth0
                     addresses:
                       - <Primary private IPv4 address/prefix length, e.g. 192.168.1.11/24>         
                       - <Assigned secondary private IPv4 address 1/prefix length, e.g. 192.168.1.22/24> 
                       - <Assigned secondary private IPv4 address 2/prefix length, e.g. 192.168.1.33/24>  
                     gateway4: <Default gateway, e.g. 192.168.1.1>
                     nameservers:
                        addresses: [100.96.0.2,100.96.0.3] # 100.96.0.2, 100.96.0.3 are the default DNS servers; modify as needed.
         ```

         > In the above configuration, the <CIDR notation\> is converted from the subnet mask. For example, the subnet mask 255.255.255.0 corresponds to a CIDR notation of /24.

         Taking Ubuntu 22.04.1 LTS as an example:

         ```Bash
         network:
             version: 2
             ethernets:
                 eth0:
                     dhcp4: false                    # set dhcp4 to false
                     match:
                         macaddress: 00:16:3e:5e:**:**
                     mtu: 0
                     set-name: eth0
                     addresses:
                       - <Primary private IPv4 address/prefix length, e.g. 192.168.1.11/24>          
                       - <Assigned secondary private IPv4 address 1/prefix length, e.g. 192.168.1.22/24>  
                       - <Assigned secondary private IPv4 address 2/prefix length, e.g. 192.168.1.33/24>  
                     routes: 
                       - to: default
                         via:  <Default gateway, e.g. 192.168.1.1> 
                     nameservers:
                        addresses: [100.96.0.2,100.96.0.3] # 100.96.0.2, 100.96.0.3 are the default DNS servers; modify as needed.
         ```

         > In the above configuration, the <CIDR notation\> is converted from the subnet mask. For example, the subnet mask 255.255.255.0 corresponds to a CIDR notation of /24.

      3. Run `netplan apply `command to restart the network service and apply the configuration.

      4. Run `ip address show `command to view the configuration updates.

         As shown below, two secondary private IPv4 addresses have been successfully configured.

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2dbb55f2839642d9c98c43700cc60619.png)

   * Taking Ubuntu 16.04.7 LTS, Debian 9/10/11, and veLinux as examples

      1. Modify network configuration. Run the vim /etc/network/interfaces command, press i to enter the edit mode, and type the following configuration content, press Esc to exit edit mode after configuration is complete, then type :wq and press Enter.

         ```Plain Text
         auto eth0:0
         iface eth0:0 inet static
         address <Assigned secondary private IPv4 address 1, e.g. 192.168.1.22/24>
         netmask <IPv4 subnet mask, e.g. 255.255.255.0>              
         
         auto eth0:1
         iface eth0:1 inet static
         address <Assigned secondary private IPv4 address 2, e.g. 192.168.1.33/24> 
         netmask <IPv4 subnet mask, e.g. 255.255.255.0> 
         ```

      2. Run `reboot `command to restart the ECS instance.

      3. Run `ip address `command to view the configuration updates.

         As shown below, two secondary private IPv4 addresses have been successfully configured.

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b690bd576d5fa3cae93c345386f7b257.png)

**OpenSUSE**

1. [Remote log in to ECS](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run `ip address `command to view the subnet mask of the ECS instance.

   The echoed output is as follows. The value after the primary private IP address of network interface eth0 represents the CIDR notation, which needs to be converted to the corresponding subnet mask. If the mask length is /24, the corresponding subnet mask is 255.255.255.0.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e08472ef6d8cc3771cedffcc3f600e8c.png)

3. Modify the network configuration. This topic uses modifying network interface eth0 as an example.

   1. Run `vim /etc/sysconfig/network/ifcfg-eth0 `command to open the network configuration file.

   2. Pressito enter edit mode, then input the following content:

      ```Plain Text
      IPADDR_0=<Assigned secondary private IPv4 address 1>
      NETMASK_0=<IPv4 subnet mask>
      LABEL_0='0'
      
      IPADDR_1=<Assigned secondary private IPv4 address 2>
      NETMASK_1=<IPv4 subnet mask>
      LABEL_1='1'
      ```

   3. Press `Esc `to exit the edit mode, input `:wq `and press Enter.

4. Run `service network restart `command to restart the network service to apply the configuration.

5. Run `ip address show `command to view the configuration updates.

   As shown below, two secondary private IPv4 addresses have been successfully configured.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4a898cf5f0ac457532493a3c46bf3400.png)
