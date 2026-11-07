---
title: "Capturing network packets"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Packet_capture"
---

Cloud\-native observability of BytePlus (full\-stack observability) can capture network packets on the specified workload or pod, which facilitates troubleshooting of container networks. This topic describes how to configure the network packet capture feature.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Network packet capture is an important troubleshooting method for complex container environments. If you perform network packet analysis on specified workloads or pods, the following scenario issues can be effectively resolved:


1. **Network troubleshooting**: When network issues occur, packet capture can help identify the issues. Packets on different nodes are analyzed to troubleshoot connections or configurations.

2. **Security analysis**: Security teams can use packet capture to monitor network traffic and identify potential security threats, such as DDoS attacks and ARP spoofing.

3. **Performance optimization**: Network traffic is analyzed to identify performance issues, such as requests with long response times or unnecessary repeated requests. This provides optimization solutions to specific performance issues.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* TOS has been activated, and a TOS bucket has been created in the same region as the target VKE cluster. For details, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* Cloud\-native observability has been enabled. For details, see [Enabling observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability).

* Full\-stack observability has been enabled. For details, see [Enabling full-stack observability](https://docs.byteplus.com/en/docs/vke/Network-and-application-observability).

* The microscope agent in full\-stack observability has been upgraded to version 1.10.0 or later.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5oqT5YyF6YWN572u"></span>
### Step 1: Configure packet capture


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster.

4. In the left navigation bar of the cluster management page, click **Monitoring center** \> **Packet capture**. On the page that appears, click **Packet capture configuration** to configure the TOS that corresponds to the packet capture task.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_40b040d7a9b9609234231060beef01b2.png) </span>

5. Click **Enable** to enable the TOS configuration and specify the parameters of the TOS bucket.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_96e8b5982135987895e06a508b686e37.png) </span>

   
   |Parameters |Description |
   |---|---|
   |Bucket name |Select the created TOS bucket from the drop\-down list. |
   |Subdirectory |Specify the path where the packet capture results are saved in the TOS bucket. If this parameter is not specified, the path is `/`. |
   

6. Click **Confirm**.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65oqT5YyF5Lu75Yqh"></span>
### Step 2: Create a packet capture task

<span id="FtBJgCiN"></span>
#### Directly creating a packet capture task

You can perform the following steps to directly configure a packet capture task on the **Network packet capture** page:


1. In the left navigation bar of the cluster management page, click **Monitoring center** \> **Packet capture**. On the page that appears, click **Create packet capture task**, and configure the details of the packet capture task.

   * **Basic information**

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b1fb6d74e090bc0a3e4bfaf34115573f.png) </span>

      
      |Parameters |Description |
      |---|---|
      |Name |The name of the packet capture task. |
      |Description |You can add a description for the packet capture task as needed. This parameter is left empty by default. |
      

   * **Targets**

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_318236a0bd1d25093126b2ffa48f4eb1.png) </span>

      
      |Parameters |Description |
      |---|---|
      |Target |Configure the targets of the packet capture task. You can configure multiple packet capture targets for the same packet capture task. |
      |Namespace |Select the namespace where the target of the packet capture task is located. |
      |Workload type |Select the type of packet capture target. Valid values:<br><br><br>* **Deployment**<br><br>* **StatefulSet**<br><br>* **DaemonSet**<br><br>* **Pod** |
      |Workload name |Select the target workload of the packet capture task. |
      |Pods |Select the target pod of the packet capture task. |
      |Network interface |Configure a network interface card (NIC) for the packet capture target, such as `eth0`. The default value is `any`, which indicates all NICs. |
      |Maximum packet length |Specify the maximum length of the packet. The value must be an integer. Units can be KB, MB, or GB. The packet can be up to 2 GB in length. |
      |Duration |Specify the duration of the packet capture task. The value must be an integer. Unit: seconds. If you have not configured a packet capture duration, you need to manually stop the packet capture task. |
      |Rules |Configure the packet capture rules.<br><br><br>* **Protocol**: Configure the packet capture protocol. Valid values: **Any**, **TCP**, **UDP**, and **ICMP**.<br><br>* **Source addresses**: Configure the source address for packet capture. You can configure a single IP address, such as `192.168.1.10`, multiple IP addresses that need to be separated by `\|`, such as `192.168.1.10\|192.168.1.20`, or a CIDR block, such as `192.168.1.0/24`.<br><br>* **Source port**: Configure the source port number for packet capture. You can configure a single port number, such as `80`. If this parameter is left empty, it indicates all ports are used, which are `1 to 65535`.<br><br>* **Target addresses**: Configure the target address for packet capture. You can configure a single IP address, such as `192.168.1.10`, multiple IP addresses that need to be separated by `\|`, such as `192.168.1.10\|192.168.1.20`, or a CIDR block, such as `192.168.1.0/24`.<br><br>* **Target port**: Configure the target port number for packet capture. You can configure a single port number, such as `80`. If this parameter is left empty, it indicates all ports are used, which are `1 to 65535`. |
      

2. Click **Confirm** to start capturing packets.


<span id=".57uT5p6c6aqM6K-B"></span>
#### Creating tasks by using cluster topologies

You can perform the following steps to create a packet capture task by using network topologies on the **Topology** page:


1. In the left navigation bar of the cluster management page, click **Monitoring center** \> **Cluster topology**. View the topology chart of workload resources.

2. In the topology, find the target line between two workload nodes, move the pointer over the line, and then click **Network packet capture** in the pop\-up overview window. Then, you are redirected to the Network packet capture page and configure the packet capture task. For a specific packet capture configuration, see [Directly creating packet capture tasks](https://docs.byteplus.com/en/docs/90/41302#.55u05o6l5Yib5bu65oqT5YyF5Lu75Yqh).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c65099a4cabfa2d749b3575edb36a6e.png) </span>


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

After the packet capture task is configured, the system starts capturing packets based on the configurations.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b26d2d6db81ff829bdec07a3a671733.png) </span>

When the task state changes to **Finish**, it indicates that the packet capture task is complete. Click **View details** in the **Actions** column to view the details of the packet capture task. Click **Download** in the **Actions** column that corresponds to the target **packet capture task** to download the packet capture file in pcap format to your on\-premises computer.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_587ffec73a1c0291d781b8a0d7d87f6e.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can use the Wireshark tool on your on\-premises computer to analyze the packet capture file in pcap format.</div>
