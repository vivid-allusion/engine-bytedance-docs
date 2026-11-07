---
title: "Synchronizing an allowlist"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/synchronizing_allowlists"
---

This topic describes the steps to manually synchronize allowlists.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

If the status of the instance associated with an allowlist is **Running**, the modified content of the allowlist will be immediately synchronized to the instance. If the status of the instance associated with the allowlist does not meet this condition, the system automatically performs synchronization when the condition is met. You can also perform a manual synchronization.

<span id=".5pON5L2c5q2l6aqk"></span>
## Precautions

To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its allowlist feature to support project authentication. After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view the allowlists in the "Global resources" project, you must select "All resources" in the top navigation bar.

<span id="iGZRLAUo"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click **Allowlists** on the left navigation bar.

4. On the **Allowlists** page, click the **Name** of the target allowlist to go to the **Allowlist details** page.

5. In the **List of associated instances** area on the **Allowlist information** page, click **Synchronize allowlist** in the actions column of the target instance to complete the synchronization.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the allowlist has been synchronized to the instance, the Synchronize allowlist button will be grayed out and cannot be operated.   </div>
