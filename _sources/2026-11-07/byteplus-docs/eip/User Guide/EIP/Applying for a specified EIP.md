---
title: "Applying for a specified EIP"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Apply-for-a-designated-EIP"
---

If an Elastic IP Address (EIP) is mistakenly released and has not been applied by other users, you can recover it through this action.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only normal BGP (Multi\-ISP) type EIPs can be recovered.</div>


<span id="QvsSoCMi"></span>
## **Instructions**


* Only EIPs released after May 28, 2024, that have not been allocated to other users or locked can be recovered.

* Each account can apply up to 3 times per month per region.

* Specified recovered specified EIPs will still occupy the EIP quota. The recovered EIPs are billed by default on a pay\-by\-data\-transfer basis, with a maximum bandwidth of 1 Mbps. You can [modify](https://docs.byteplus.com/en/docs/eip/Modifying-the-maximum-bandwidth) it as needed after successful application.

* EIPs released from the IP address pool can only be recovered by the root account of the IP address pool.


<span id="1p9MlCUm"></span>
## **Procedure**


1. Log in to the EIP [console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the target region and project.

3. Click **Apply for specified EIP** on the EIP interface to open the application window.

4. Enter the EIP address and select the ISP type (default is **BGP (multi\-line)** ).

5. Click **Apply** to complete the action.


<span id="CeuOg12n"></span>
## **Related documents**

[AllocateEipAddress](https://docs.byteplus.com/en/docs/eip/AllocateEipAddress): Apply for an EIP.
