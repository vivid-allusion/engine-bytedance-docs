---
title: "Applying parameter template in a batch"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Appling_a_parameter_template_in_batch"
---

RDS for PostgreSQL supports applying the same parameter template to batch instances, so that the parameters of batch instances can be set uniformly. This topic introduces the parameter process of applying parameter template to batch instance.

<span id="UG1U6Ktr"></span>
## Precautions


* If the parameter template that needs to be applied contains parameters that need to be restarted, the instance will be restarted after applying the parameter template. If the parameter template that needs to be applied contains parameters that need to be restarted, the instance will be restarted after applying the parameter template. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database connection disconnection on the business.

* Batch application parameter template operations are supported only for instances with the same database version.

* In a batch application parameter template operation, up to 20 instances can be selected.


<span id="wVfTD97N"></span>
## Prerequisites


* A parameter template has been created, and the database engine version of the parameter template matches the database version of the parameter template instance to be applied. For more information about creating a parameter template, see [Creating a parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Creating_a_parameter_template).

* Instances that need to apply parameter templates are all in **Running** state.


<span id="32iiDzOT"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, check one or more instances that need to apply the same parameter template.

5. Click the **Apply parameter template** below the **Instance** list.

6. In the pop\-up **Apply parameter template in batch \- Select templates** page, after confirming the selected instance and selecting the parameter template to apply, click **Next**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only parameter templates that match the database engine version of the instance are listed.   </div>
   

7. In the pop\-up **Apply parameter template in batch \- Confirm to apply** page, after confirming the selected instance and selecting the parameter template to apply, click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the selected parameter template contains parameters that require an instance restart to take effect, after clicking <strong>OK</strong>, a dialog box will pop up again prompting the impact of applying the parameter template to the instance \- instance restart. If you are sure that this impact is acceptable, click <strong>OK</strong> in the dialog box to complete the batch instance application parameter template.   </div>
