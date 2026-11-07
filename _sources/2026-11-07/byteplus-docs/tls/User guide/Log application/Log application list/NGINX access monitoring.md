---
title: "NGINX access monitoring"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/NGINX_access_monitoring"
---

This section introduces the NGINX access monitoring log application provided by the TLS application marketplace.

<span id="8eac7c9f"></span>
## Overview

Built on Nginx, the log observability capability supports Nginx access analysis and operational monitoring.


* Nginx access dashboard: Statistically analyzes the access behavior of Nginx end users, including metrics such as PV, UV, and request geographic distribution.

* Nginx monitoring dashboard: Statistically analyzes the current operational status of Nginx, including request success rate, request status code distribution, request latency, and more.


<span id="fb554018"></span>
## Monitoring chart details

The chart details for Nginx access monitoring in TLS are as follows:


|Type |Chart |
|---|---|
|Nginx access dashboard |* PV month\-over\-month, PV week\-over\-week, UV month\-over\-month, UV week\-over\-week<br><br>* PV province distribution, PV country distribution, UV province distribution, UV country distribution<br><br>* PV trend over the past day, UV trend over the past day, PV trend over the past 7 days, UV trend over the past 7 days<br><br>* Top 10 access provinces, Top 10 access cities, Top 10 UserAgents by access, Top 10 Hosts by access<br><br>* Mobile access ratio, Android/iOS ratio, Top URL, Top access IP |
|Nginx monitoring dashboard |* PV, UV, outbound traffic, inbound traffic<br><br>* Request type distribution, request status code distribution, request count distribution, PV & UV 15\-minute granularity<br><br>* Request success rate, request failure rate, 404 ratio, 4xx ratio, 5xx ratio<br><br>* Request latency, average latency, P95 latency, P99 latency, P9999 latency<br><br>* TOP 10 service request count, TOP 10 service request failure rate, TOP 10 service request average latency, TOP 10 service request traffic<br><br>* TOP request URL, TOP request service |


<span id="338f5c9c"></span>
## Integrate log applications


1. Log in to [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. On the **Application marketplace** tab, select the log application card to be integrated. For example, on the **Nginx access monitoring** card, click **Integrate application**.

5. Configure the application integration parameters, and then click **Integrate application**.

   
   |Parameters |Description |
   |---|---|
   |Log application name |Name of the log application to be integrated. |
   |Description |Description of the log application to be integrated. |
   |Region |Region of the log application to be integrated. |
   |Log project |Select the log project for storing data. |
   |Report center |Select the reports to generate. For example, select **Nginx access dashboard**, then configure the following parameters:<br><br><br>* Dashboard name: Set the dashboard name for the report.<br><br>* Log topic: Select the log topic as the data source.<br><br>* Field validation:<br><br>   * The system automatically matches the corresponding index fields in the log topic based on the log application type.<br><br>   * If some fields are missing, field types differ, or statistics are not enabled, manually replace the fields.<br><br>   * For dashboard field descriptions, see [Log field description for preset dashboard](https://docs.byteplus.com/docs/tls/Description_of_preset_template_dashboard_log_fields). |
   

6. After successful integration, you are redirected to the dashboard page by default.


<span id="82f21dcd"></span>
## Manage my applications

After successfully integrating a log application, you can manage the integrated log applications.


1. Log in to [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. Go to the **My applications** tab. In the **Actions** column for the corresponding log application, you can perform the following management operations:

   
   |Actions |Description |
   |---|---|
   |Integration management |Click **Integration management** to enter the **Integration management** tab, where you can modify the name and description of the log application to be integrated. |
   |Cancel integration |Click **Cancel integration**, confirm the details in the cancel integration popup, and then click **Cancel integration** again. |
   |View in dashboard |Click **View in dashboard** to enter the corresponding dashboard page and view relevant monitoring information on the dashboard. You can add charts and perform other operations. For details, see [Common dashboard actions](https://docs.byteplus.com/docs/tls/Managing_dashboards). |
