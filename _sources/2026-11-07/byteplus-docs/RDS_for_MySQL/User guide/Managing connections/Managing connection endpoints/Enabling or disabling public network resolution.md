---
title: "Enabling or disabling public network resolution"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_or_disabling_public_network_resolution"
---

The VPC domain name of RDS for MySQL can be resolved to a private IP address in the internet environment. This document describes how to manually enable public network resolution.

<span id="background"></span>
## Background

RDS for MySQL provides access points for a variety of protocols that you can use for connection. When you access a VPC access point, you should resolve the private domain name. However, the private domain name must be in the private environment of BytePlus by default so that it can be successfully resolved to a private IP address. Therefore, you can enable public network resolution for an instance so that you can successfully resolve a private domain name to a private IP address even over the Internet. Public network resolution is suitable for scenarios in test environments and other non\-production environments, such as direct connections from test environments to RDS for MySQL instances, and access of personal devices to private domain names.

<span id="precautions"></span>
## Precautions


* A BytePlus private IP address is obtained through the public network resolution of a private domain name. Your local environment should support BytePlus private network through VPN or other means, otherwise you cannot successfully access the private IP address.

* Due to the complexity of the internet environment, the accuracy and timeliness of domain name resolution cannot be ensured. Therefore, the internet DNS resolution function **only applies to non\-production environments**. The DNS Forward solution is strongly recommended for the production environment. You can configure Forward to BytePlus DNS in the local DNS Server to implement private domain name resolution.


<span id="prerequisites"></span>
## Prerequisites

The instance has been created and is in the **Running** status.For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>All resources</strong> at this step.</div>



3. In the left navigation bar, choose **MySQL** \> **Instances**.

4. On the **Instances** page, click the target instance name.

5. Click the **Connectivity** tab at the top of the page.

6. Click **Edit** on the target endpoint card in the **Endpoints** area to go to the **Modify endpoint** page.

7. Enable or disable public network resolution in the **Private network address (ibytepluses.com)**  area on the **Modify endpoint** page.

   * If public network resolution is not enabled, you can click **Enable public network resolution** and confirm the domain name involved in this operation in the pop\-up dialog box, and then click **Are you sure to enable**.

   * If public network resolution is enabled, you can click **Disable public network resolution** and confirm the domain name involved in this operation in the pop\-up dialog box, and then click **Confirm to disable**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="tip">After performing the operation, the instance status changes to <strong>Network changing</strong>. After the operation is completed, the instance status changes to <strong>Running</strong>.</div>


<span id="related-apis"></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBEndpointDNS](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifydbendpointdns) |Call the ModifyDBEndpointDNS interface to modify the resolution method of the private network address. |
