---
title: "Associating with an allowlist"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/associating_an_allowlist"
---

This topic describes the procedure of associating with an allowlist.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Allowlists and instances have a many\-to\-many relationship. By quantity limits, each allowlist can be associated with up to 1000 instances, and each instance can be associated with up to 100 allowlists. By association relationships, you can associate an allowlist from an instance or associate an instance from an allowlist.

RDS for PostgreSQL provides two association entry points, allowing you to choose freely based on your business scenarios.


* [Associating allowlists from an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/associating_an_allowlist#.5LuO5a6e5L6L57uR5a6a55m95ZCN5Y2V): operate inside an instance to associate multiple allowlists for one instance in one operation.

* [Associating instances from an allowlist](https://docs.byteplus.com/en/docs/RDS_for_PG/associating_an_allowlist#.5LuO55m95ZCN5Y2V57uR5a6a5a6e5L6L): operate inside an allowlist to associate one allowlist to multiple instances in one operation.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage restrictions


* Each allowlist can be associated with up to 1,000 instances.

* Each instance can associate up to 100 allowlists.

* The total number of IP addresses or IP address segments in all allowlists associated to each instance cannot exceed 300. When there are many IP addresses, it is recommended to merge scattered IP addresses into IP address segments.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5LuO55m95ZCN5Y2V57uR5a6a5a6e5L6L"></span>
### Associating instances to allowlists


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click **Allowlists** on the left navigation bar.

4. Click **Associate with an allowlist** in the **Actions** column of the target allowlist to open the **Associate instances** page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can search for the target instance by Instance name or Instance ID at the top right of the instances list.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can associate up to 50 instances with an allowlist at a time.   </div>
   

5. On the **Associate instances** page, select the target instances in the instances list and click **OK** to complete the association.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can search for the target instance by Instance name or Instance ID at the top right of the instances list.   </div>
   

<span id=".5LuO5a6e5L6L57uR5a6a55m95ZCN5Y2V"></span>
### Disassociating an instance with an allowlist


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. On the **Data Security** tab, under the **Allowlists** subtab, click **Associate with an allowlist** to enter the **Associate with an allowlist** page. On this page, you can associate with an allowlist by choosing either **Existing allowlist** or **New allowlist**. The rules for each are as follows:

   * **Associate with an existing allowlist** a. On the **Associate with an allowlist** page, click **Existing allowlist** to go to the **Existing allowlist** list.  b. On the **Existing allowlist** list, select the allowlist to associate with the current instance, and then click **OK**. The successfully associated allowlist appears in the **Associated allowlists list**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In the upper\-right corner of the allowlist list, you can search for the target allowlist by allowlist name, allowlist ID, or description.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can associate up to 100 allowlists with one instance each time.      </div>
      

   * **Associate new allowlist** a. On the **Associate with an allowlist** page, click **New allowlist** to enter the **create an allowlist** page.  b. On the **Create an allowlist** page, add **Allowlist name**, **Description**, and **IP address**, then click **OK**.

      
      |Parameter |Note |
      |---|---|
      |Allowlist name |Required The naming convention for allowlist names is as follows:<br><br><br>* Within the current region, the allowlist name is unique.<br><br>* Begin with Chinese, a letter, or an underscore (_).<br><br>* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).<br><br>* The name length is limited to 1~128 characters. |
      |Description |Optional. The description information can be used to search for the allowlist in the allowlist list, and the length of the description should not exceed 200 characters. |
      |IP address |Required. Only IP addresses added to the allowlist can access the instance. Supports pasting IP addresses or IP address segments, separated by Chinese and English commas, spaces or newlines. |
      


&nbsp;

<span id=".55u45YWzIEFQSQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[AssociateAllowList](https://docs.byteplus.com/en/docs/RDS_for_PG/associateallowlist) |Call AssociateAllowList API to associates an allowlist. |


&nbsp;
