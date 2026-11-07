---
title: "Applying parameter template"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Applying_a_parameter_template"
---

RDS for PostgreSQL supports batch and templated setting of instance parameters through application parameter templates. This paper introduces the operation process of the application parameter template.

<span id="bGi3rjce"></span>
## Precautions

If the parameter template that needs to be applied contains parameters that need to be restarted, the instance will be restarted after applying the parameter template. If the parameter template that needs to be applied contains parameters that need to be restarted, the instance will be restarted after applying the parameter template. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database connection disconnection on the business.

<span id="ikwSMPGK"></span>
## Prerequisites


* Already created an instance, and the instance is **Running**. For more information about creating an instance, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

* A parameter template has been created, and the database engine version of the parameter template matches the database version of the parameter template instance to be applied. For more information about creating a parameter template, see [Creating a parameter template](https://docs.byteplus.com/en/docs/RDS_for_PG/Creating_a_parameter_template).


<span id="YZvlhtdf"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Click on **Instances** in the left navigation bar.

4. On the **Instances** page, click on the target instance name.

5. At the top of the page, click **Parametes**.

6. On the **PostgreSQL parameter** tab, click **Apply parameter template**.

7. In the pop\-up **Select parameter template** window, select the parameter template to be applied by the template name, and confirm the parameter changes and effects of applying the parameter template to the instance, click **OK**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Only parameter templates that match the database engine version of the instance are listed.   </div>
   

<span id="FX3EyTuO"></span>
##
