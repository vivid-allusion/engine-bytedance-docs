---
title: "Increasing instance quotas"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/increase-instance-quota"
---

If the standard quota in your current instance does not meet your business requirements, you may apply for quota scale\-out. The scaled\-out portion will incur corresponding charges.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Currently, only the following resources support increasing quotas.


|Billing item |Description |Documentation |
|---|---|---|
|Namespace Quota |The cost incurred when using namespaces that exceed the sandard quota. |[Namespace Quota](https://docs.byteplus.com/en/docs/cr/namespace-quota) |
|OCI artifact repository quota |The cost incurred when using OCI artifact repositories that exceed the standard quota. |[OCI artifact repository quota](https://docs.byteplus.com/en/docs/cr/repository-quota) |
|VPC access quota |The cost incurred when using VPC accesses that exceed the standard quota. |[VPC access quota](https://docs.byteplus.com/en/docs/cr/vpc-quota) |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* Only **Standard Edition instances** support quota scale\-out.

* Once the quota scale\-out is completed, **scale\-in is not supported**.

* Only the scaled\-out quota is charged; the standard quota is free of charge. For standard quota details, see [Limits](https://docs.byteplus.com/en/docs/cr/limits).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the[ CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the target instance area, click **Enter instance** to enter the instance overview page.

4. In the **Quota usage** section on the overview page, click **Quota increase**.

5. On the instance configuration modification page, increase the quota as prompted.

6. Click **Confirm order** to complete the quota increase.
