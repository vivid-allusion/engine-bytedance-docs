---
title: "Enabling or disabling public network resolution"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_or_disabling_public_network_resolution"
---

RDS for PostgreSQL supports resolving its VPC domain names as private IP addresses in the Internet environment. This topic describes how to manually enable public network resolution.

<span id=".6IOM5pmv5L-h5oGv"></span>
## **Background information**

RDS for PostgreSQL provides various protocol endpoints for your connection. When accessing endpoints of the private network VPC type, private network domain names need to be resolved, but by default, private network domain names can only be successfully resolved into private network IP addresses within the BytePlus private network environment. To resolve private network domain names in a public network environment, you can enable public network resolution for the instance. Public network resolution applies to non\-production scenarios such as testing environments, for example, direct connection to RDS for PostgreSQL instances from testing environments or personal devices accessing private network domain names.

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* After public network resolution, a private IP address is resolved into a private IP address of BytePlus. Your local environment can be connected to a BytePlus private network through VPN or other means, otherwise the access to the private IP address will fail.

* Due to the complexity of the public network environment, the accuracy and timeliness of domain name resolution cannot be guaranteed. Therefore, the public network resolution function **can only be used in non\-production environments**. It is strongly recommended to adopt a DNS Forward solution in production environments and configure forwarding to BytePlus DNS on the local DNS server to resolve internal domain names.

* DNS resolution results are cached for a while. Therefore, please do not perform local resolution within the first five minutes after public network resolution to avoid resolution failures.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click on the target instance name.

4. Click the **Connectivity** tab at the top of the page.

5. Hover over the target endpoint in the **Instance topology** section and enable or disable public network resolution in the **Private network address (ivolces.com)**  section of the floating window.

   * Enable public network resolution: Click **Enable public network resolution** and then click **OK** in the dialog box that appears.

   * Disable public network resolution: Click **Disable public network resolution** and then click **OK** in the dialog box that appears.

6. Confirm the domain name in the pop\-up dialog box and click **OK**.
