---
title: "Releasing an EIP"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Releasing-an-EIP"
---

You can release an Elastic IP Address (EIP) when it is no longer needed.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* Attached EIPs cannot be released. Disassociate the EIP before performing the release operation. Refer to [Disassociating an EIP](https://docs.byteplus.com/en/docs/eip/Disassociating-Cloud-Resource-from-an-EIP) for specific operations.

* The EIP is pay\-as\-you\-go or the subscription EIP has expired. To release a subscription EIP before expiration, see [Unsubscription notes](https://docs.byteplus.com/en/docs/eip/Unsubscription).

* Normal release of BGP (Multi\-ISP) type EIPs allows recovery via [Applying for specified EIP](https://docs.byteplus.com/en/docs/eip/Apply-for-a-designated-EIP). If the EIP is allocated to another user or locked, it cannot be recovered.

* EIPs support both standard release and force release. Standard release has scenario restrictions to prevent accidental business disruptions. Force release removes most restrictions, enabling more efficient EIP release. Details are as follows:

   
   |Scenario restriction |Standard release |Force release |
   |---|---|---|
   |Add to Bandwidth Package |x |✓ |
   |Associate with ECS |x |✓ |
   |Associate with network interface |x |✓ |
   |Associate with Private CLB |x |✓ |
   |Associate with HAVIP |x |✓ |
   |Associate with IP address |x |✓ |
   |Associate with Internet NAT gateway |x |If an EIP is associated with an Internet NAT gateway that has no SNAT or DNAT entries, you can forcibly release the EIP. If it is associated with a SNAT or DNAT entry, delete the entry first, then forcibly release the EIP. |
   |Associate with Public CLB |x |x |
   

   "✓" indicates support for the release method, and "x" indicates no support for the release method.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After forcibly releasing the EIP attached to Elastic Compute Service (ECS), network interface, private Classic Load Balancer (CLB), High\-Availability Virtual IP Address (HAVIP), or IP Address, the services using these IPs will stop working. You must reattach the EIP and complete relevant configurations for recovery. Fully evaluate your services before using force release.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">EIPs of Public CLBs do not support release. If release is needed, first <a href="https://docs.byteplus.com/en/docs/clb/CLB-instances-04">convert to private load balancer </a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The feature of associating IP addresses is in the beta stage. If you need a trial, contact your account manager.   </div>
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in [to the EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of your target EIP.

3. Select the release method based on your actual business scenario:

   
   <Tabs>
   <Tab zoneid="O5fPaYUTUF" title="Standard release">
   <TabTitle>Standard release</TabTitle>
   
   1. In the EIP list, click  **··· \> Release** next to the target Elastic IP Address to open the confirmation dialog box.
   
   2. Click **Release ** to complete the operation.
   
   
   </Tab>
   <Tab zoneid="lw7TmYyP3q" title="Force release">
   <TabTitle>Force release</TabTitle>
   
   1. In the EIP list, click the target EIP's right side  **··· \> Force release** to open the confirm force release dialog box.
   
   2. Click **Force release** to complete the action.
   
   
   </Tab>
   </Tabs>
   


<span id="xDF2P8g0"></span>
## Related actions

[Apply for a specified EIP](https://docs.byteplus.com/en/docs/eip/Apply-for-a-designated-EIP): When an EIP is mistakenly released, you can apply to recover the EIP before another user applies for it.

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ReleaseEipAddress](https://docs.byteplus.com/en/docs/eip/ReleaseEipAddress): Release an EIP.
