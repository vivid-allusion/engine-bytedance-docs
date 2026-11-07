---
title: "Modifying arp_announce and arp_ignore parameters in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Adjusting_arp_announce_and_arp_ignore_parameters_in_the_Linux_operating_system"
---

By modifying the `arp_announce` and `arp_ignore` parameters, you can control the kernel policies for sending and responding to ARP requests, optimize network communication, and reduce the likelihood of encountering ARP spoofing.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Except in specific complex network scenarios, especially those where ARP anomalies are caused by multiple network interfaces in the same CIDR block, you do not need to configure the <code>arp_announce</code> and <code>arp_ignore</code> parameters.</div>


<span id=".5pyv6K-t6Kej6YeK"></span>
## Terms

<span id=".5YWz5LqOQVJQ"></span>
### About ARP

Address Resolution Protocol (ARP) is a protocol used to resolve a network\-layer (IP layer) IP address to a data link layer physical (MAC) address. In a TCP/IP network, every device has a unique IP address to identify its location on the network, while a MAC address is used to identify the network interface of a device. The ARP protocol enables computers to determine the MAC address of the destination device prior to sending data. When sending an IP packet, if a computer does not know the MAC address corresponding to the IP address of the destination device, it will obtain it by broadcasting an ARP request packet.

<span id=".5YWz5LqOYXJwX2Fubm91bmNl5Y-C5pWw"></span>
### About the arp_announce parameter

The `arp_announce` parameter is a network parameter in Linux systems, primarily used to control the policy for selecting the source IP address of an ARP request packet. Valid values:


* `0`: The kernel uses any available local IP address as the source IP address of the ARP request packet.

* `1`: The kernel tries to avoid using an IP address that is not in the subnet of the network interface sending the request packet as the source IP address of the ARP request packet. If no suitable IP address is available, the ARP request packet is sent according to the rule specified by `arp_announce=2`.

* `2`: The kernel prefers a local IP address in the same subnet as the destination IP address as the source IP address of the ARP request packet. If no suitable IP address is available, the kernel uses an IP address from another network interface capable of receiving ARP responses.


<span id=".5YWz5LqOYXJwX2lnbm9yZeWPguaVsA=="></span>
### About the arp_ignore parameter

The `arp_ignore` parameter is a network parameter in Linux systems, primarily used to control the policy for how a network interface responds to an ARP request with a destination IP address matching the local IP address. Valid values:


* `0`: When the destination IP address is the IP address configured on any network interface of the local machine, the network interface responds to the ARP request.

* `1`: When the destination IP address is the IP address of the network interface, the network interface can respond to the ARP request.

* `2`: When the destination IP address is the IP address of the network interface and both the source and destination IP addresses of the ARP request are in the same subnet, the network interface can respond to the ARP request.

* `3`: If the local IP address corresponding to the destination IP address has a host scope, the network interface does not respond to the ARP request. If the scope is global or link, the network interface responds to the ARP request.

* `4` \-`7`: Parameter values reserved by the system and not in use.

* `8`: The network interface does not respond to any ARP requests.


<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario


* **Prevent ARP spoofing**

   When you set the `arp_announce` parameter to `0`, the source IP address in the sent ARP packet is used as the source IP address of the IP data packet. Attackers can forge ARP packets to claim they are the intended device for the ARP request or response, causing ARP spoofing and resulting in a man\-in\-the\-middle attack. In this case, you can modify the `arp_announce` parameter to ensure that the source of ARP requests sent by the server is clear and not easily exploited by attackers. At the same time, you can also modify the value of the `arp_ignore` parameter to restrict how the server responds to ARP requests, thereby reducing the likelihood of successful ARP spoofing.

* **Use the parameters in LVS\-DR mode**

   Linux Virtual Server \- Direct Routing (LVS \- DR) mode is an IP layer\-based load balancing technology. In this mode, each physical server node associates the virtual service IP address with its loopback network interface.

   * When a network interface sends an ARP request, if the source IP address in the ARP request packet is not the IP address of the network interface itself, other nodes that receive this request may record incorrect IP address and MAC address mappings in their ARP tables. This can lead to unexpected network issues and poses security risks. In such cases, you need to set the `arp_announce` parameter of the server to `2`.

   * When ARP requests for the virtual service IP address are broadcast to each real server node, if the real servers respond to these requests arbitrarily, it may cause network traffic confusion. This could further result in traffic being routed to a single node continuously, rendering the load balancing capability ineffective. In such cases, you need to set the `arp_ignore` parameter of the server to `1`.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

The `arp_announce` and `arp_ignore` parameters can be configured either globally (for all interfaces) or on a per\-network interface basis.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The actual effective value for each network interface is the maximum of the global (all) configuration and the configuration specific to that interface. For example: The global <code>arp_announce</code> parameter is set to <code>1</code>, and the <code>arp_announce</code> parameter for the <code>eth0</code> network interface is set to <code>2</code>. In such cases, the actual effective value of the <code>arp_announce</code> parameter on the <code>eth0</code> network interface is <code>2</code>.</div>


<span id=".6YWN572u5YWo5bGA5Y-C5pWw"></span>
### Configure global parameters

Global parameters configured using this method apply the same ARP policy to all network interfaces, facilitating batch management.


<Tabs>
<Tab zoneid="qvtGNjqDVe" title="Configuration by using the proc interface">
<TabTitle>Configuration by using the proc interface</TabTitle>

You can use this method to temporarily modify the parameter values while the operating system is running. Each time the instance restarts, you need to configure the parameters again.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the values of the global `arp_announce` and `arp_ignore` parameters.

   ```Plain Text
   cat /proc/sys/net/ipv4/conf/all/arp_announce
   cat /proc/sys/net/ipv4/conf/all/arp_ignore
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_da95e36101e0bbb935714f3e4a0c9d21.png) </span>

3. Execute the following command to configure the values of the global `arp_announce` and `arp_ignore` parameters.

   ```Plain Text
   echo 2 > /proc/sys/net/ipv4/conf/all/arp_announce
   echo 1 > /proc/sys/net/ipv4/conf/all/arp_ignore
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>1</code> and <code>2</code> with the actual values required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjusting_arp_announce_and_arp_ignore_parameters_in_the_Linux_operating_system#.5YWz5LqOYXJwX2Fubm91bmNl5Y-C5pWw">About the arp_announce parameter</a> and <a href="https://docs.byteplus.com/en/docs/ecs/Adjusting_arp_announce_and_arp_ignore_parameters_in_the_Linux_operating_system#.5YWz5LqOYXJwX2lnbm9yZeWPguaVsA==">About the arp_ignore parameter</a>.   </div>
   


</Tab>
<Tab zoneid="Hy2QKHCgbD" title="Configuration by using the arp.conf file">
<TabTitle>Configuration by using the arp.conf file</TabTitle>

You can use this method to permanently modify the parameter values while the operating system is running. You do not need to configure the parameters again after the instance restarts.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the values of the global `arp_announce` and `arp_ignore` parameters.

   ```Plain Text
   sysctl net.ipv4.conf.all.arp_announce
   sysctl net.ipv4.conf.all.arp_ignore
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb2ac0ec150843e85c1aee3f86468b40.png) </span>

3. Modify the values of the `arp_announce` and `arp_ignore`  parameters.

   1. Execute the following command to create the arp.conf file.

      ```Plain Text
      vim /etc/sysctl.d/arp.conf
      ```
      

   2. Press the `i` key to enter edit mode and add the following content to the end of the file.

      ```Plain Text
      net.ipv4.conf.all.arp_announce = 2
      net.ipv4.conf.all.arp_ignore = 1
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>1</code> and <code>2</code> with the actual values required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjusting_arp_announce_and_arp_ignore_parameters_in_the_Linux_operating_system#.5YWz5LqOYXJwX2Fubm91bmNl5Y-C5pWw">About the arp_announce parameter</a> and <a href="https://docs.byteplus.com/en/docs/ecs/Adjusting_arp_announce_and_arp_ignore_parameters_in_the_Linux_operating_system#.5YWz5LqOYXJwX2lnbm9yZeWPguaVsA==">About the arp_ignore parameter</a>.      </div>
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to make the configuration take effect.

   ```Plain Text
   sysctl -p /etc/sysctl.d/arp.conf
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_36a0c7674884aceaeedb1bde556c906c.png) </span>


</Tab>
</Tabs>


<span id=".5Li654m55a6a572R5Y2h6YWN572u"></span>
### Configure parameters for a specific network interface

This method allows you to specify parameter values for a specific network interface without impacting the ARP request transmission and response policies of other network interfaces.


<Tabs>
<Tab zoneid="sZGS7v8gMP" title="Configuration by using the proc interface">
<TabTitle>Configuration by using the proc interface</TabTitle>

You can use this method to temporarily modify the parameter values while the operating system is running. Each time the instance restarts, you need to configure the parameters again.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the parameter values of the `eth0` network interface.

   ```Plain Text
   cat /proc/sys/net/ipv4/conf/eth0/arp_announce
   cat /proc/sys/net/ipv4/conf/eth0/arp_ignore
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>eth0</code> with the actual name of the network interface.   </div>
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5772b5d5e41a61c96561c1edb438f05e.png) </span>

3. Execute the following command to configure the values of the `arp_announce` and `arp_ignore` parameters.

   ```Plain Text
   echo 2 > /proc/sys/net/ipv4/conf/eth0/arp_announce
   echo 1 > /proc/sys/net/ipv4/conf/eth0/arp_ignore
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>1</code> and <code>2</code> with the actual values required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjusting_arp_announce_and_arp_ignore_parameters_in_the_Linux_operating_system#.5YWz5LqOYXJwX2Fubm91bmNl5Y-C5pWw">About the arp_announce parameter</a> and <a href="https://docs.byteplus.com/en/docs/ecs/Adjusting_arp_announce_and_arp_ignore_parameters_in_the_Linux_operating_system#.5YWz5LqOYXJwX2lnbm9yZeWPguaVsA==">About the arp_ignore parameter</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>eth0</code> with the actual name of the network interface.   </div>
   


</Tab>
<Tab zoneid="tn7KQQgqbQ" title="Configuration by using the arp.conf file">
<TabTitle>Configuration by using the arp.conf file</TabTitle>

You can use this method to permanently modify the parameter values while the operating system is running. You do not need to configure the parameters again after the instance restarts.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the parameter values of the eth0 network interface.

   ```Plain Text
   sysctl net.ipv4.conf.eth0.arp_announce
   sysctl net.ipv4.conf.eth0.arp_ignore
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>eth0</code> with the actual name of the network interface.   </div>
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f2d003e5187a2de678c1fabe59a4c255.png) </span>

3. Modify the values of the `arp_announce` and `arp_ignore`  parameters.

   1. Execute the following command to create the arp.conf file.

      ```Plain Text
      vim /etc/sysctl.d/arp.conf
      ```
      

   2. Press the `i` key to enter edit mode and add the following content to the end of the file.

      ```Plain Text
      net.ipv4.conf.eth0.arp_announce = 2
      net.ipv4.conf.eth0.arp_ignore = 1
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>1</code> and <code>2</code> with the actual values required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjusting_arp_announce_and_arp_ignore_parameters_in_the_Linux_operating_system#.5YWz5LqOYXJwX2Fubm91bmNl5Y-C5pWw">About the arp_announce parameter</a> and <a href="https://docs.byteplus.com/en/docs/ecs/Adjusting_arp_announce_and_arp_ignore_parameters_in_the_Linux_operating_system#.5YWz5LqOYXJwX2lnbm9yZeWPguaVsA==">About the arp_ignore parameter</a>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>eth0</code> with the actual name of the network interface.      </div>
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to make the configuration take effect.

   ```Plain Text
   sysctl -p /etc/sysctl.d/arp.conf
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_026f165dd628381d7adffe3a470ade32.png) </span>


</Tab>
</Tabs>
