---
title: "Merging allowlists"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/unifying_allowlists"
---

This topic describes the procedure for merging allowlists from multiple instances into a single allowlist.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Merge to generate an allowlist is a feature provided by rds for postgresql that merges allowlists from multiple instances into a new allowlist. This feature removes duplicates and merges multiple allowlists from different instances to create a new allowlist.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The merge to generate an allowlist feature only creates a new allowlist and does not replace the allowlist currently associated with the instance. To replace it, use the disassociate and associate with an allowlist features yourself. For more information about associating and disassociating allowlists, refer to [Associate with an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/associating_an_allowlist) and [Disassociate with an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/disassociating_an_allowlist).

* When merging to generate an allowlist, scattered IPs will not be merged into IP address segments.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage restrictions


* Supports merging up to 300 instances' allowlists.

* The merged allowlist can contain up to 300 IP addresses or IP address segments. Before merging, Please confirm that the IP addresses or IP address segments in the allowlists to be merged do not exceed the quantity limit.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, select the instances to merge into an allowlist, and click **merge to generate an allowlist** at the bottom left of the page.

5. In the popped\-up **merge to generate an allowlist** window, set the **name** and **description** of the merged allowlist, then click **OK**.

   
   |Parameters |Note |
   |---|---|
   |Allowlist name |Required The naming convention for allowlist names is as follows:<br><br><br>* Within the current region, the allowlist name is unique.<br><br>* Begin with Chinese, a letter, or an underscore (_).<br><br>* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).<br><br>* The name length is limited to 1~128 characters. |
   |Description |Optional. The description information can be used to search for the allowlist in the allowlist list, and the length of the description should not exceed 200 characters. |
   


<span id=".5ZCO57ut5q2l6aqk"></span>
## Next steps

[Associating with an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/associating_an_allowlist)

<span id=".55u45YWzIEFQSQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[UnifyNewAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/unifynewallowlist) |Call UnifyNewAllowList API to merge some allowlists of multiple instances into a new allowlist. |
