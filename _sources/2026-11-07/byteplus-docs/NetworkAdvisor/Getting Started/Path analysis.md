---
title: "Path analysis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Path-Analysis"
---

This topic describes how to view the cloud traffic path between a source and a destination, and verify their connectivity.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

When an Elastic Compute Service (ECS) hosting your applications needs to access an ECS hosting your database, you can use Path Analysis to quickly verify network connectivity between them.​​

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_23160760831bffede0784bd33bbb9126.png) </span>

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

Before you begin, complete the following preparations:


1. Complete account registration.

2. [Create VPC and subnet](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

3. [Create a security group](https://docs.byteplus.com/en/docs/vpc/Creating-a-security-group) named Database.

4. Create two ECS instances. Name one ECS\-A and associate it with the default security group Default. Name the other ECS\-B and associate it with the security group Database. For specific steps, see [Purchasing an Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id=".5pON5L2c5rWB56iL"></span>
## Procedures

<span id=".5q2l6aqk5LiA77ya5Y-R6LW35YiG5p6Q"></span>
### Step 1: Initiate analysis


1. Log in to the [Path analysis console](https://console.byteplus.com/netadvisor/analysis).

2. Click **Analyze**.

3. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Example |
   |---|---|---|
   |Source |Enter the source IP address. This topic uses ECS\-A's primary private IP. |ECS\-A 192.168.0.2 |
   |Destination |Enter the destination IP address. This topic uses ECS\-B's primary private IP. |ECS\-B 192.168.3.2 |
   |Agreement |Select the protocol, supported types:<br><br><br>* TCP<br><br>* UDP<br><br>* ICMP |TCP |
   |Destination port |Enter the destination port, port range: 1–65535. This topic uses a Database server running on port 3306 as the scenario. |3306 |
   |Path instance |Whether to save the path instance. If you select Yes, the system will automatically generate a name for it based on your parameters. If the default name does not meet your requirements, you can manually enter a name for the path instance. |Yes, ECS_ECS_TCP_3306_172931 |
   

4. Click **Analyze** to start the analysis.


<span id=".5q2l6aqk5LqM77ya5p-l55yL6Lev5b6E5YiG5p6Q5oql5ZGK"></span>
### Step 2: View Path Analysis report


1. After the analysis is complete, view the Path Analysis report. As shown in the following figure:

2. Examine the traffic path between the source and destination resources, and verify whether the configuration of each path node is correct. If the path is unreachable, click the node highlighted in red to identify the configuration issue. Click the node name to navigate directly to the corresponding resource for configuration adjustments. For details, see [Analysis result and node](https://docs.byteplus.com/en/docs/NetworkAdvisor/Analysis-result-and-node).


<span id=".5q2l6aqk5LiJ77ya6YeN5paw5YiG5p6Q"></span>
### Step 3: Re\-analyze

After reconfiguring based on the analysis report, you can perform the analysis again (refer to this procedure) to verify whether the configuration is now correct.


1. Log in to the [Path analysis console](https://console.byteplus.com/netadvisor/analysis).

2. Click **Reanalyze** to the right of the target path instance.

3. After the analysis is complete, view the Path Analysis report.


&nbsp;
