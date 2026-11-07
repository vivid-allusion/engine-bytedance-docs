---
title: "Configuring a secondary network interface for ECS"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Configuring-a-network-interface-and-a-private-address"
---

## Scenarios

After attaching a secondary network interface to an Elastic Compute Service (ECS), most system images may not automatically recognize the primary private IP address of the secondary network interface or add the corresponding routes, which will result in the secondary network interface being unusable. The following images are exceptions to this behavior. Therefore, you must manually configure the secondary network interface and its routes on the ECS.

|Operating System Types |Version |
|---|---|
|CentOS |CentOS 8.x, CentOS Stream |
|Fedora |Fedora 37 64\-bit |
|Windows Server |All versions |

## Prerequisites

The ECS image does not recognize the primary private IPv4 address of the secondary network interface. If detected, no action is required.

> **tip**

> The command to view the IP address is as follows:

* > Linux: Run `ip address show` in the command line.

* > Windows: Run `ipconfig` in the command line.

## Configure secondary network interface

### Configure using tools

BytePlus provides you with an automatic configuration tool for secondary network interfaces (ENIs). ECSs with the following images can use this tool for one\-click configuration of secondary ENIs.

|Operating System Types |Version |
|---|---|
|CentOS |CentOS 7.1 to 7.9 64\-bit |
|Ubuntu |* Ubuntu Server 22.04 LTS 64\-bit<br><br>* Ubuntu Server 20.04 LTS 64\-bit<br><br>* Ubuntu Server 18.04 LTS 64\-bit<br><br>* Ubuntu Server 16.04 LTS 64\-bit |

After configuring the secondary network interface using the automatic configuration tool, only the default network management tool provided by the image distribution is supported for operating the secondary network interface.

|Operating System Types |Version |Default Network Management Tool |
|---|---|---|
|CentOS |* CentOS 7.1 to 7.9 64\-bit |* ifup ethx<br><br>* ifdown ethx |
|Ubuntu |* Ubuntu Server 16.04 LTS 64\-bit<br><br>* Ubuntu Server 22.04 LTS 64\-bit<br><br>* Ubuntu Server 20.04 LTS 64\-bit<br><br>* Ubuntu Server 18.04 LTS 64\-bit |* ifdown ethx<br><br>* ifconfig ethx up<br><br>* ifconfig ethx down |

> **tip**

> If the secondary network interface configuration files are based on Manual configuration, you must remove these custom configurations before using the automatic secondary network interface configuration tool.

**CentOS 7**

**CenOS 7**

For instance running CentOS 7.1 to 7.9, you can use the automatic tool to configure secondary network interfaces.

1. For CentOS 7 systems with the network service type set to network\-scripts, execute the following command to download and install the automatic secondary network interface configuration tool.

   ```Plain Text
   wget http://mirrors.ivolces.com/extra-tools/centos/7/rpms/multi-nic-hotlog-for-centos7-v1.0.1-1.ve1.x86_64.rpm
   yum install ./multi-nic-hotlog-for-centos7-v1.0.1-1.ve1.x86_64.rpm
   ```

2. After installing the tool, run the `reboot` command to restart the instance. The tool will automatically complete the secondary network interface configuration upon reboot.

3. Run `ip address show` to check whether the primary private IP address of the secondary ENI is correctly recognized.

   As shown in the figure below, the primary private IP address of the secondary network interface (eth1) is correctly recognized.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e8501d354ea8db0829c442312db815f8.png)

4. You should log in to the ECS to verify whether the automatically generated routes meet your requirements. If they do not, see **Modifying a network interface route**.

**Ubuntu**

* Ubuntu 16

   1. For Ubuntu 16 systems with the network service type set to interface, you can execute the following command to download and install the automatic secondary network interface configuration tool.

      ```Plain Text
       wget http://mirrors.ivolces.com/extra-tools/ubuntu/pool/main/m/multi-nic-hotlog-for-ubuntu-le-17/multi-nic-hotlog-for-ubuntu-le-17_1.0.1_amd64.deb
      dpkg -i multi-nic-hotlog-for-ubuntu-le-17_1.0.1_amd64.deb
      ```

   2. After installing the tool, run the `reboot` command to restart the instance. The tool will automatically complete the secondary network interface configuration upon reboot.

   3. Run `ip address show` to check whether the primary private IP address of the secondary ENI is correctly recognized.

      As shown in the figure below, the primary private IP address of the secondary network interface (eth1) is correctly recognized.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5c4a15643515fbb0eddc4389fef30c9.png)

* Ubuntu18/20/22

   1. For Ubuntu 18/20/22 systems with the network service type set to interface, you can execute the following command to download and install the automatic secondary network interface configuration tool.

      ```JSON
      wget http://mirrors.ivolces.com/extra-tools/ubuntu/pool/main/m/multi-nic-hotlog-for-ubuntu/multi-nic-hotlog-for-ubuntu_1.0.1_amd64.deb
      dpkg -i multi-nic-hotlog-for-ubuntu_1.0.1_amd64.deb
      ```

   2. After installing the tool, run the `reboot` command to restart the instance. The tool will automatically complete the secondary network interface configuration upon reboot.

   3. Run `ip address show` to check whether the primary private IP address of the secondary ENI is correctly recognized.

      As shown in the figure below, the primary private IP address of the secondary network interface (eth1) is correctly recognized.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ac545c760b8c7581ae45331dc3a3f898.png)

### Manual configuration

For images that cannot be configured by the automatic tool, you must configure them manually.

**Debian/veLinux**

System Configuration for Debian 9, Debian 10, Debian 11, and veLinux 1.0

1. Remotely connect to and log in to the ECS. For specific operations, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to open the configuration file of the network interface eth1.

   ```JSON
   vi /etc/network/interfaces
   ```

3. Type `i` to enter edit mode, then add configuration information to the ENI eth1 configuration file.

   After completing the configuration, press Esc, type `:wq` and press Enter to save the changes and exit.

   > `eth1` is the newly configured Network Interface.

   ```Plain Text
   auto eth0
   iface eth0 inet dhcp
   
   auto eth1  
   iface eth1 inet dhcp
   ```

5. Run the following command to view the network interface configuration file and confirm the changes.

   ```JSON
   cat /etc/network/interfaces
   ```

6. Run the following command to restart the network service.

   ```JSON
   systemctl restart networking
   ```

7. You can execute the command `ip address show` to check whether the primary private IP address of the network interface eth1 has been recognized.

   As shown in the figure below, the primary private IP address of the secondary network interface (eth1) is correctly recognized.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d5c4a15643515fbb0eddc4389fef30c9.png)

**OpenSUSE**

1. Remotely connect to and log in to the ECS. For specific operations, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to open the configuration file of the network interface eth1.

   ```JSON
   vi /etc/sysconfig/network/ifcfg-eth1
   ```

3. Type `i` to enter edit mode, then add configuration information to ENI eth1 configuration file.

   After completing the configuration, press `Esc`, type `:wq`and press Enter to save the changes and exit.

   ```Plain Text
   BOOTPROTO='dhcp4'
   STARTMODE='auto'
   USERCONTROL='no'
   ```

4. Run the following command to view the network interface configuration file and confirm the changes.

   ```JSON
   cat /etc/sysconfig/network/ifcfg-eth1
   ```

5. Run the following command to restart the network service.

   ```JSON
   systemctl restart network
   ```

6. Run `ip address show` to check whether the primary private IP address of the secondary ENI is correctly recognized.

   As shown in the figure below, the primary private IP address of the secondary network interface (eth1) is correctly recognized.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_adce0ce619c3434f50a1c3a4e95f0270.png)

**Ubuntu**

Ubuntu 24.04 System Configuration

1. Remotely connect to and log in to the ECS. For specific operations, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to create and edit the configuration file for the secondary network interface eth1.

   Using secondary network interface eth1 as an example. Replace eth1 with the actual name of your secondary network interface.

   ```JSON
   vim /etc/netplan/eth1-netcfg.yaml
   ```

3. Press `i` to enter edit mode, then add the configuration information to the configuration file for ENI eth1.

   ```Plain Text
   network:
     version: 2
     ethernets:
       eth1:
        dhcp4: true
        dhcp4-overrides:
          route-metric: 200
   ```

   * This configuration file is in `.yaml` format and must adhere to YAML syntax when editing.

   * `In .yaml` format, use spaces for indentation and do not use tabs.

   * To avoid formatting issues, it is recommended to directly copy and modify the default configuration file `/etc/netplan/99-netcfg.yaml`.

4. After configuration, `press `Esc, type `:wq`, and press Enter to save and exit.

5. Run `netplan apply` to apply the configuration.

   If the instance has multiple secondary network interfaces attached, please repeat steps 2\-5 to update the Netplan configuration for each secondary network interface.

   The `metric` parameter value must be unique for each secondary network interface and cannot be `100` (this value is reserved for the primary network interface).

6. Run `systemctl restart systemd-networkd.service` to restart the network.

7. Run `ip address show` to check whether the primary private IP address of the secondary ENI is correctly recognized.

   As shown in the figure below, the primary private IP address of the secondary network interface (eth1) is correctly recognized.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d1248646be9639f5b31061b470536c41.png)

### What to do next

After configuring the secondary network interface, the operating system automatically generates routes for it. You should log in to the ECS to verify whether the automatically generated routes meet your requirements. If they do not, see **Modifying a network interface route**.

> **tip**

> The command to view routes is as follows:

* > Linux: Run `ip route` command.

* > Windows: Run `route print` command.

## Modify network interface route

If, after logging into the ECS instance, you find that the current routes of the network interface do not meet your requirements, you can refer to the instructions below to modify them.

### Modify routes via command line

You can quickly modify the route information of an ECS instance using the command line.

> **tip**

> Routes modified this way on Linux instances will not persist after reboot. To configure routes that are automatically added at startup, see the **Modifying Routes via Script** section below.

**Modify network interface route on Linux instance**

For the existing ECS vm\-1, the primary private IP address of the primary Network Interface (eth0) is `192.168.1.11`, and the primary private IP address of the newly bound secondary Network Interface (eth1) is `192.168.2.2`.

1. Remotely connect to and log in to the ECS. For specific operations, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to check whether the current routes meet your requirements.

   ```Plain Text
   route -n
   ```

   Example Output:

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7d6bc341e5b69ff0ed190346291791f.png)

   * If they meet the requirements, no further action is needed.

   * If they do not meet the requirements, proceed to step 3 to add or delete route forwarding policies based on your actual needs.

3. You can execute the following command to explore routing\-related commands.

   ```Plain Text
   ip route help
   ```

   This topic introduces commonly used commands for adding/deleting static routes, as follows:

   ```Plain Text
   ip -4 route <Policy> <Destination CIDR Block> via <Gateway Address> dev <Network Interface> metric <Priority>
   ```

   |**Parameter name** |**Notes** |
   |---|---|
   |Policy |Command operation. Values:<br><br><br>* add: Indicates adding a route.<br><br>* del: Indicates deleting a route. |
   |Destination CIDR |Routes are matched based on the Longest Prefix Match (LPM) rule, where a longer subnet mask indicates a higher priority. |
   |Gateway address |Specify the gateway address for the network interface. |
   |Network Interface |Specify Network Interface. |
   |Priority |When the target network segment is the same, a lower metric value indicates a higher priority for that route. |

4. For example, if the secondary network interface eth1 is bound to an EIP and needs to be used by default for Internet access, you can configure the routing accordingly.

   Execute the following commands sequentially to add or delete route forwarding policies for eth1 and eth0.

   ```Plain Text
   ip -4 route add 0.0.0.0/0 via 192.168.2.1 dev eth1 metric 98
   ip -4 route add 0.0.0.0/0 via 192.168.1.1 dev eth0 metric 99
   ip -4 route del 0.0.0.0/0 via 192.168.1.1 dev eth0 metric 0
              
   ```

**Modify network interface route on Windows instance**

For the existing ECS vm\-2, the primary private IP address of the primary ENI is `192.168.3.239`, and the primary private IP address of the newly bound secondary ENI is `192.168.3.240`.

1. Remotely connect to and log in to the ECS. For specific operations, see [Logging in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Open the cmd.exe command prompt window on the Windows instance.

3. Execute the following command to view the current network interface routing information.

   ```Plain Text
   route print
   ```

   * As shown below, equivalent routes exist for both the primary and secondary ENIs when the instance attempts to access the destination network segment `192.168.3.0/24` (or others). You can customize the routes based on your business requirements to specify the routing policy for accessing particular destination address ranges.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9395578244e783bbb10bdc69916671a.png)

   * As shown below, two default public routes exist after the network interface is enabled. When you bind an EIP to a network interface for your business needs, you must manually specify the routing policy for Internet access. If multiple routes with the same public destination address exist simultaneously, Internet access may fail due to traffic being routed through an incorrect network interface.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_781adc7d06023670a44382487fdc5d6f.png)

4. Specify the route forwarding policy.

   1. Execute the following command to verify if the current routes meet your requirements. If they do not, you can refer to the steps below to add or delete route forwarding policies.

      ```Plain Text
      route print
      ```

   2. Add routing forwarding policy:

      1. Click **ECS instance \> Device Management** tab to view the MAC addresses of the network interfaces.

      2. Execute the following command to identify the interface index of the target network interface by its MAC address:

         ```Plain Text
         route print
         ```

         Example Output:

         ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d83744efd70d9d420323bf3cd57d5cbc.png)

      3. Execute the following command to add a route.

         ```Plain Text
         route add 0.0.0.0 mask 0.0.0.0 192.168.3.1 metric 100 IF 12 -p
         ```

         * Destination Address​​: Specifies the destination address. Required.

         * Subnet Mask: ​​Specifies the subnet mask for the destination address. Required.

         * Gateway Address​​: Specifies the gateway address for the network interface. Required.

         * Metric​​: Specifies the route metric (hop count), indicating the number of hops required to reach the destination address. Optional. A higher metric value indicates a lower priority for that route.

         * IF: Specifies the network interface. Optional. If not specified, the system will default to the optimal Network Interface.

         * \-p​​: Configures a persistent route. Optional. If configured, the modification remains effective after the ECS reboots. If not configured, the modification is automatically discarded after the ECS reboots.

   3. Run the following command to delete the route forwarding policy.

      ```Plain Text
      route delete 0.0.0.0 mask 0.0.0.0 192.168.3.1
      ```

### Modify routes via script

**CentOS/RHEL/Rocky Linux/AlmaLinux**

* CentOS 7.1

   1. Execute the following command to create a new file `/etc/sysconfig/network-scripts/route-<network_interface>`.

      ```Plain Text
      vim /etc/sysconfig/network-scripts/route-eth1
      ```

   2. Press `i` to enter edit mode and add the following content to configure the route.

      ```Plain Text
      0.0.0.0/0 via 192.168.2.1 dev eth1 metric 98
      ```

   3. Press `esc` to exit edit mode, type `:wq`, then press Enter to save and exit.

   4. Repeat the previous steps to configure routes for eth0.

   5. Execute the following command to restart the ECS.

      ```Plain Text
      reboot
      ```

   6. Execute the following command to view the route.

      ```Plain Text
      route -n
      ```

* Taking CentOS Stream 9/RHEL 9/CentOS Stream 8/CentOS 8/RHEL 8/Rocky Linux/AlmaLinux as examples, the procedure is as follows:

   1. Create a routing configuration script.

      1. Execute the following command to create a new script `file route_config.sh`.

         ```Plain Text
         vim /root/route_config.sh
         ```

      2. Press `i` to enter edit mode, then copy and paste the following content into the file.

         ```Bash
         #!/bin/bash
         function add_ip_route() {
             local retries=0
             until /usr/sbin/ip -4 route add default via 192.168.XX.1 dev eth1 table 100; do
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
             until /usr/sbin/ip -4 rule add from 192.168.XX.4 lookup 100; do
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

         > **tip**

         > This script is used to create a route table for the secondary network interface, and add a route policy associated with that routing table. Parameters:

         * > Secondary network interface name: eth1.

         * > Gateway address: 192.168.XX.1.

         * > Secondary network interface primary IPv4 address: 192.168.XX.4.

      3. Press `esc` to exit edit mode, type `:wq`, then press Enter to save and exit.

   2. Execute the following command to grant execution permission to the script file.

      ```Plain Text
      chmod +x route_config.sh
      ```

   3. Execute the following command to configure the default route.

      ```Plain Text
      sh /root/route_config.sh
      ```

   4. Configure automatic route updates on system boot.

      1. Execute the following command to open the `/etc/rc.local` file.

         ```Plain Text
         vim /etc/rc.local
         ```

      2. Press `i` to enter edit mode and add the following content.

         ```Plain Text
         sh /root/route_config.sh
         ```

      3. Press `esc` to exit edit mode, type `:wq`, then press Enter to save and exit.

      4. Execute the following command to grant execution permission to the script file.

         ```Plain Text
         chmod +x /etc/rc.local
         ```

   5. Execute the following command to restart the ECS.

      ```Plain Text
      reboot
      ```

   6. Execute the following command to view the configured routes and IP rules.

      ```Plain Text
      ip route list table 100 && ip rule list
      ```

   > **tip**

   > Replace table 100 with the actual route table name configured in your script.

**Ubuntu**

* Using Ubuntu 16.04 LTS as an example, the procedure is as follows:

   1. Run the following command to open `/etc/network/interfaces.d/50-cloud-init.cfg` to add a route for eth0.

      ```Plain Text
      vi /etc/network/interfaces.d/50-cloud-init.cfg
      ```

   2. Press `i` to enter edit mode and add the following content:

      ```Plain Text
      up ip -4 route add 0.0.0.0/0 via 192.168.1.1 dev eth0 metric 99
      ```

   3. Press `esc` to exit edit mode, type `:wq`, then press Enter to save and exit.

   4. Run the following command to open `/etc/network/interfaces.d/eth1-multic-hotlog` to add a route for eth1.

      ```Plain Text
      vi /etc/network/interfaces.d/eth1-multic-hotlog
      ```

   5. Press `i` to enter edit mode and add the following content:

      ```Plain Text
      up ip -4 route add 0.0.0.0/0 via 192.168.2.1 dev eth1 metric 98
      ```

   6. Press `esc` to exit edit mode, type `:wq`, then press Enter to save and exit.

   7. Execute the following command to restart the ECS and apply the configuration.

      ```Plain Text
      reboot
      ```

   8. Execute the following command to view the route.

      ```Plain Text
      route -n
      ```

* Using Ubuntu 18.04 LTS as an example, the procedure is as follows:

   1. Execute the following command to open `/etc/netplan/50-cloud-init.yaml` to add a route for eth0.

      ```Plain Text
      vim /etc/netplan/50-cloud-init.yaml
      ```

   2. Press `i` to enter edit mode and add the content shown below:

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e1c2061139c8095f11dabe297edcbbaa.png)

   3. Press `esc` to exit edit mode, type `:wq`, then press Enter to save and exit.

   4. Execute the following command to open `/etc/netplan/eth1-multic-hotlog.yaml` to add a route for eth1.

      ```Plain Text
      vi /etc/netplan/eth1-multic-hotlog.yaml
      ```

   5. Press `i` to enter edit mode and add the content shown below.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f735863999bc20d53336a81ef2f7b23d.png)

   6. Press `esc` to exit edit mode, type `:wq`, then press Enter to save and exit.

   7. Run the following command to restart the network service and apply the configuration.

      ```Plain Text
      netplan apply
      ```

   8. Execute the following command to view the route.

      ```Plain Text
      route -n
      ```

**veLinux/Debian**

Taking veLinux 1.0 and Debian 9 as examples, the procedure is as follows:

1. Execute the following command to open the network configuration file and add routes for eth0 and eth1.

   ```Plain Text
   vi /etc/network/interfaces
   ```

2. Press `i` to enter edit mode and add the content shown below.

   ```Plain Text
   up ip -4 route add 0.0.0.0/0 via 192.168.1.1 dev eth0 metric 99
   up ip -4 route add 0.0.0.0/0 via 192.168.2.1 dev eth1 metric 98
   ```

3. Press `esc` to exit edit mode, type `:wq`, then press Enter to save and exit.

4. Execute the following command to restart the network and apply the configuration.

   ```Plain Text
   systemctl restart networking
   ```

5. Execute the following command to view the route.

   ```Plain Text
   ip route
   ```
