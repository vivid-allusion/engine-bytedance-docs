---
title: "Exporting the instance list"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/exporting_an_instance_list"
---

To facilitate offline viewing of RDS for PostgreSQL instance resources, RDS for PostgreSQL supports exporting the instance list to a file. This topic explains how to export the instance list.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

You have [created an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance), and the instance is in the **Running** status.

<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the Instances page, click the Export instances list icon in the upper\-right corner.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_abc3f64eb3604219cd40012afd46efa9.png) </span>。

4. In the Export instances list dialog box, configure the following settings and click **OK**.

   * Select the **Export scope**. You can select Export all data, Export selected data, or Export current search results.

      * **Export all data**: Exports information for all instances in the Instances list.

      * **Export selected data**: Exports information for the selected instances in the Instances list. To select this export scope, first select the target instance in the Instances list before clicking the export instances list icon.

      * **Export current search results**: Exports information for the instances included in the search results on the Instances list.

   * Select the **Fields** to export. In the pop\-up Export Summary dialog box, select the information to be exported. **Instance name/ID** is required. You may select to export information such as **State**, **Primary node availability zone**, **Private network address/port**, **Public network address/port**, **IP address**, **Virtual private cloud**, **Instance type**, **Tag**, **Primary node specifications**, **Number of nodes**, **Database engine version**, **Billing method**, **Creation time, affiliated project**, and **Endpoint address**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The exported instance information is exported as a CSV file.</div>
