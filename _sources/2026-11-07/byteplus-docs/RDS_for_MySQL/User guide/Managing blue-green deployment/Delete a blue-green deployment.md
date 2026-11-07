---
title: "Delete a blue-green deployment"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Delete_a_blue-green_deployment"
---

This topic describes how to delete a blue\-green deployment.

<span id="hJSpTiph"></span>
## Precautions


* After you delete a blue\-green deployment, the synchronization and association between the blue and green instances are removed. Each instance retains its existing configuration and is converted to a regular instance.

* The green instance remains in a read\-only state, which you can adjust.


<span id="aM2HcrkR"></span>
## Prerequisites

A blue\-green deployment has been created for the target instance.

<span id="wnVAm22W"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

4. In the left navigation bar, click **Instances** to view the list of RDS for MySQL instances.

5. In **Instances,**  click the name of the target blue or green instance to go to the **Summary** tab.

6. Click the **Connectivity** tab, and in the **Instance topology** section, click the **Delete blue\-green deployment** button from the **Actions** drop\-down menu on the **green instance** card. In the pop\-up **Confirm deleting the blue\-green deployment?**  dialog box, click **OK** to delete the blue\-green deployment for the target instance.


<span id="MqkVHJZk"></span>
## Related API


|API |Description |
|---|---|
|[DeleteDBBlueGreenRelation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/DeleteDBBlueGreenRelation) |Call the DeleteDBBlueGreenRelation API to delete the blue\-green deployment. |
