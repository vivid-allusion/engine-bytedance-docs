---
title: "What is Network Advisor"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/What-is-Network-Advisor"
---

Network Advisor (NA) provides functionalities such as network topology, path analysis, instance diagnostics, traffic analysis, and performance monitoring to facilitate network O&M.

## Network Topology

Through network topology, users can clearly and intuitively understand their cloud resources on the BytePlus, quickly grasp the network architecture, and thus facilitate subsequent network operations, expansion, and optimization of the network architecture.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f0fc87779aa60b5c297a18463d467096.png)

## Path Analysis

Path Analysis allows users to intuitively check network reachability and view the cloud path of access traffic from the source to the destination. This helps troubleshoot configuration issues at various nodes along the path, aiding in the resolution of network configuration problems.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d72a1357dfc46bfca9d00bd28bbbaf38.png)

|Composition |Explanation |
|---|---|
|Analysis nodes |Analysis nodes refer to the path nodes traversed by the access traffic from the source to the destination within the cloud. For example, Network Interface, subnet, Internet NAT Gateway, Classic Load Balancer (CLB), etc. For details, see [Analysis nodes](https://docs.byteplus.com/en/docs/NetworkAdvisor/Analysis-result-and-node#.5YiG5p6Q6IqC54K5). |
|Analysis results |Analyze the traffic path from the source to the destination. A path analysis report is automatically generated. For details, see [Analysis results](https://docs.byteplus.com/en/docs/NetworkAdvisor/Analysis-result-and-node#.5YiG5p6Q57uT5p6c). |

## Instance Diagnosis

Instance Diagnostics enables users to diagnose the configuration and operational status of target network products. Based on the diagnostic results, users can verify product configurations and identify potential risks and issues during product operation, thereby enhancing operational efficiency.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_39fd3aabe9798f43ca47e8278b70bd8e.png)

|Composition |Explanation |
|---|---|
|Diagnostic​ items |Instance Diagnostics identifies and organizes error\-prone, easily overlooked, and hard\-to\-locate issues during product configuration and operation into diagnostic items. [Prerequisite](https://docs.byteplus.com/en/docs/NetworkAdvisor/Instance-Diagnostic-item) |
|Diagnostic report |After diagnosing an instance, Instance Diagnostics compares the diagnostic items and generates a diagnostic report to help users pinpoint issues. |

## Traffic Analysis

Traffic Analysis provides users with clear visibility into service traffic distribution and usage, facilitating subsequent network optimization and expansion. When traffic anomalies occur, you can analyze abnormal traffic and perform targeted mitigation.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_909c63fb4e7a571e6219d53b3d95121e.png)

|Classification |Explanation |
|---|---|
|Cross\-region traffic analysis |It supports analyzing outbound traffic between specific cloud regions. |
|Internet Traffic Analysis |It supports analyzing inbound and outbound internet traffic by region. |
|Hybird Cloud Traffic Analysis |It supports analyzing traffic between cloud and on\-premises environments. |

## Performance Monitoring

Internet performance monitoring lets you view the average delay of access to BytePlus resources across different Regions. This helps you select the optimal Region for deploying your services.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b350ff860ccd564b162d56d5ff8f564.png)

Cloud network performance lets you view the average delay between different Regions of BytePlus, as well as between different Availability Zones within the same Region. Use this information to choose the best Region or Availability Zone for deploying your services.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c80f71baf7a220c5d98f97d74a4790f3.png)
