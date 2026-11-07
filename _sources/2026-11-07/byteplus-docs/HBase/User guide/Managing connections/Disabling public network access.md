---
title: "Disabling public network access"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Disabling_public_network_access"
---

When devices outside the VPC no longer need to access the HBase instance, we recommend that you promptly disable public network access. This article describes how to disable public network access.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Public network access is enabled for the instance. To learn how to enable public network access, see [Enabling public network access](https://docs.byteplus.com/en/docs/HBase/Enabling_public_network_access).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

To ensure database security, we recommend promptly deleting the IP addresses of related client devices from the IP allowlist after you disable public network access. To modify allowlist IP addresses, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Configuring_an_Allowlist).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Connectivity**.

5. On the **Connectivity** tab, in the **Public network access** area, click **Disable public network access**.

6. In the dialog box that appears, confirm the public access address to be disabled and the EIP to be unbound, then click **OK**.

   <div data-tips="true" data-tips-type="danger" data-tips-is-title="true" data-wrapper-indent="1">danger   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">After disabling public network access, the corresponding public network access address will be deleted, and the client will not be able to access the HBase instance through the original public network address. Please confirm that your business does not use public network addresses to avoid losses.   </div>
   

   * <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">After public network access is disabled, the associated EIP is automatically unbound. The unbound EIP will be retained and continue to incur charges. If no longer needed, release the relevant resources manually. To learn how to release an EIP, see <a href="https://docs.byteplus.com/en/docs/eip/Releasing-an-EIP">Releasing an EIP</a>.   </div>
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DeleteDBEndpoint](https://docs.byteplus.com/en/docs/HBase/DeleteDBEndpoint) |Call the DeleteDBEndpoint interface to close public network access to the specified connection address. |
