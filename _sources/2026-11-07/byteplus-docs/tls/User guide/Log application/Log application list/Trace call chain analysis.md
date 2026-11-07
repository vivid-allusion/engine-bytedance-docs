---
title: "Trace call chain analysis"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Trace_call_chain_analysis"
---

This section introduces the Trace call chain analysis application for basic service monitoring, available in the TLS application marketplace.

<span id="8eac7c9f"></span>
## Overview

Based on the standard OpenTelemetry protocol for data ingestion, TLS enables the visualization of call chain flame graphs, intuitively presenting the distribution of latency across the chain and the relationships between service calls. This provides comprehensive lifecycle tracing, analysis, and visualization of request chains in distributed systems, delivering precise support for fault localization, performance optimization, and architecture governance.

<span id="28695403"></span>
## Monitoring chart details

The details of the Trace call chain observation and monitoring charts in TLS are as follows:


|Type |Chart |
|---|---|
|Evaluation result |Assessment result (last 90 days) |
|Trace analysis |Trace analysis (data retrieval limit: 50,000 records) |


<span id="8e001212"></span>
## Integrate a log application


1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. On the **Application Marketplace** tab, select the log application card to be integrated. For example, on the **Trace call chain analysis** card, click **Integrate application**.

5. Configure the integration parameters, then click **Integrate application**.

   
   |Parameter |Description |
   |---|---|
   |Name |Name of the integrated log application. |
   |Description |Description of the integrated log application. |
   |Region |Region of the integrated log application. |
   |Project |Select the project where the data will be stored. |
   |Report center |Select the reports to generate. For example, in this case, select **Trace call chain analysis**, then configure the following parameters:<br><br><br>* Dashboard name: Set the dashboard name corresponding to the report.<br><br>* Log topic: Select the log topic as the data source.<br><br>* Field validation:<br><br>   * The system automatically matches the corresponding index fields in the log topic based on the log application type.<br><br>   * If some fields are missing, field types differ, or statistics are not enabled, manually replace the fields.<br><br>   * Dashboard field description. For details, see [Log field description for preset dashboard](https://docs.byteplus.com/docs/tls/Description_of_preset_template_dashboard_log_fields). |
   

6. After successful integration, you will be redirected to the dashboard page by default.


<span id="2379f932"></span>
## Manage my applications

After a log application is successfully integrated, you can perform the following management operations on the integrated log applications:


1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. Go to the **My applications** tab. In the **Actions** column for the corresponding log application, the following management operations are supported:

   
   |Operation |Description |
   |---|---|
   |Access management |Click **Access management** to enter the **Access management** tab, where you can modify the name and description of the connected log application. |
   |Cancel access |Click **Cancel access**, confirm the information in the cancel access pop\-up window, and then click **Cancel access** again. |
   |View in dashboard |Click **View in dashboard** to enter the corresponding dashboard page and view related monitoring information in the dashboard. You can add charts and perform other operations. For details, see [Common dashboard actions](https://docs.byteplus.com/docs/tls/Managing_dashboards). |
