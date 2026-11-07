---
title: "Disassociating an allowlist with an instance"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/disassociating_an_allowlist_from_an_instance"
---

Allowlists and instances have a many\-to\-many relationship. You can disassociate an allowlist from an instance or disassociate an instance from an allowlist. This topic describes how to disassociate an allowlist with an instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background


* Whether accessing an instance via a VPC private network or the public network, you must first configure an allowlist for the instance to ensure connectivity.

* Regularly maintain the allowlists. Remove IP addresses of devices that do not need to access the MySQL instance to ensure the security of the database connection.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* After disassociating with the allowlist, it is not able to access the instance from the IPs in the allowlist. Operate carefully.

* To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its allowlist feature to support project authentication. After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view and adjust historical allowlists under the "Global resources" project, select the "All resources" project in the top navigation bar. Use an account with the required project privileges to change the project of the historical allowlist. Refer to [Changing the project of an allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Changing_the_project_of_an_allowlist).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The instance is associated with an allowlist.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. Select the region for the instance in the upper\-left corner of the top menu bar.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the target instance name.

4. Click the **Security** tab at the top of the page.

5. Under the **Security** tab, locate the allowlist to be disassociated in the **Allowlists** subtab’s **Associated allowlists** list.

6. Click **Disassociate allowlist**. In the **Disassociate allowlist** pop\-up window, select whether to enable non\-allowlist IP session cleanup and click **OK**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If non\-allowlist IP session cleanup is enabled, disassociating the allowlist terminates all existing sessions from non\-allowlist host IPs in the instance. The sessions to be cleared are displayed in the <strong>Disassociate allowlist</strong> window. Ensure that all host IPs required by your services have been added to the allowlist to prevent abnormal services.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/RDS_for_MySQL/disassociateallowlist1) |Call the DisassociateAllowList API to disassociate the target instance from the specified IP address allowlist. |
