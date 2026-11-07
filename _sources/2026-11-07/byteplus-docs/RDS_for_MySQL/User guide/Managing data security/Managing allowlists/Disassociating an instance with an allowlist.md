---
title: "Disassociating an instance with an allowlist"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/disassociating_an_instance_from_an_allowlist"
---

Allowlists and instances have a many\-to\-many relationship. You can disassociate an allowlist from an instance or disassociate an instance from an allowlist. This topic describes how to disassociate an instance from an allowlist.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* the allowlist has associated instances.

* The instance to be disassociated from the allowlist must be in a **Running** state.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After disassociating with the allowlist, it is not able to access the instance from the IPs in the allowlist. Operate carefully.

* To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its allowlist feature to support project authentication. After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view the allowlists in the "Global resources" project, you must select "All resources" in the top navigation bar.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click **Allowlists** on the left navigation bar.

4. On the **Allowlists** page, click  **...**  \> **Disassociate instance** in the **Actions** column for the target allowlist. in the pop\-up page, you can see the list of instances associated with the allowlist.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Alternatively, click the name of the target allowlist to go to the <strong>Allowlist details</strong> page. On the <strong>Allowlist details</strong> page, click the <strong>Disassociate instance</strong> button to go to the <strong>Disassociate instance</strong> page.   </div>
   

5. In the **Associated instances** list, click **Disassociate instance** to disassociate the corresponding instance from the allowlist.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Alternatively, you can select multiple instances in the list, and then click <strong>Disassociate instance</strong> at the bottom right of the list to disassociate them from the allowlist.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/disassociateallowlist1) |Call the DisassociateAllowList API to disassociate the target instance from the specified IP address allowlist. |
