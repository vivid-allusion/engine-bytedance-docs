---
title: "Direct Connect troubleshooting"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Troubleshooting-and-solutions-for-Direct-Connect-issues"
---

Direct Connect (DC) is used to establish a high\-speed, low\-latency, stable, and secure dedicated connection channel between your on\-premises data center (IDC) and the Virtual Private Cloud (VPC). When servers in your on\-premises IDC cannot access services in your VPC via Direct Connect, or when other issues such as packet loss or failure to meet bandwidth standards occur, you can refer to this topic for preliminary troubleshooting.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the Direct Connect issue remains unresolved after self\-service troubleshooting following this topic, <a href="https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000250&FlowKey=dWDQrtPnGIfADlVgCfaz">submit a ticket</a> to contact BytePlus operational engineers for assistance.</div>


<span id=".5qOA5p-l5LiT57q_6ZO-6Lev6L-e5o6l54q25oCB"></span>
## **Check Direct Connect link status**

<span id=".5Y-v6IO95Y6f5Zug"></span>
#### Possible reasons

The Direct Connect link status is abnormal.

<span id=".5o6S5p-l5pa55qGI"></span>
#### Troubleshooting solution


1. Check whether the status of the on\-premises IDC access port is **DOWN**.

   * If the status of the on\-premises IDC access port is **DOWN**, follow the steps below to troubleshoot.

   * If the status of the on\-premises IDC access port is not **DOWN**, refer to other sections in this topic for further troubleshooting.

2. When the status of the on\-premises IDC access port is **DOWN**, follow these steps to troubleshoot the connection issue.

   1. Check the access port configuration.

      confirm that the port on your on\-premises IDC access device is already in an active status. You need to review the relevant configuration to ensure the port has not been shut down via a `shutdown` command or placed in another inactive status. If such configurations exist, remove them promptly.

   2. Check the status of the optical modules.

      check if your optical modules are functioning normally, including indicators such as optical transmit/receive power and voltage. The details are as follows:

      * If this is your first time deploying Direct Connect, it is recommended to use optical module pairs from the same manufacturer and of the same specifications to avoid failures caused by device compatibility issues.

      * If optical module abnormalities occur during use, it may indicate a module failure. confirm whether the optical module status on the data center side is normal, and contact the after\-sales service manager to check the condition of the DC Gateway optical module. If all appears normal, the issue may lie within the transmission link. In this case, consult your network line operator to check for any link failures.

   3. Verify Direct Connect connectivity.

      If you are accessing Direct Connect for the first time, you need to confirm with the Direct Connect line operator whether the Direct Connect has been connected end\-to\-end and obtain relevant documentation, including the Direct Connect construction completion certificate and end\-to\-end network connectivity test report.


<span id=".5qOA5p-l5piv5ZCm5a2Y5ZyoQ1JD6ZSZ5YyF"></span>
## Check for CRC error packets

<span id=".5Y-v6IO95Y6f5Zug"></span>
#### Possible reasons

CRC error packets. CRC error packets related to Direct Connect may appear at the following two locations:


* CRC error packets on the interconnection port of the on\-premises IDC side.

* CRC error packets on the BytePlus Direct Connect Virtual Interface.

   You can view the CRC error packet status for the BytePlus Virtual Interface on the data monitoring page of the BytePlus Direct Connect console. If the number of CRC error packets reaches a high\-risk threshold, the platform will proactively notify you.


<span id=".5o6S5p-l5pa55qGI"></span>
#### Troubleshooting solution


1. Check for CRC error packet issues. CRC errors typically originate from the physical layer of data transmission and may be related to abnormal optical module status.

   * If CRC error packets are observed, follow the steps below to troubleshoot.

   * If CRC error packets are not observed, refer to other sections in this topic for further troubleshooting.

2. When CRC error packets occur, follow these steps to troubleshoot the issue:

   1. Check whether key indicators of the optical modules, such as optical transmit/receive power and voltage, are within normal ranges. If abnormal data indicators are found, it is recommended that you first try reseating the optical modules to see if this restores normal operation.

   2. If the problem persists, further test whether the fiber optic attenuation is abnormal.

      * If an issue is found with the fiber optic cables, promptly contact your cable supplier for repair.

      * If the fiber optic cables are normal, it is recommended that you consider replacing the optical modules. To replace the optical module provided by BytePlus, [submit a ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000250&FlowKey=dWDQrtPnGIfADlVgCfaz).


<span id=".5qOA5p-l572R57uc6YWN572u"></span>
## Check network configuration

<span id=".5Y-v6IO95Y6f5Zug"></span>
#### Possible reasons

The cause of Direct Connect faults due to network issues may fall into the following four scenarios, you need to troubleshoot them separately.


* Virtual Interface IP cannot be pinged

* BGP fails to establish

* Protocol is not working properly

* Packet loss during ping


<span id=".5o6S5p-l5pa55qGI"></span>
#### Troubleshooting solution

**Check 1: Virtual Interface IP cannot be pinged**


1. Ping the Virtual Interface IP address from the on\-premises IDC side to check if the Virtual Interface IP is reachable.

   * If the Virtual Interface IP cannot be pinged, proceed with the following troubleshooting steps.

   * If the Virtual Interface IP can be pinged, proceed to check the BGP peer negotiation status.

2. If the interface indicators on the local IDC equipment are normal, but the access device cannot ping the DC Gateway's Virtual Interface IP, troubleshoot the issue using the following steps:

   * **IP address configuration**: Ensure that you have correctly configured the interconnection IP addresses.

      * Check whether the interconnection IP addresses are in the same subnet as the IP addresses configured for the Virtual Interface.

      * Verify that the IP addresses configured at both ends of the Direct Connect are unique (no IP address reuse) and ensure these IP addresses are configured in the correct VLAN.

   * **VLAN configuration**: If the VLAN ID configured when creating the Virtual Interface in the BytePlus console is not 0, you must ensure that all devices—​including the on\-premises IDC access device, the line operator's DC connection, the DC Gateway device, and any Layer 2/Layer 3 devices between them—​allow the configured VLAN ID to pass through.

   * **ARP table verification**: Check the ARP table of the on\-premises IDC device to confirm that it has correctly learned the MAC address entry for the DC Gateway's Virtual Interface.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the correct ARP entry has not been learned, or if you still cannot ping the DC Gateway Virtual Interface after completing the above checks, <a href="https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000250&FlowKey=dWDQrtPnGIfADlVgCfaz">Submit ticket</a> for further consultation.</div>


&nbsp;

**Check 2: BGP negotiation failure**

If the BGP peer configured between the IDC device and the DC Gateway cannot reach an Established status, troubleshoot this issue with the following steps:


1. Check the BGP configuration.

   Ensure BGP is correctly configured on your IDC device. The BGP Local ASN on the on\-premises IDC side should match the ASN configured when you create the Virtual Interface in the BytePlus console. The BGP Remote ASN on the on\-premises IDC side should be BytePlus's ASN: 137718. The BGP peer IP should be set to the Virtual Interface IP address of the DC Gateway. The BGP MD5 authentication key must match the key you configured in the cloud console.

2. Confirm the security policy.

   Check the security policies on your IDC device to ensure they permit the passage of BGP packets and TCP port 179 (the default port used by BGP).

3. Monitor the BGP peer status machine and observe its status.

   
   |Status |Description |
   |---|---|
   |**Idle** |If the BGP peer remains in this status, the BGP peer may have been shutdown or ignored, which automatically closes all connections. You need to check the relevant configuration on the device and remove these commands if possible. |
   |**Connect/Active** |If the BGP peer is in the Connect or Active status, it indicates a failure in the TCP connection for BGP. This could be due to a link communication failure or an incorrect BGP peer password configuration. You need to check the related configuration. |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If no issues are found after completing the above checks but the BGP status still cannot reach <strong>Established</strong>, <a href="https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000250&FlowKey=dWDQrtPnGIfADlVgCfaz">Submit ticket</a> for consultation.</div>


&nbsp;

**Check 3: Verify protocol operation**


* If BFD protocol is enabled, check that BFD is correctly configured on your IDC device. This requires referring to the configuration guide provided by your IDC switch vendor for the specific switch model. Also, verify that security policies allow BFD packets / UDP ports 3784/3785.

   You can observe the BFD status machine to infer potential issues.

   
   |Status |Description |
   |---|---|
   |**Admin Down** |In this status, it indicates that your BFD has been manually shut down. You need to remove configurations (such as shutdown) and re\-enable BFD. |
   |**Down** |Down status: This occurs in two scenarios:<br><br><br>1. The initial status has never negotiated to UP. This is likely due to incorrect configuration preventing the correct sending and receiving of BFD packets.<br><br>2. It was previously negotiated to UP but has now transitioned to Down due to some reason. In this case, use tools like Ping to check link connectivity.<br><br>   * If link connectivity is fine, it might be due to link flapping or increased latency causing BFD packet timeouts.<br><br>   * If it remains persistently Down or fluctuates frequently, [Submit ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000250&FlowKey=dWDQrtPnGIfADlVgCfaz) for consultation. |
   |**Init** |Init status: This is an intermediate status and is usually not problematic. If it remains persistently in the Init status, it is likely that there is an issue with the peer's BFD status machine; investigate this. |
   

* If NQA detection is enabled: The BytePlus side of the Direct Connect uses NQA\-ICMP for path detection. Ensure that the security policies on your local IDC device allow ICMP packets.


&nbsp;

**Check 4: Packet loss during ping**

When using `ping` command to test the network connection, if there is packet loss or intermittent connectivity, consider the following issues:


* **Network congestion**: When your Direct Connect bandwidth is fully utilized, Ping packets may be dropped due to congestion. You can go to the BytePlus Direct Connect console and check the Traffic Monitoring to determine if this is the issue.

* **Route ECMP**: If there is Route ECMP (Equal\-Cost Multi\-Path) on the Ping path, one of the paths might be faulty. You need to check if this situation exists in your on\-premises IDC network. If you need to check whether this situation exists on the BytePlus side, you can [Submit ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000250&FlowKey=dWDQrtPnGIfADlVgCfaz) for assistance with troubleshooting.


<span id=".5qOA5p-l6Lev55Sx6YWN572u"></span>
## **Check route configuration**


* If you select **Static routing** as the routing type when creating the Virtual Interface in the BytePlus console, perform the following checks:

   1. On the BytePlus console, check if the configured static route is used for egress traffic (from the VPC to the on\-premises IDC direction). You need to confirm that the network segment of the configured static route aligns with your network plan.

   2. On the on\-premises IDC device, check if the configured static route is used for ingress traffic (from the on\-premises IDC to the VPC direction). Similarly, you should check if the route's network segment matches the network plan.

* If you select **BGP route** as the routing type when creating the Virtual Interface in the BytePlus console: For ingress routes (from the on\-premises IDC to the VPC direction), when associated with CEN, the routes within the CEN will be automatically advertised to your on\-premises IDC device to enable BGP route propagation. For egress routes (from the VPC to the on\-premises IDC direction), they need to be configured in the BGP settings of your on\-premises IDC.

   You can view the routing information on the DC Gateway \> Routing information page in the BytePlus console.


<span id=".5qOA5p-l5bim5a695piv5ZCm56ym5ZCI6aKE5pyf"></span>
## Check for the MAC addresses conflict

If the MAC address used by your local IDC device is identical to any MAC address on the BytePlus DAS side, interconnection and forwarding will fail after Direct Connect access. Therefore, avoid using the following five MAC addresses for your IDC devices:


* 0001\-0001\-0100

* 0001\-0001\-0101

* 0001\-0001\-0102

* 0001\-0001\-0103

* 0001\-0001\-0104


<span id=".5qOA5p-l5bim5a695piv5ZCm56ym5ZCI6aKE5pyf"></span>
## Verify whether the bandwidth meets expectations

<span id=".5Y-v6IO95Y6f5Zug"></span>
#### Possible reasons

Issues caused by insufficient bandwidth.

<span id=".5o6S5p-l5pa55qGI"></span>
#### Troubleshooting solution

If you feel that the bandwidth of Direct Connect does not match the purchased bandwidth while using Direct Connect, you can use the iPerf tool to test the bandwidth. For detailed operation methods, see [Using iPerf3 to Test Network Performance--Elastic Compute Service (ECS)-BytePlus](https://docs.byteplus.com/en/docs/ecs/Using-iPerf3-to-test-network-performance). If testing with the iPerf tool shows that the bandwidth indeed does not meet expectations, you can perform segmented troubleshooting, as illustrated in the figure below:


1. Connect a laptop at Point **1**, test the speed from IDC\-PC to Point **1**, and record the result.

   * If the rate meets expectations, proceed to Step 2.

   * If the rate does not meet expectations, troubleshoot the intranet of the on\-premises IDC.

2. Connect a laptop at Point **1**, test the speed to Volcano VPC\-ECS, and record the result.

   * If the rate meets expectations, troubleshoot the IDC switch configuration, interface negotiation rate, and whether the network cables/fiber optics have degraded.

   * If the rate does not meet expectations, proceed to Step 3.

3. At Point **1** and Point **2**, connect laptops simultaneously, test the speed from laptop 1 to laptop 2, and record the result.

   * If the rate meets expectations, proceed to Step 4;

   * If the rate does not meet expectations, report the issue to your line operator for fault investigation.

4. Access the laptop at Point **2**, test the VPC\-ECS rate, and record the result.

   * If it meets expectations, focus on troubleshooting Inside the building, etc.

   * If the rate does not meet expectations, it is necessary to focus on investigating the link between the DAS and the VPC. contact the BytePlus operations team to assist you with the investigation.
