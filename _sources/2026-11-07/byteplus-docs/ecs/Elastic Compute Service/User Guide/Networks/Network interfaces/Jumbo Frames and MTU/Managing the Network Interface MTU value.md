---
title: "Managing the Network Interface MTU value"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Modify-the-MTU-of-the-Network-Interface"
---

<span id="EhlGuaaA"></span>
## Introduction​

MTU (Maximum Transmission Unit) refers to the maximum amount of data that a single data link layer frame can carry in network communication.

<span id="oYZhZxPp"></span>
### Action notes

The default MTU value of BytePlus Network Interface is 1500 bytes.

When the default MTU value of the network interface cannot meet requirements (such as [traffic mirror](https://docs.byteplus.com/en/docs/vpc/Traffic-mirror-overview#.5L2_55So6ZmQ5Yi2)), you need to manually modify the network interface's MTU value.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Unless necessary, do not modify the MTU value. This is because modifying the ENI MTU value may cause data to be fragmented or dropped.</div>


<span id="LUNzxcze"></span>
### Procedures


<Tabs>
<Tab zoneid="znYCArNA" title="CenOS">
<TabTitle>CenOS</TabTitle>

Taking CentOS 7.9 as an example, the procedure is as follows:


1. Log in to the ECS remotely. For details, see [Logging into an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the `ifconfig `command to view the ENI MTU value. The output should be similar to the following figure:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_141c98809012fee4365b088eed25f8f3.png) </span>

3. Execute the following command to set the MTU value for Network Interface eth0.

   ```Plain Text
   mtu=<MTU value>
   echo "${mtu}" > /sys/class/net/eth0/mtu
   echo "echo \""${mtu}"\" > /sys/class/net/eth0/mtu">> /etc/rc.d/rc.local && chmod +x /etc/rc.d/rc.local
   ```
   

   Example configuration in this topic:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7ac3a1600d4a2d48289f6cef5ba13c31.png) </span>

4. Execute `ifconfig` command to check if it takes effect. The output should be similar to the following figure:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_912b4079d8fcd5b8ba1c783129155d9d.png) </span> 


</Tab>
<Tab zoneid="TPQeoxdX" title="Ubuntu">
<TabTitle>Ubuntu</TabTitle>

Taking Ubuntu Server 16.04 LTS and Ubuntu Server 18.04 LTS as examples, the procedure is as follows:


1. Log in to the ECS remotely. For details, see [Logging into an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute `ifconfig` to check the Network Interface MTU value. The output should be similar to the following figure:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f62cb0ba36de9e68194cb20091490a33.png) </span>

3. Setting the MTU value on different Ubuntu versions.

   * **Ubuntu Server 16.04 LTS**

      1. Execute the following command to create a script file.

         `vim /etc/network/if-up.d/setmtu`

      2. Press `i `to enter edit mode, then enter the following content to set the MTU value.

         ```Bash
         #!/bin/sh
         ifconfig <Network Interface Name> mtu <MTU value>
         ```
         


                  The figure demonstrates:


```Bash
#!/bin/sh
ifconfig eth0 mtu 1000
```


      3. Press `esc` key to exit edit mode, then press `:wq` to save changes and exit.

      4. Run the following command to grant execute permission to the `setmtu` file.

         `chmod +x /etc/network/if-up.d/setmtu`

      5. Run the `reboot` command to restart the ECS.

      6. Execute `ifconfig` command to check if it takes effect. The output should be similar to the following figure:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4ac9c66ea2ef5d604bfa345e484a3efe.png) </span>

   * **Ubuntu Server 18.04 LTS**

      1. Run the `vim /etc/netplan/50-cloud-init.yaml `command, press `i` to enter edit mode, and enter the following configuration:

         ```YAML
         network:
           version: 2
           ethernets:
             eth0:            # The example in this document is eth0
               dhcp4: true
               match:
                 macaddress: 00:16:3e:5e:**:**
               mtu: 1000      # The example in this document is 1000
               set-name: eth0
         ```
         

      2. Press `esc` key to exit edit mode, then press `:wq` to save changes and exit.

      3. Run `netplan apply `command to restart the network service and apply the configuration.

      4. Execute `ifconfig` to check the Network Interface MTU value. The output should be similar to the following figure:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c8e17b6195a9138b393b5d6654e6d813.png) </span> 


</Tab>
<Tab zoneid="SRfbxbdZ" title="Windows">
<TabTitle>Windows</TabTitle>

Taking Windows Server 2016 as an example, the steps are as follows:


1. Log in to the ECS remotely. For details, see [Logging into an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. On the Windows desktop, click Start \> Windows PowerShell to open Windows PowerShell.

3. Run the following command to view the Network Interface name.

   ```Plain Text
   netsh interface ipv4 show subinterfaces
   ```
   

   The output is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ed756b2382ae6d0374421836abaf6aaa.png) </span>

4. Run the following command to modify the Network Interface MTU value.

   ```Plain Text
   netsh interface ipv4 set subinterface "Network Interface Name" mtu=1399 store=persistent
   ```
   

   The example is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_151d046a82ebf61eeac7b43cb6f5815e.png) </span>

5. Execute the following command to check whether it takes effect.

   ```Plain Text
   netsh interface ipv4 show subinterfaces
   ```
   

   The output is as follows:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d4a7ad73da45ca7fa38cd2d381c9a43d.png) </span>


</Tab>
</Tabs>



&nbsp;

&nbsp;
