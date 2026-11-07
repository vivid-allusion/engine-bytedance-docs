---
title: "Viewing blue-green instance differences"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Viewing_blue-green_instance_differences"
---

After you create a blue\-green deployment for an instance, you can view the differences between the blue and green instances. This allows you to fully understand the differences, assess risks, and adjust business logic before a switchover. This topic describes how to view the differences between blue and green instances.

<span id="edJszfbD"></span>
## Prerequisites

A blue\-green deployment has been created. For more information, refer to [Create a blue-green deployment](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_a_blue-green_deployment).

<span id="F9cHlPqO"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

   3. In the left navigation bar, click **Instances** to view the list of RDS for MySQL instances.

4. On the **Instances** page, click the name of the target blue or green instance to open the **Summary** tab.

5. On the **Connectivity** tab, in the **Instance topology** section, select **View blue\-green differences** from the **Actions** dropdown menu on the **green instance** card.

6. The blue\-green differences page displays the compatible version, kernel minor version, proxy information, specifications, storage, instance type, allowlists, endpoint information, and parameter information for the blue and green instances.

   * Hover over the endpoint name of the blue or green instance to view the endpoint type, ID, public network IP, public network domain, port, private network IP, private network domain, private network address port, read/write mode, and read/write separation status of the connection endpoint on the pop\-up card.

   * Click the **View differences** button in the parameter information row for the blue or green instance to view the different parameters and all parameters for both instances on the **Parameter comparison** page that appears. Under the **Differences** and **All items** tabs, click the download button in the upper\-right corner to download the different or all parameters and their running values for both instances.


<span id="SP470yID"></span>
## Related API


|API |Description |
|---|---|
|[DescribeDBBlueGreenDifferences](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DescribeDBBlueGreenDifferences) |Call the DescribeDBBlueGreenDifferences API to query the differences between the blue and green instances in a blue\-green deployment. |
