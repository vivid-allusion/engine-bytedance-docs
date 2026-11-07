---
title: "View monitoring dashboard (K8s YAML)"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/View_monitoring_dashboard_K8s_YAML"
---

K8s YAML\-based applications provide instance\-level monitoring metrics to help you monitor the operational status of your applications in real time. View the monitoring dashboard for K8s YAML applications

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The K8s YAML application has been created and deployed. The application must be deployed in a Container Service VKE cluster. For detailed instructions, refer to [K8s YAML application deployment](https://docs.byteplus.com/en/docs/cp/K8s_YAML_application_deployment).

* Container service monitoring has already been turned on for the VKE cluster pending deployment. For specific actions, see [Container Service Monitoring](https://docs.byteplus.com/en/docs/vke/VKE-observability).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the application management page.

   1. Log in to the [Code Pipeline Console](https://console.byteplus.com/cp).

   2. Select **workspace** in the left navigation bar.

   3. Click the target workspace name to enter that workspace.

   4. In the left navigation bar, select **Application Delivery \> Application Management**.

2. On the application management page, select the target K8s YAML application, click the application card, and go to the current application's **Basic Information** tab.

3. Switch to the **environment** tab, click the target environment card, and access the selected environment.

4. Switch to the **Monitoring dashboard** tab, select the target instance and monitoring time range to view its monitoring dashboard.
