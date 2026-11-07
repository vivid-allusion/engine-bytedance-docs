---
title: "Add an API gateway"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Add_an_API_gateway"
---

Add an API gateway to the application to enable other applications to access the current application via public or private domain names. This article explains how to add an API gateway.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A managed application has been created and deployed, and it must be deployed on a Container Service VKE cluster. For detailed steps, see [Create a managed application](https://docs.byteplus.com/en/docs/cp/Managed_applications_K8s).

* API Gateway has been created. For detailed instructions, see [Create an instance](https://docs.byteplus.com/en/docs/apig/Creating_an_instance).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the application management page.

   1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the name of the target workspace to enter that workspace.

   4. Select **Application Delivery \> Application Management** in the left navigation bar.

2. On the application management page, select the target hosted application, click the application card, and go to the Basic Information tab for the current application.

3. Switch to the application orchestration tab. In the access method settings section, select **API Gateway \> Add API Gateway**.

4. In the Add API Gateway dialog box, set the relevant parameters.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Api gateway instances |Select an API gateway instance. |
   |Port |Enter the actual service port of your application. Caution: Ensure that the port number matches your program's listening port. |
   

5. Click **OK** to start configuring the API gateway.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result validation


1. View the service domain name of the API Gateway in the table.

2. On a machine with access to the public or private network, enter the corresponding service domain name in the browser address bar to access the application homepage.
