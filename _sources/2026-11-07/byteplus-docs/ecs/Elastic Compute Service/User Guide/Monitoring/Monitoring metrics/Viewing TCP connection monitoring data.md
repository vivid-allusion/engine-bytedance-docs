---
title: "Viewing TCP connection monitoring data"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Viewing-instance-processes_TCP-connection-monitoring-data"
---

To allow you to view the TCP connection monitoring data for the instance operating system, BytePlus provides you with the TCP connection monitoring feature. This allows you to view metrics of the TCP connection state.

<span id=".5p-l55yLVENQ6L-e5o6l55uR5o6n5pWw5o2u"></span>
## View TCP connection monitoring data

<span id=".5L2_55So6K-05piO"></span>
### Usage notes

Before using TCP connection monitoring, you need to take the following actions:


* Currently, you can only view TCP connection monitoring information for instances with certain operating systems. Please make sure that the operating system of your instance has one of the following versions:

   
   |Type |Released version |
   |---|---|
   |CentOS |* CentOS Stream 9 64 bit<br><br>* CentOS Stream 8 64 bit<br><br>* CentOS 8.x 64 bit<br><br>* CentOS 7.2 64 bit and later versions |
   |Ubuntu |* Ubuntu Server 22.04 LTS 64 bit<br><br>* Ubuntu Server 20.04 LTS 64 bit<br><br>* Ubuntu Server 16.04 LTS 64 bit |
   |Debian |* Debian 11 64 bit<br><br>* 64\-bit Debian 9 |
   |Fedora |Fedora 37 64 bit |
   |veLinux |* veLinux 1.0 64 bit quick start image<br><br>* veLinux 1.0 CentOS compatible version with 5.10 kernel 64 bit<br><br>* veLinux 1.0 64 bit Hardened Image for Security Protection<br><br>* veLinux 1.0 CentOS compatible version 64 bit<br><br>* veLinux 1.0 with 5.10 kernel 64 bit<br><br>* veLinux 1.0 64 bit |
   |AlmaLinux |* AlmaLinux 9.1 64 bit<br><br>* AlmaLinux 8.7 64 bit |
   

* Please check whether the instance has been installed with the Cloud Monitor plugin according to the [ECS monitoring](https://docs.byteplus.com/en/docs/cloudmonitor/Overview-1) guide. If not, please refer to [Installing plugin](https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent) to install it.

* You need to manually enable the TCP connection monitoring feature. For details, refer to [TCP connection metrics missing](https://docs.byteplus.com/en/docs/ecs/Resolve-the-issue-of-missing-monitoring-metrics#.dGNw6L-e5o6l55uR5o6n57y65aSx).

* The collection frequency for TCP connection monitoring metrics is 30s. This means that TCP connection monitoring metrics are collected every 30s. 


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the top navigation bar, select the project and region of the target instance.

3. In the left\-side navigation pane, select "Instances & Images \> Instances".

4. Click the name of the target instance to go to the instance details page.

5. Select the "Monitoring \> TCP connection monitor" tab. On this tab, you can view metrics such as TCP bytes sent/received and connection retransmission counts for connections between local and remote IP addresses. For more metric details, refer to [Viewing TCP connection monitoring metrics](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-processes_TCP-connection-monitoring-data#.5p-l55yLdGNw6L-e5o6l55uR5o6n5oyH5qCH).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After the instance starts, wait approximately 10 minutes and then view the relevant metric data within the instance.   </div>
   

<span id=".55u45YWz5pON5L2c"></span>
### Related operation

You can also [create an alarm strategy](https://docs.byteplus.com/en/docs/cloudmonitor/Creating-an-alarm-strategy) for TCP connection monitoring. This helps you to learn whether processes on your ECS instance are alive in a timely manner and thereby ensures processes run properly.

<span id=".5p-l55yLVENQ6L-e5o6l55uR5o6n5oyH5qCH"></span>
## View TCP connection monitoring metrics

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The collection frequency for TCP connection monitoring is 30 seconds. This means that relevant TCP connection monitoring data is collected every 30 seconds.</div>



|Metric |Explanation |Unit |
|---|---|---|
|ProcTxBytes |Network bytes sent by processes |Byte |
|ProcRxBytes |Network bytes received by processes |Byte |
|ProcTxPackets |Network packets sent by processes |Count |
|ProcRxPackets |Network packets received by processes |Count |
|ConnTxBytes |Network bytes sent by TCP connections |Byte |
|ConnRxBytes |Network bytes received by TCP connections |Byte |
|ConnTxPackets |Network packets sent by TCP connections |Count |
|ConnRxPackets |Network packets received by TCP connections |Count |
|ConnRetransmits |Retransmission count of TCP connections |Count |
|ConnRTT |RTT of TCP connections |μs |
|ConnRTTVar |RTT variance of TCP connections |μs |
