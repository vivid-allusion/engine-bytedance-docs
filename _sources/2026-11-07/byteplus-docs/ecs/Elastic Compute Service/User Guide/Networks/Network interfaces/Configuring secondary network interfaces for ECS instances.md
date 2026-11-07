---
title: "Configuring secondary network interfaces for ECS instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances"
---

<span id="zTKIcOPb"></span>
## Applicable scenarios

After you mount a secondary network interface to an ECS instance, except for the images listed below, other images may not automatically identify the primary private IP address of the secondary network interface or add the corresponding routes. As a result, the secondary network interface cannot work as expected. You need to configure the secondary network interface and routes for the ECS instance.


|**Operating system type** |**Version** |
|---|---|
|CentOS |CentOS 8.x, CentOS Stream |
|Fedora |Fedora 37 64 bit |
|Windows Server |All versions |


<span id="8635JXXX"></span>
### Prerequisites

This procedure is required only if the image used by the ECS instance does not identify the primary private IPv4 address of the secondary network interface. Otherwise, no operations are required.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Commands for viewing IP addresses:</div>



* <div data-tips="true" data-tips-type="default">Linux: Execute the <code>ip address show</code> command in the command line.</div>


* <div data-tips="true" data-tips-type="default">Windows: Execute the <code>ipconfig</code> command in the command line.</div>



<span id="nu79ddq3"></span>
## Configure secondary network interfaces

<span id="99P3WUok"></span>
### Tool\-based configuration

The BytePlus platform provides you with an automatic configuration tool for secondary network interfaces. Non\-lightweight bare metal instances based on the following image types can use the tool to configure secondary network interfaces with a few clicks.


|**Operating system type** |**Version** |
|---|---|
|CentOS |CentOS 7.1–7.9 64 bit |
|Ubuntu |* Ubuntu Server 22.04 LTS 64 bit<br><br>* Ubuntu Server 20.04 LTS 64 bit<br><br>* Ubuntu Server 18.04 LTS 64 bit<br><br>* Ubuntu Server 16.04 LTS 64 bit |


<span id="fRB8ybj4"></span>
#### Limits

After you configure a secondary network interface by using the automatic configuration tool, you can manage the secondary network interface only by using the default network management tool of the image.


|**Operating system type** |**Version** |**Default network management tool** |
|---|---|---|
|CentOS |* CentOS 7.1\-7.9 64 bit |* ifup ethx<br><br>* ifdown ethx |
|Ubuntu |* Ubuntu Server 16.04 LTS 64 bit<br><br>* Ubuntu Server 22.04 LTS 64 bit<br><br>* Ubuntu Server 20.04 LTS 64 bit<br><br>* Ubuntu Server 18.04 LTS 64 bit |* ifdown ethx<br><br>* ifconfig ethx up<br><br>* ifconfig ethx down |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you have edited the configuration file of the secondary network interface according to the <a href="https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances">manual configuration guidelines</a>, you need to delete the manually added configuration before you can use the automatic configuration tool for secondary network interfaces.</div>



<Tabs>
<Tab zoneid="B5IjlPAk" title="CentOS 7">
<TabTitle>CentOS 7</TabTitle>

For instances running CentOS 7.1 to 7.9, you can configure the secondary network interface by using the automatic configuration tool.


1. For CentOS 7 systems where the network service type is set to network\-scripts, you can execute the following commands to download and install the automatic configuration tool for secondary network interfaces.

   ```Plain Text
   wget http://mirrors.ivolces.com/extra-tools/centos/7/rpms/multi-nic-hotlog-for-centos7-v1.0.1-1.ve1.x86_64.rpm
   yum install ./multi-nic-hotlog-for-centos7-v1.0.1-1.ve1.x86_64.rpm
   ```
   

2. After you install the tool, execute the reboot command to restart the instance. After a restart, the tool automatically completes the secondary network interface configuration.

3. Execute the `ip address show` command to check whether the primary private IP address of the secondary network interface can be identified.

   As shown in the following figure, the primary private IP address of the secondary network interface eth1 is identified as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e8501d354ea8db0829c442312db815f8.png) </span>

4. Log in to the ECS instance to check whether the automatically generated routes for the secondary network interface meet your business requirements. If they do not meet your business requirements, you can [modify network interface routes](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances).


</Tab>
<Tab zoneid="vwsWOauD" title="Ubuntu">
<TabTitle>Ubuntu</TabTitle>

* Ubuntu 16

   1. For Ubuntu 16 systems where the network service type is set to interface, you can execute the following commands to download and install the automatic configuration tool for secondary network interfaces.

      ```Plain Text
      wget http://mirrors.ivolces.com/extra-tools/ubuntu/pool/main/m/multi-nic-hotlog-for-ubuntu-le-17/multi-nic-hotlog-for-ubuntu-le-17_1.0.1_amd64.deb
      dpkg -i multi-nic-hotlog-for-ubuntu-le-17_1.0.1_amd64.deb
      ```
      

   2. After you install the tool, execute the `reboot` command to restart the instance. After a restart, the tool automatically completes the secondary network interface configuration.

   3. Execute the `ip address show` command to check whether the primary private IP address of the secondary network interface can be identified.

      As shown in the following figure, the primary private IP address of the secondary network interface eth1 is identified as expected.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5c4a15643515fbb0eddc4389fef30c9.png) </span>

* Ubuntu18/20/22

   1. For Ubuntu 18/20/22 systems where the network service type is set to interface, you can execute the following commands to download and install the automatic configuration tool for secondary network interfaces.

      ```Plain Text
      wget http://mirrors.ivolces.com/extra-tools/ubuntu/pool/main/m/multi-nic-hotlog-for-ubuntu/multi-nic-hotlog-for-ubuntu_1.0.1_amd64.deb
      dpkg -i multi-nic-hotlog-for-ubuntu_1.0.1_amd64.deb
      ```
      

   2. After you install the tool, execute the `reboot` command to restart the instance. After a restart, the tool automatically completes the secondary network interface configuration.

   3. Execute the `ip address show` command to check whether the primary private IP address of the secondary network interface can be identified.

      As shown in the following figure, the primary private IP address of the secondary network interface eth1 is identified as expected.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ac545c760b8c7581ae45331dc3a3f898.png) </span>


</Tab>
</Tabs>


<span id="JU4HaKkG"></span>
### Manual configuration

If the images of your instance do not support the automatic configuration tool, you need to manually configure the secondary network interface.


<Tabs>
<Tab zoneid="ejgt8IxS" title="Debian/veLinux">
<TabTitle>Debian/veLinux</TabTitle>

Debian 9, Debian 10, Debian 11, and veLinux 1.0 system configuration


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to open the configuration file for the eth1 network interface.

   `vi /etc/network/interfaces`

3. Press `i` to enter the edit mode, and add configuration information to the configuration file for the eth1 network interface.

   After the configuration is complete, press `Esc` on the keyboard, input `:wq`, then press the Enter key to save the changes and exit.

   > `eth1` is the newly configured network interface.   
   

   ```Plain Text
   auto eth0
   iface eth0 inet dhcp
   
   auto eth1
   iface eth1 inet dhcp
   ```
   

4. Run the following command to view the network interface configuration file and confirm the changes.

   `cat /etc/network/interfaces`

5. Execute the following command to restart the network service.

   `systemctl restart networking`

6. You can execute the `ip address show` command to check whether the primary private IP address of the eth1 network interface is identified.

   As shown in the following figure, the primary private IP address of the eth1 secondary network interface is identified as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5c4a15643515fbb0eddc4389fef30c9.png) </span>


</Tab>
<Tab zoneid="duTSc9ug" title="OpenSUSE">
<TabTitle>OpenSUSE</TabTitle>

1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to open the configuration file for the eth1 network interface.

   `vi /etc/sysconfig/network/ifcfg-eth1`

3. Press `i` to enter the edit mode, and add configuration information to the configuration file for the eth1 network interface.

   After the configuration is complete, press `Esc` on the keyboard, input `:wq`, then press the Enter key to save the changes and exit.

   ```Plain Text
   BOOTPROTO='dhcp4'
   STARTMODE='auto'
   USERCONTROL='no'
   ```
   

4. Execute the following command to view the network interface configuration file and confirm the modification.

   `cat /etc/sysconfig/network/ifcfg-eth1`

5. Execute the following command to restart the network service.

   `systemctl restart network`

6. Execute the `ip address show` command to check whether the primary private IP address of the secondary network interface can be identified.

   As shown in the following figure, the primary private IP address of the eth1 secondary network interface is identified as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_adce0ce619c3434f50a1c3a4e95f0270.png) </span>


</Tab>
<Tab zoneid="zNPbCs5W" title="Ubuntu">
<TabTitle>Ubuntu</TabTitle>

Ubuntu 24.04 system configuration


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to create and open the configuration file for the eth1 secondary network interface.

   `vim /etc/netplan/eth1-netcfg.yaml`

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the preceding command, the eth1 secondary network interface is used as an example. Replace eth1 with the name of the actual secondary network interface.   </div>
   

   3. Press `i` to enter the edit mode, and add configuration information to the configuration file for the eth1 network interface.

   ```Plain Text
   network:
     version: 2
     ethernets:
       eth1:
        dhcp4: true
        dhcp4-overrides:
          route-metric: 200
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This configuration file is in <code>.yaml</code> format, and YAML syntax should be followed when editing.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In <code>.yaml</code> format, use spaces for indentation, and do not use the Tab key.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To avoid formatting issues, we recommend that you copy the default configuration file <code>/etc/netplan/99-netcfg.yaml</code> for modifications.   </div>
   

      4. After you complete the configuration, press the `Esc` key, enter `:wq`, and then press Enter to save the changes and exit the file.

5. Execute `netplan apply` command to make the configuration effective.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The instance is mounted with multiple secondary network interfaces. Refer to steps 2 to 5 to update the netplan configuration for each secondary network interface.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The value of the metric parameter for each secondary network interface must be unique, and must not be <code>100</code> (this is the value for the primary network interface).   </div>
   

   6. Execute the `systemctl restart systemd-networkd.service` command to restart the network.

7. Execute the `ip address show` command to check whether the primary private IP address of the secondary network interface can be identified.

   As shown in the following figure, the primary private IP address of the eth1 secondary network interface is identified as expected.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d1248646be9639f5b31061b470536c41.png) </span>


</Tab>
</Tabs>


<span id="0b7ExVuK"></span>
### Subsequent operation

After you configure a secondary network interface, the operating system automatically generates routes for the secondary network interface. You can log in to the ECS instance to check whether the automatically generated routes for the secondary network interface meet your business requirements. If they do not meet your business requirements, you can [modify network interface routes](https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Commands for viewing routes:</div>



* <div data-tips="true" data-tips-type="default">Linux: Execute the ip route command in the command line.</div>


* <div data-tips="true" data-tips-type="default">Windows: Execute the route printcommand in the command line.</div>



<span id="WeoBIl26"></span>
## Modify network interface routes

After you log in to the ECS instance, if you find that the current network interface routes do not meet your business requirements, you can refer to the following instructions to modify the network interface routes.

<span id="sjidbN60"></span>
### Modify routes in the command line

You can quickly modify routing information of an ECS instance in the command line.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Routes modified in a Linux instance by using this method become invalid after the instance restarts. To address this, you can <a href="https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances">create a script that automatically adds the required routes</a> when the instance starts.</div>



<Tabs>
<Tab zoneid="YS9pq92n" title="Modify network interface routes for a Linux instance">
<TabTitle>Modify network interface routes for a Linux instance</TabTitle>

For the existing ECS instance vm\-1, the primary private IP address of the primary network interface eth0 is `192.168.1.11`, and the primary private IP address of the newly associated secondary network interface eth1 is `192.168.2.2`.


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to check whether the current routes meet your business requirements.

   ```Plain Text
   route -n
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7d6bc341e5b69ff0ed190346291791f.png) </span>

   * If the current routes meet your business requirements, no further operations are required.

   * If the current routes do not meet your business requirements, add or remove route forwarding policies based on your business requirements by referring to Step 3.

3. You can execute the following command to view route\-related commands.

   ```Plain Text
   ip route help
   ```
   

   This topic describes commonly used commands for adding and removing static routes. Example:

   ```Plain Text
   ip -4 route <Policy> <Destination CIDR block> via <Gateway address> dev <Interface> metric <Priority>
   ```
   

   
   |**Parameter** |**Description** |
   |---|---|
   |<Policy\> |The command\-based action. Valid values:<br><br><br>* add: Add a route.<br><br>* del: Remove a route. |
   |<Destination CIDR block\> |Routes are matched according to the longest mask principle: the longer the subnet mask, the higher its priority for routing. |
   |<Gateway address\> |The gateway address of the specified network interface. |
   |<Interface\> |The specified network interface. |
   |<Priority\> |When the destination CIDR block is the same, a route with a smaller value of the metric parameter has a higher priority. |
   

4. For example, when the secondary network interface eth1 is associated with an EIP, the EIP of the secondary network interface must be used by default to access the Internet.

   Execute the following commands to add or remove route forwarding policies for eth1 and eth0.

   ```Plain Text
   ip -4 route add 0.0.0.0/0 via 192.168.2.1 dev eth1 metric 98
   ip -4 route add 0.0.0.0/0 via 192.168.1.1 dev eth0 metric 99
   ip -4 route del 0.0.0.0/0 via 192.168.1.1 dev eth0 metric 0
   ```
   


</Tab>
<Tab zoneid="vSZJX1VI" title="Modify network interface routes for a Windows instance">
<TabTitle>Modify network interface routes for a Windows instance</TabTitle>

For the existing ECS instance vm\-2, the primary private IP address of the primary network interface is 172.16.100.223, and the primary private IP address of the newly associated secondary network interface is 172.16.100.93.


1. Remotely connect to and log in to the ECS instance. For more information, see [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Open the Command Prompt window (cmd.exe) on the Windows instance.

3. Execute the following command to view the routing information of the current network interface.

   ```Plain Text
   route print
   ```
   

   * The following figure shows the private network routes. As shown in the following figure, when the instance accesses the 172.16.100.0/24 CIDR block or other destination CIDR blocks, equivalent routes exist to forward the traffic to the primary and secondary network interfaces. You can customize routes based on your business requirements and specify a route forwarding policy for traffic to a specific CIDR block.

   * The following figure shows the public network routes. As shown in the following figure, when network interfaces are enabled, two public network routes are generated by default. When you associate an EIP with a network interface based on your business requirements, you need to manually specify the route forwarding policy for Internet access. If multiple routing policies exist for the same public network destination address, Internet access may fail because traffic could be routed through a network interface not associated with an EIP.

4. Specify route forwarding policies.

   1. Execute the following command to check whether the current routes meet your business requirements. If the current routes do not meet your business requirements, refer to the following steps to add or remove route forwarding policies.

      ```Plain Text
      route print
      ```
      

   2. Add a route forwarding policy:

      1. In the ECS console, click the name of the instance, select the "Network Interface" tab, and click the name of the network interface. Then, you can view the Mac address of the network interface in the MAC Address field.

      2. Execute the following command to view the interface number of the network interface to be configured by using the MAC address.

         ```Plain Text
         route print
         ```
         

      3. Execute the following command to add a route.

         ```Plain Text
         route add 0.0.0.0 mask 0.0.0.0 172.16.100.1 metric 100 IF 9 -p
         ```
         

         * The add parameter is required and specifies the destination address.

         * The mask parameter is required and specifies the mask for the destination address.

         * The content following the mask is required and specifies the gateway address for the network interface.

         * The metric parameter is optional and specifies the number of route hops required to reach the destination address. The higher the value of the metric parameter, the lower the priority of the corresponding route.

         * The IF parameter is optional and specifies the network interface. If you do not configure the IF parameter, the best network interface is selected by default.

         * The \-p parameter is optional and specifies that the current route is permanent. If you configure the parameter, the modification is effective after the ECS instance restarts. If you do not configure the parameter, the modification automatically becomes invalid after the ECS instance restarts.

   3. Execute the following command to remove the route forwarding policy.

      ```Plain Text
      route delete 0.0.0.0 mask 0.0.0.0 172.16.100.1
      ```
      


</Tab>
</Tabs>


<span id="Luu51GiZ"></span>
### Modify routes by using a script

You can add a route configuration script for a Linux ECS instance to automatically configure routing information when the instance starts.


<Tabs>
<Tab zoneid="xRR0qEA6" title="CentOS/RHEL/Rocky Linux/AlmaLinux">
<TabTitle>CentOS/RHEL/Rocky Linux/AlmaLinux</TabTitle>

* CentOS 7.1

   1. Execute the following command to create the `/etc/sysconfig/network-scripts/route-<Interface>` file.

      ```Plain Text
      vim /etc/sysconfig/network-scripts/route-eth1
      ```
      

   2. Press the `i` key to enter the edit mode, and add the following content to configure routes.

      ```Plain Text
      0.0.0.0/0 via 192.168.2.1 dev eth1 metric 98
      ```
      

   3. Press the `Esc` key to exit the edit mode, enter `:wq`, and then press Enter to save the changes and exit the file.

   4. Similarly, configure the routes for eth0.

   5. Execute the following command to restart the ECS instance.

      ```Plain Text
      reboot
      ```
      

   6. Execute the following command to view the routes.

      ```Plain Text
      route -n
      ```
      

* Procedure for modifying the routes by using a script when CentOS Stream 9, RHEL 9, CentOS Stream 8, CentOS 8, RHEL 8, Rocky Linux, or AlmaLinux is used:

   1. Create a routing configuration script file.

      1. Execute the following command to create a script file named route_config.sh.

         ```Plain Text
         vim /root/route_config.sh
         ```
         

      2. Press the `i` key to enter the edit mode, and then copy and paste the following content into the file.

         ```Bash
         #!/bin/bash
         function add_ip_route() {
             local retries=0
             until /usr/sbin/ip -4 route add default via 192.168.***.**1 dev eth1 table 100; do
                 ((retries++))
                 if [ $retries -gt 10 ]; then
                     echo "Add IP route failed."
                     return 1
                 fi
                 sleep 3
              done
              return 0
         }
         
         function add_ip_rule() {
             local retries=0
             until /usr/sbin/ip -4 rule add from 192.168.***.4 lookup 100; do
                 ((retries++))
                 if [ $retries -gt 10 ]; then
                     echo "Add IP rule failed."
                     return 1
                 fi
                 sleep 3
              done
              return 0
         }
         
         add_ip_route
         if [ $? -ne 0 ]; then
             exit 1
         fi
         
         add_ip_rule
         if [ $? -ne 0 ]; then
             exit 1
         fi
         ```
         

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">This script is used to create a routing table for the secondary network interface and a corresponding routing policy associated with that table. Where:         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Secondary network interface name: <code>eth1</code>.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Gateway address: <code>192.168.***.**1</code>.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Primary IPv4 address of the secondary network interface: <code>192.168.***.4</code>.         </div>
         

               3. Press the Esc key to exit the edit mode, enter :wq, and then press Enter to save the changes and close the file.

   2. Execute the following command to add executable permission to the script file.

      ```Plain Text
      chmod +x route_config.sh
      ```
      

   3. Execute the following command to configure the default route.

      ```Plain Text
      sh /root/route_config.sh
      ```
      

   4. Configure automatic routing updates when the instance starts.

      1. Execute the following command to open the /etc/rc.local file.

         ```Plain Text
         vim /etc/rc.local
         ```
         

      2. Press the i key to enter the edit mode and add the following content.

         ```Plain Text
         sh /root/route_config.sh
         ```
         

      3. Press the `Esc` key to exit the edit mode, enter `:wq`, and then press Enter to save the changes and close the file.

      4. Execute the following command to add executable permission to the script file.

         ```Plain Text
         chmod +x /etc/rc.local
         ```
         

   5. Execute the following command to restart the ECS instance.

      ```Plain Text
      reboot
      ```
      

   6. Execute the following command to view the configured routes and IP rules.

      ```Plain Text
      ip route list table 100 && ip rule list
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>table 100</code> with the actual route table name configured in your script.      </div>
      


</Tab>
<Tab zoneid="JodxNdy6" title="Ubuntu">
<TabTitle>Ubuntu</TabTitle>

* Procedure when Ubuntu 16.04 LTS is used:

   1. Execute the following command to open the `/etc/network/interfaces.d/50-cloud-init.cfg` file and add a route for eth0.

      ```Plain Text
      vi /etc/network/interfaces.d/50-cloud-init.cfg
      ```
      

   2. Press the `i` key to enter the edit mode and add the following content.

      ```Plain Text
      up ip -4 route add 0.0.0.0/0 via 192.168.1.1 dev eth0 metric 99
      ```
      

   3. Press the `Esc` key to exit the edit mode, enter `:wq`, and then press Enter to save the changes and exit the file.

   4. Execute the following command to open the `/etc/network/interfaces.d/eth1-multic-hotlog` file and add a route for eth1.

      ```Plain Text
      vi /etc/network/interfaces.d/eth1-multic-hotlog
      ```
      

   5. Press the `i` key to enter the edit mode and add the following content.

      ```Plain Text
      up ip -4 route add 0.0.0.0/0 via 192.168.2.1 dev eth1 metric 98
      ```
      

   6. Press the `Esc` key to exit the edit mode, enter `:wq`, and then press Enter to save the changes and close the file.

   7. Execute the following command to restart the ECS instance and apply the configuration.

      ```Plain Text
      reboot
      ```
      

   8. Execute the following command to view the routes.

      ```Plain Text
      route -n
      ```
      

* Procedure when Ubuntu 18.04 LTS is used:

   1. Execute the following command to open the /etc/netplan/50\-cloud\-init.yaml file and a route for eth0.

      `vim /etc/netplan/50-cloud-init.yaml`

   2. Press the `i` key to enter the edit mode and add the following content.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e1c2061139c8095f11dabe297edcbbaa.png) </span>

   3. Press the `Esc` key to exit the edit mode, enter `:wq`, and then press Enter to save the changes and close the file.

   4. Execute the following command to open the /etc/netplan/eth1\-multic\-hotlog.yaml file and add a route for eth1.

      ```Plain Text
      vi /etc/netplan/eth1-multic-hotlog.yaml
      ```
      

   5. Press the i key to enter the edit mode and add the following content.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f735863999bc20d53336a81ef2f7b23d.png) </span>

   6. Press the Esc key to exit the edit mode, enter :wq, and then press Enter to save the changes and close the file.

   7. Execute the following command to restart the network service and apply the configuration.

      ```Plain Text
      netplan apply
      ```
      

   8. Execute the following command to view the routes.

      ```Plain Text
      route -n
      ```
      


</Tab>
<Tab zoneid="1WYbCyu7" title="veLinux/Debian">
<TabTitle>veLinux/Debian</TabTitle>

Procedure when veLinux 1.0 or Debian 9 is used:


1. Execute the following command to open the network interface configuration file and add routes for eth0 and eth1.

   ```Plain Text
   vi /etc/network/interfaces
   ```
   

2. Press the `i` key to enter the edit mode and add the following content.

   ```Plain Text
   up ip -4 route add 0.0.0.0/0 via 192.168.1.1 dev eth0 metric 99
   up ip -4 route add 0.0.0.0/0 via 192.168.2.1 dev eth1 metric 98
   ```
   

3. Press the `Esc` key to exit the edit mode, enter `:wq`, and then press Enter to save the changes and exit the file.

4. Execute the following command to restart the network and apply the configuration.

   ```Plain Text
   systemctl restart networking
   ```
   

5. Execute the following command to view the routes.

   ```Plain Text
   ip route
   ```
   


</Tab>
</Tabs>
