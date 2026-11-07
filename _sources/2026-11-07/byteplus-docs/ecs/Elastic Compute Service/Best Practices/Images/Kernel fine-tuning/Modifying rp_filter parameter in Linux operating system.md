---
title: "Modifying rp_filter parameter in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Adjust_the_rp_filter_parameter_in_the_Linux_operating_system"
---

Modifying the `rp_filter` parameter to configure reverse path filtering mode for the server can help you prevent network security issues such as IP address spoofing.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the <code>rp_filter</code> parameter is configured incorrectly, it may block the source IP address and cause network disconnection. Additionally, enabling reverse routing verification may also lead to packet loss. In such cases, evaluate carefully before you modify the parameter.</div>


<span id=".5pyv6K-t6Kej6YeK"></span>
## Terms

<span id=".5YWz5LqOcnBfZmlsdGVy5Y-C5pWw"></span>
### About the rp_filter parameter

`rp_filter` (Reverse Path Filtering) is a network\-related parameter in the Linux kernel. It defines rules for network interfaces to perform reverse routing on received packets. It also helps verify the legitimacy of packets entering network devices (such as routers, firewalls, servers and other devices with network interfaces) by using reverse routing verification. Valid values:


* `0`: Disable reverse routing verification and do not verify the source IP address.

* `1`: Enable strict reverse routing verification. If the interface that receives the packet is not the optimal reverse path, the packet check will fail. By default, the packet will be discarded if the check fails.

* `2`: Enable loose reverse routing verification. If the source IP address cannot be reached through any interface, the packet check will fail.


<span id=".5Y-N5ZCR6Lev55Sx5qCh6aqM"></span>
### Reverse routing verification

Reverse routing verification is a check performed on data packets entering a network device. When a data packet arrives at a network interface of a network device, the device will check its routing table based on the source IP address of the packet. This is to determine which network interface should be used to return a packet to that source IP address, which refers to the return path. If the network interface corresponding to the identified return path is inconsistent with the actual network interface through which the packet entered the device, the packet may be problematic and potentially a forged one. In such cases, the packet can be handled according to the corresponding policy.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios


* **Servers with multiple network interfaces**

   In environments with multiple network interfaces, the `rp_filter` parameter can guide data packets to enter and exit through the intended network interfaces. This prevents packets from looping between different network interfaces.

* **Preventing IP spoofing attacks**

   On servers or hosts connected to the Internet, proper configuration of the `rp_filter` parameter enables checking the source IP addresses of inbound packets. This allows the system to discard packets that claim to originate from a subnet associated with a specific network interface but actually enter through an unintended network interface, thus avoiding IP spoofing.

* **Filtering exceptional traffic**

   In DDoS attack scenarios, attackers often forge source IP addresses to send massive amounts of packets. By properly configuring the `rp_filter` parameter to check the outbound paths corresponding to the source IP addresses of inbound packets, some abnormal packets with forged source IP addresses can be discarded. This discard process helps reduce invalid traffic flowing into the server.

* **Asymmetric routing or other complex routing**

   In scenarios using asymmetric routing or other complex routing setups, the `rp_filter` parameter can be configured to enable reverse routing verification (such as `1` or `2`) to prevent normal packets from being discarded.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

The `rp_filter` parameter can be configured either globally (for all interfaces) or on a per\-network interface basis.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The actual effective value for each network interface is the maximum of the global (all) configuration and the configuration specific to that interface. For example: The global <code>rp_filter</code> parameter is set to <code>1</code>, and the <code>rp_filter</code> parameter for the <code>eth0</code> network interface is set to <code>2</code>. In such cases, the actual effective value of the <code>rp_filter</code> parameter on the <code>eth0</code> network interface is <code>2</code>.</div>


<span id=".6YWN572u5YWo5bGA5Y-C5pWw"></span>
### Configure the global parameter

The global parameter configured using this method applies the same reverse path filtering mode to all network interfaces, facilitating batch management.


<Tabs>
<Tab zoneid="VTTpuQQ0DP" title="Configuration by using the proc interface">
<TabTitle>Configuration by using the proc interface</TabTitle>

You can use this method to temporarily modify the parameter value while the operating system is running. Each time the instance restarts, you need to configure the parameter again.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the value of the global `rp_filter` parameter.

   ```Plain Text
   cat /proc/sys/net/ipv4/conf/all/rp_filter
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_933f30e000ec27bc689b2111be5e2591.png) </span>

3. Execute the following command to configure the `rp_filter` parameter.

   ```Plain Text
   echo 1 > /proc/sys/net/ipv4/conf/all/rp_filter
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>1</code> with the actual value required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjust_the_rp_filter_parameter_in_the_Linux_operating_system#.5YWz5LqOcnBfZmlsdGVy5Y-C5pWw">About the rp_filter parameter</a>.   </div>
   


</Tab>
<Tab zoneid="kM4SadMtiy" title="Configuration by using the net_rp_filter.conf file">
<TabTitle>Configuration by using the net_rp_filter.conf file</TabTitle>

You can use this method to permanently modify the parameter value while the operating system is running. You do not need to configure the parameter again after the instance restarts.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current parameter value.

   ```Plain Text
   sysctl net.ipv4.conf.all.rp_filter
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9b346590e04d05a6596f9bf668524b9.png) </span>

3. Modify the value of the `rp_filter` parameter.

   1. Execute the following command to create the net_rp_filter.conf file.

      ```Plain Text
      vim /etc/sysctl.d/net_rp_filter.conf
      ```
      

   2. Press the `i` key to enter edit mode and add the following content to the end of the file.

      ```Plain Text
      net.ipv4.conf.all.rp_filter = 1
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>1</code> with the actual value required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjust_the_rp_filter_parameter_in_the_Linux_operating_system#.5YWz5LqOcnBfZmlsdGVy5Y-C5pWw">About the rp_filter parameter</a>.      </div>
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to make the configuration take effect.

   ```Plain Text
   sysctl -p /etc/sysctl.d/net_rp_filter.conf
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe703a704bdcf735d44f02e68f129f39.png) </span>


</Tab>
</Tabs>


<span id=".5Li654m55a6a572R5Y2h6YWN572u"></span>
### Configure the parameter for a specific network interface

This method allows you to specify the parameter value for a specific network interface without impacting the reverse path filtering mode of other network interfaces.


<Tabs>
<Tab zoneid="xfwVHHTnvR" title="Configuration by using the proc interface">
<TabTitle>Configuration by using the proc interface</TabTitle>

You can use this method to temporarily modify the parameter value while the operating system is running. Each time the instance restarts, you need to configure the parameter again.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the parameter value of the `eth0` network interface.

   ```Plain Text
   cat /proc/sys/net/ipv4/conf/eth0/rp_filter
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>eth0</code> with the actual name of the network interface.   </div>
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e20eb2454c54892ba3914746ff346790.png) </span>

3. Execute the following command to configure the `rp_filter` parameter.

   ```Plain Text
   echo 1 > /proc/sys/net/ipv4/conf/eth0/rp_filter
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>1</code> with the actual value required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjust_the_rp_filter_parameter_in_the_Linux_operating_system#.5YWz5LqOcnBfZmlsdGVy5Y-C5pWw">About the rp_filter parameter</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"> Replace <code>eth0</code> with the actual name of the network interface.   </div>
   


</Tab>
<Tab zoneid="Mcv10AXmWs" title="Configuration by using the net_rp_filter.conf file">
<TabTitle>Configuration by using the net_rp_filter.conf file</TabTitle>

You can use this method to permanently modify the parameter value while the operating system is running. You do not need to configure the parameter again after the instance restarts.


1. Log in to the target instance. For more information, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current parameter value.

   ```Plain Text
   sysctl net.ipv4.conf.eth0.rp_filter
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>eth0</code> with the actual name of the network interface.   </div>
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08b902b38da84c9337079d6b14f24d6b.png) </span>

3. Modify the value of the `rp_filter` parameter.

   1. Execute the following command to create the net_rp_filter.conf file.

      ```Plain Text
      vim /etc/sysctl.d/net_rp_filter.conf
      ```
      

   2. Press the `i` key to enter edit mode and add the following content to the end of the file.

      ```Plain Text
      net.ipv4.conf.eth0.rp_filter = 1
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>1</code> with the actual value required for your business. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Adjust_the_rp_filter_parameter_in_the_Linux_operating_system#.5YWz5LqOcnBfZmlsdGVy5Y-C5pWw">About the rp_filter parameter</a>.      </div>
      

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>eth0</code> with the actual name of the network interface.      </div>
      

   3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.

4. Execute the following command to make the configuration take effect.

   ```Plain Text
   sysctl -p /etc/sysctl.d/net_rp_filter.conf
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7aa3fb585c1c8077fff5ad64f1f8d331.png) </span>


</Tab>
</Tabs>
