---
title: "Viewing the details of an instance"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_the_details_of_an_instance"
---

This topic introduces the procedure to view detailed information of an RDS for PostgreSQL instance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

On the **Summary** tab, you can view the instance’s **Summary**, **Configuration**, **Usage statistics**, and **Billing method**.


|Category |Details |
|---|---|
|Summary |Summary includes the instance ID, instance name, network information (VPC and subnet), instance type, storage type, availability zones, affiliated project, and tags. |
|Configuration |Configuration includes the database version, primary node specifications, number of nodes, CPU cores, memory, disk size, data synchronization method, and WAL backup policy.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the WAL backup policy is not configured, you can click <strong>Go to configure</strong> to configure it. For more information, refer to Configuring local remaining space protection. For more details, please refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/configuring_local_remaining_space_protection">setting local remaining available space protection</a>.</div><br> |
|Usage statistics |Disk Usage is the overall storage space usage of the instance and also shows the usage of data files, temporary files, WAL files and log files. |
|Billing information |Billing information includes billing method, creation time, and enable automatic renewal (displayed when the instance billing method is Subscription). |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong> for this operation.   </div>
   

3. In the **Instances**, click the name of the target instance to enter the **Summary** tab and view detailed information about the instance.
