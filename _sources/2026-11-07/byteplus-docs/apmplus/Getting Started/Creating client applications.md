---
title: "Creating client applications"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Create_a_client_application"
---

After a client application is integrated, you can monitor and observe the metrics of the application, such as health status and crash information in the APM console. This topic describes how to integrate an application with the RUM console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. Prepare an account.

   Before activating the service, you need to create a  account and complete either enterprise or individual authentication.

   * Create a  account. 

   * Complete enterprise authentication. 

   * Complete individual authentication. 

2. Top up your account.

3. Create a project to achieve logical resource isolation. This facilitates project\-based authorization and bill splitting.


<span id=".5Yib5bu65bqU55So"></span>
## Create an application


1. Log in to the [RUM console](https://console.byteplus.com/observe/apmplus-client).

2. In the top navigation bar, select the target region.

3. Click **Create app monitoring**.

4. Configure the application‑related information, read **I have read and agree to Application Performance Management Plus terms of service**, check the box to agree, and then click **Confirm**.

   
   |**Parameter** |**Description** |
   |---|---|
   |Chinese app name |Specify a custom Chinese name for the application to identify the application. |
   |English app name |Specify a custom English name. |
   |Upload icon |Click **Change image** to select an image from a local file to identify the application. |
   |Select the services you need |Select the client service to be activated and configure the related service information.<br><br><br>* **Project**: The project to which the service belongs. Project management is a resource management mechanism that  provides to enable grouping of cloud resources by project. Project\-based authorization with Identity and Access Management (IAM) facilitates resource isolation and data security, as well as cost calculation across cloud resources. <br><br>* **Payment**: When you activate the RUM service, the pay\-as\-you\-go billing method is used by default. You can purchase a package after the service is activated.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When you create a client application, activate at least one client service.</div><br> |
   

5. After the application is created, click the application to view its AppID and AppToken, which are used for subsequent SDK integration.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you find that services such as App Monitoring, WebPro Monitoring, or PC Monitoring are not displayed on the details page of the application, it means your current account does not have read and write permissions on the relevant services of this application. The root user (super administrator of the APMPlus platform) needs to grant the read and write permissions on the application and service to the IAM user. For details, see <a href="https://docs.byteplus.com/en/docs/apmplus/Permission_management_client">Permission management</a>.   </div>
