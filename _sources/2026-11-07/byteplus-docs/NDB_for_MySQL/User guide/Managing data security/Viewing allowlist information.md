---
title: "Viewing allowlist information"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Viewing_allowlist_information"
---

The allowlist list shows the detailed information of all allowlists under the main account. This article describes the steps to view the allowlist list and allowlist information.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. Click **Allowlists** in the left navigation bar to view all allowlist information under the target account.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can search for the target allowlist by <strong>Allowlist name</strong>, <strong>Allowlist ID</strong>, <strong>Description</strong>, or <strong>Security group ID</strong>, and fuzzy match is supported.   </div>
   

   
   |Column name |Description |
   |---|---|
   |**Allowlist name** |Displays the name and allowlist ID of the allowlist. Place the mouse over the allowlist name and click<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)<sub> </sub></span>icon to modify the allowlist name. |
   |**Number of IP addresses** |The number of IP addresses or IP address segments contained in the allowlist.<br><br>Click a quantity to view the included IP addresses and IP address ranges. In the pop\-up text box, click the ** Copy all** to copy all IP addresses and IP address segments. |
   |**Number of associated instances** |The number of instances associated with the allowlist. |
   |**Associated security groups** |The number of security groups associated with the allowlist.<br><br>Click the number to view the name and association mode of the associated security groups. |
   |**Description** |Description of the allowlist. Click on the allowlist description to the right<span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png)<sub> </sub></span>icon to modify the description information. |
   |**Affiliate project** |The allowlist belongs to the project. |
   |**Operation** |The allowlist list provides shortcuts to the following operations:<br><br><br>* [Associating allowlist and instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Associating_allowlist_and_instance)<br><br>* [Modifying an allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_an_allowlist)<br><br>* [Deleting an allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Deleting_an_allowlist)<br><br>* [Disassociating instance and allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Disassociating_instance_and_allowlist)<br><br>* [Copying an allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Copying_an_allowlist) |
   

4. On the **Allowlists** page, click the target allowlist name.

5. On the target allowlist information page, you can view the following information for the allowlist.

   
   |Classification |Description |
   |---|---|
   |**Allowlist information** |Displays the target allowlist name, description, IP address, and other information.  You can click **Edit** after the allowlist information to modify the allowlist information. For details, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_an_allowlist). |
   |**Associated security groups** |Displays the associated security groups for the target allowlist, including the security group name, association mode, and IP address. |
   |**List of associated instances** |Display all the instance information of the target allowlist binding, including instance name, instance ID, VPC, affiliated project and other information.<br><br>You can also click **Associate instance** in this area to associate an instance with the allowlist. Or click **Disassociate instance** to disassociate instance with allowlist. Activity details See [Associating allowlist and instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Associating_allowlist_and_instance) and [Disassociating instance and allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Disassociating_instance_and_allowlist).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After you disassociate an allowlist from an instance, users on the allowlist will no longer be able to access the instance. Please operate with caution.</div><br> |
   


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowLists) |Call the DescribeAllowLists to query all allowlist information in the specified area under the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DescribeAllowListDetail) |Call DescribeInstanceAllowLists to query the allowlist information associated with the instance. |
