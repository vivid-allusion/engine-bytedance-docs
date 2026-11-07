---
title: "Traffic Cost"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/network-traffic"
---

When pushing or pulling container images and Helm Charts from the Container Registry, traffic costs will be incurred.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The Micro Edition offers 1GB of Outbound Public Network Traffic per month by default, with any excess charged on a Pay\-as\-you\-go basis.</div>


* <div data-tips="true" data-tips-type="warning">The Micro Edition supports both intranet and public network access by default, with no additional operation required. Intranet connectivity within the same region is enabled by default, which not only avoids consuming public network bandwidth but also effectively enhances the speed of image pushing and pulling.</div>


* <div data-tips="true" data-tips-type="warning">For the Standard Edition, manual configuration is required to enable both public and private network connectivity. For operating instructions, please refer to <a href="https://docs.byteplus.com/en/docs/cr/enable-public-network-access">Enable Public NAT for Internet Endpoint</a> and <a href="https://docs.byteplus.com/en/docs/cr/connect-vpcs-under-the-same-account">Connect to the VPC of the Current Account</a>.</div>



The specific billing rules are as follows:


|Billing item |Description |Billing method |Unit Price ||
|---|---|---|---|---|
||||**Chinese mainland** |**China (Hong Kong) and other regions** |
|Outbound Public Network Traffic Cost |The cost incurred for outbound public network traffic generated when pushing or pulling container images and Helm Charts over the public network.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When using the registry replication feature to synchronize container images and Helm Charts between image instances in different regions under the same root user, no outbound public network traffic cost will be incurred.</div><br> |Pay\-as\-you\-go billing |USD 0.0714/GB |* China (Hong Kong): USD 0.0728/GB<br><br>* Other regions: USD 0.1050/GB |
|Outbound Intranet Traffic Cost |Internal network outbound traffic cost is incurred when you Push or Pull Container images or Helm Charts via the internal network. |Free |\- |\- |
