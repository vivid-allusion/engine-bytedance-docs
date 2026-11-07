---
title: "Managing path analysis"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/Managing-path-analysis"
---

<span id=".5Y-R6LW35YiG5p6Q"></span>
## Analyze


1. Log in to the [Path Analysis console](https://console.byteplus.com/netadvisor/analysis).

2. Click **Analyze**.

3. Configure parameters based on the table below.

   
   |Parameters |Notes |Example |
   |---|---|---|
   |Source |Select the End Type (i.e., how the source IP accesses the network) and configure the source IP address. The following options are supported:<br><br><br>* Elastic Compute Service (ECS): Select the primary private IPv4 address of the ECS instance's primary network interface or secondary network interface.<br><br>* EIP: Enter a public IPv4 address (it is not restricted to BytePlus public IPv4 addresses).<br><br>* Direct Connect Gateway: Enter the private IP address of the on\-premises IDC.<br><br>* TR\-type IPsec\-VPN connection: Enter the private IPv4 address of the on\-premises IDC.<br><br>* VPN gateway: Enter a private IPv4 address. |EIP, 101.XX.XX.161 |
   |Destination |Select the End Type (i.e., how the destination IP accesses the network) and configure the destination IP address. Supported options:<br><br><br>* Elastic Compute Service (ECS): Select the primary private IPv4 address of the ECS instance's primary network interface or secondary network interface.<br><br>* Classic Load Balancer: select CLB.<br><br>* Elastic IP Address (EIP): Enter a public IPv4 address (it is not restricted to BytePlus public IPv4 addresses).<br><br>* Direct Connect Gateway: Enter the private IP address of the on\-premises IDC.<br><br>* TR\-type IPsec\-VPN connection: Enter the private IPv4 address of the on\-premises IDC.<br><br>* VPN gateway: Enter a private IPv4 address.<br><br>* Private IP: Select the Private IP end type when the network access method of the destination IP is uncertain, and enter the private IP address.<br><br>* PrivateLink: Enter the IP address of the interface endpoint network interface. |ECS\-A, 192.168.0.2 |
   |Protocol |Select protocol. Supported protocols include TCP, UDP, and ICMP. |TCP |
   |Destination port |Enter the destination port, port range: 1–65535. |80 |
   |Path instance |Whether to save the path instance. If you select Yes, the system will automatically generate a name for it based on your parameters. If the default name does not meet your requirements, you can manually enter a name for the path instance. |Yes, PublicIP_ECS_TCP_80_192657 |
   

4. Click **Analyze** to run path analysis.

5. After the analysis is complete, view the Path Analysis report. As shown in the following figure:

6. You can troubleshoot issues based on the prompts provided in the diagnostic report. If the path is unreachable, click the node highlighted in red to identify the configuration issue. Click the node name to navigate directly to the corresponding resource for configuration adjustments. For details, see [Analysis results and nodes](https://docs.byteplus.com/en/docs/NetworkAdvisor/Analysis-result-and-node).


<span id=".6YeN5paw5YiG5p6Q"></span>
## Reanalyze

You can refer to this procedure to re\-analyze the target path instance and verify whether the traffic is reachable.


1. Log in to the [Path Analysis console](https://console.byteplus.com/netadvisor/analysis).

2. Click **Reanalyze** to the right of the target path instance.

3. After the analysis is complete, view the Path Analysis report.


<span id=".5Y-N5ZCR5YiG5p6Q"></span>
## Reverse analysis

Simply swap the source and destination IP addresses of the target path instance and perform the path analysis again.

<span id=".57qm5p2f6ZmQ5Yi2"></span>
### Limits

Reverse analysis is not supported when the destination **End type** is selected as CLB or Private IP.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [Path Analysis console](https://console.byteplus.com/netadvisor/analysis).

2. Click **Reverse** to the right of the target path instance.

3. Click **Reverse** to run path analysis.

4. You can troubleshoot issues based on the prompts provided in the diagnostic report. If the path is unreachable, click the node highlighted in red to identify the configuration issue. Click the node name to navigate directly to the corresponding resource for configuration adjustments. For details, see [Analysis results and nodes](https://docs.byteplus.com/en/docs/NetworkAdvisor/Analysis-result-and-node).


<span id=".5Yig6Zmk6Lev5b6E5YiG5p6Q"></span>
## Delete path analysis

If a path instance record is no longer needed, you can refer to this procedure to delete it.


1. Log in to the [Path Analysis console](https://console.byteplus.com/netadvisor/analysis).

2. Click **Delete** on the right side of the destination path analysis.

3. Click **Delete** to complete the action.
