---
title: "View the monitoring dashboard"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/View_the_monitoring_dashboard"
---

Managed applications provide instance\-level monitoring metrics so you can monitor the application's operational status in real time. This article introduces how to view the monitoring dashboard for hosted applications.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The managed application has been created and deployed, and the application must be deployed on a Container Service VKE cluster. For detailed instructions, see [Create managed application](https://docs.byteplus.com/en/docs/cp/Managed_applications_K8s).

* Container service monitoring has already been turned on for the VKE cluster pending deployment. For specific actions, see [Container service monitoring](https://docs.byteplus.com/en/docs/vke/VKE-observability).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the application management page.

   1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp).

   2. In the left navigation bar, select **workspace**.

   3. Click the name of the target workspace to enter it.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

2. On the application management page, select the target hosted application, click the application card, and enter the current application's **Basic Information** tab.

3. Switch to the **Monitoring Dashboard** tab, select the target instance and monitoring time range, and view the dashboard for the selected instance.
