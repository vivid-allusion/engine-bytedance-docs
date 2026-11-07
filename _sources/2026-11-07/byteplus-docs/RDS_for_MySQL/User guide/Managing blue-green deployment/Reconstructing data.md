---
title: "Reconstructing data "
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Reconstructing_data_"
---

This topic describes the information about data reconstruction for a green instance in a blue\-green deployment.

<span id="c92L55GY"></span>
## Background

After a blue\-green deployment is created for an instance, if the Read/Write mode was enabled for the green instance (the "Global read\-only" feature was disabled) due to business requirements, or if the latency between the green instance and the blue instance becomes too high, you must reconstruct the data for the green instance before performing a blue\-green switch to ensure data synchronization.

<span id="4Zoc166x"></span>
## Prerequisites

The green instance has been created and is in the **Running** state. For details, refer to [Creating blue-green deployment](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_a_blue-green_deployment).

<span id="MwPttaZe"></span>
## Precautions

If the green instance is in Read/Write mode, it is switched to the Global read\-only mode after data reconstruction.

<span id="QD86pYMY"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. In the left navigation bar, click **Instances** to view the list of RDS for MySQL instances.

4. On the **Instances** page, click the name of the target blue instance or green instance to go to the **Summary** tab.

5. Click the **Connectivity** tab, and in the **Instance topology** area, on the **Green instance** card, click **Data rebuilding** from the **Actions** drop\-down menu. In the dialog box that appears, read and select the risk warning, and then click **OK**.


<span id="wL3Lby7I"></span>
## Related API


|API |Description |
|---|---|
|[RebuildDBGreenInstance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/RebuildDBGreenInstance) |Call the RebuildDBGreenInstance API to rebuild the green instance in a blue\-green deployment. |
