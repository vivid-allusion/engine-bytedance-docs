---
title: "Manage applications"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Manage_applications"
---

This topic introduces how to manage applications through the Serverless Application Center, including creating applications, viewing application logs, and deleting applications.

<span id="create-application"></span>
## Create application

The Application Center provides a variety of application templates to help simplify the process of creating applications and creates all associated cloud resources with one click.


1. Log in to the [FaaS console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. In the left navigation bar, select **Application**.

4. On the application page, click **Create application**.

5. On the create application page, select the required application template, hover the mouse over the template card, and click **Create**.

6. Configure the application's parameters as required, and after configuration is complete, click **Confirm** to start creating and deploying the application.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The configuration items vary for different applications; please refer to the respective deployment documentation for specific details.</div>


<span id="view-applications"></span>
## View applications

In the application center, you can view all applications created under the current account, including details and logs for each application.


* **View application Log**

   In the application list on the application page, select the target application, click on the **Log** in the actions column, to quickly view the real\-time deployment log of the current application.

* **View application Details**

   On the application page, click on the target application name in the application list to enter the details page of the current application. You can view the logs, basic information, and all associated cloud resource information of the application.

* **View cloud resources associated with the application**

   1. On the application page, click on the target application name in the application list to enter the details page of the current application.

   2. In the list of cloud resources, click `+` next to the name of the Cloud Service, to view the specific cloud resources under the current Cloud Service.

      For example: click `+` next to the FaaS, to view the associated function names and their operating status. Click the function name to jump to the function details page.


<span id="delete-application"></span>
## Delete Application

Supports one\-click deletion of the Application and all associated resources under it.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">When deleting an Application, all cloud resources associated with it will be deleted as well. If some resources are used in other contexts, please be cautious about deleting them.</div>



1. In the Application list on the Application page, select the target Application, click **Delete** in the actions column.

2. In the pop\-up confirmation box, carefully confirm whether all cloud resources associated with the Application can be deleted.

3. After confirming, check the risk warning box, then click **Delete**.
