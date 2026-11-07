---
title: "Enabling RUM"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Activate_client_monitoring"
---

After enabling RUM, you can integrate the SDK and then view the monitoring data of applications in the console.

<span id="nW9XIxl2"></span>
## Prerequisites


* You have created a  root user and completed real\-name authentication. 

* Permissions have been granted to IAM users. For details, see [Managing client permissions](https://docs.byteplus.com/en/docs/apmplus/Permission_management_client).


<span id=".5byA6YCa5pyN5Yqh"></span>
## Procedure


1. Log in to the [RUM console](https://console.byteplus.com/observe/apmplus-client).

2. In the top navigation bar, select the target region.

3. Click the name of the target application to go to the application service management page. Click **Activate service** and select the service that you want to activate.

4. Configure the service‑related information, read **Terms of APMPlus Products and Services**, check the box to agree, and click **Confirm** to complete the activation.



|**Parameter** |**Description** |
|---|---|
|Service |Select the client\-side services to be activated based on your business requirements. |
|Project |The project to which the service belongs. Project management is a resource management mechanism that  provides to enable grouping of cloud resources by project. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources.  |
|Payment method |When you activate the client\-side services, the pay\-as\-you\-go billing method is used by default. You can purchase packages after the service is activated.<br><br><br>* **Pay\-as\-you\-go**: This is a postpaid method. When you use the pay\-as\-you\-go billing method, fees are calculated per hour at a fixed unit price. At the start of each hour, the system calculates the event consumption for the previous hour, generates a bill, and automatically deducts the amount from your account. Make sure that your account balance is sufficient. <br><br>* **Package**: This is a prepaid method. You need to pay in advance based on the specifications and quantity of the package. |


<span id="LTc0BdyP"></span>
## What to do next

You can perform the following operations after enabling the RUM service:


* ①: For a RUM service purchased with packages, you can configure an automatic switch to the pay‑as‑you‑go billing method after packages are exhausted or expire. 

* ②: View the event usage of the monitoring service. Event usage is related to billing. You can adjust the event sampling rate in the SDK reporting configuration based on event usage trends. For a detailed description, see [Event usage](https://docs.byteplus.com/en/docs/apmplus/Event_usage_app) and [SDK reporting configuration](https://docs.byteplus.com/en/docs/apmplus/SDK_reporting_configuration).

* ③: View package specifications, order time, and expiration time.

* ④: You can view detailed SDK integration documentation. After the SDK is integrated, you can check the data reporting. Normally, "Submitted successfully" will be returned.

* ⑤: Control application data reporting. You can disable and enable this feature. If you no longer use APMPlus, you can turn off the Data Reporting switch. After the service is disabled, APMPlus will no longer incur fees.

* ⑥: If you have not activated the shared package service within the root user and need to purchase additional packages, you can renew the purchased package before it is exhausted or expires. If you have already enabled the shared package service within the root user and need to purchase additional packages, click **Purchase shared resource package** as shown in the following figure, and the root user will purchase packages in a centralized manner. For details about shared packages within root users, see [Rules and authorization statements for activating shared package services within primary accounts](https://docs.byteplus.com/en/docs/apmplus/Rules_and_authorization_statement_for_the_activation_of_the_root_user_shared_package_service).

* ⑦: Go to the monitoring details page to view the information, such as application health status and crash information.
