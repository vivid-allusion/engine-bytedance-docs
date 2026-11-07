---
title: "Exporting parameter configuration"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/exporting_parameter_configuration"
---

You can export the set database parameters as a template for subsequent reuse.

<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>All resources</strong> at this step.</div>



3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click the target instance name.

5. Click **Parameters** at the top of the page.

6. In the **MySQL parameters** tab, click **Export as a template**.

7. In the pop\-up dialog box, set **Template name** and **Template description**, and click**OK**.


RDS for MySQL supports exporting the modifiable parameters of the instance's primary node and read\-only node to a TXT file in the form of "key=value" and saving it locally. This article describes the steps for exporting parameters.

<span id="procedure"></span>
## Procedure


1. Log in to [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no project is set, you should select the option <strong>Account's all resource</strong> at this step.   </div>
   

3. Click **Instance list** in the left\-side navigation bar.

4. On the **Instance list** page, click the target instance name.

5. At the top of the page, click **Parameter configuration**.

6. On the **MySQL Parameters** tab, select the node from which you want to export parameters in the upper right corner of the page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Only the parameter information of the primary node or read\-only node can be exported. If the current instance has no read\-only node, there is no need to select a node, and the parameter configuration of the primary node will be automatically exported.   </div>
   

7. Click **Export parameter**. After confirming the information in the popped\-up dialog box, click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the export is completed, the TXT file will be automatically downloaded to the local computer.   </div>
