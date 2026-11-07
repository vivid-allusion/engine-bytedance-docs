---
title: "VeADK observability"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/VeADK_observability"
---

This section introduces the VeADK Observability application for large model observability, available in the TLS application marketplace.

<span id="d4eb68d4"></span>
## Overview

When using the VeADK agent development framework, TLS can be used to record key paths and intermediate states during Agent execution, enabling observability of the Agent execution chain. This helps developers with debugging, performance analysis, behavior tracking, and other tasks.

<span id="9f6bec90"></span>
## Monitoring chart details

The monitoring chart details for the VeADK Observability application in TLS are as follows:


|Type |Chart |
|---|---|
|Context |Duration distribution, token distribution, execution steps |
|Trace analysis |Trace analysis (data retrieval limit: 50,000 records) |
|Model analysis |Model invocation count, model token consumption, model invocation latency |
|Tool analysis |Tool invocation count, tool invocation tokens, tool invocation latency, tool invocation details |
|Memory analysis |Tool invocation count, tool invocation tokens, tool invocation latency, tool invocation details |
|Knowledge base analysis |Tool invocation count, tool invocation tokens, tool invocation latency, tool invocation details |


<span id="6cdbdfe8"></span>
## Integrate a log application


1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. On the **Application Marketplace** tab, select the log application card to be integrated. For example, on the **VeADK** card, click **Integrate application**.

5. Configure the integration parameters, then click **Integrate application**.

   
   |Parameter |Description |
   |---|---|
   |Name |Name of the integrated log application. |
   |Description |Description of the integrated log application. |
   |Region |Region of the integrated log application. |
   |Project |Select the project where the data will be stored. |
   |Report center |Select the reports to generate. For example, select **veadk Observability**, and then configure the following parameters:<br><br><br>* Dashboard name: Set the dashboard name corresponding to the report.<br><br>* Log topic: Select a log topic as the data source.<br><br>* Field validation:<br><br>   * The system automatically matches the corresponding index fields in the log topic based on the type of log application.<br><br>   * If some fields are missing, are of different types, or statistics are not enabled, manually replace the fields.<br><br>   * For details about dashboard fields, see [Log field description for preset dashboard](https://docs.byteplus.com/docs/tls/Description_of_preset_template_dashboard_log_fields). |
   

6. After successful integration, the dashboard page opens by default.


<span id="94e25fa4"></span>
## Manage my applications

After successfully integrating a log application, you can perform the following management operations on the integrated log applications:


1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. Go to the **My applications** tab. In the **Actions** column for the corresponding log application, the following management operations are supported:

   
   |Operation |Note |
   |---|---|
   |Access management |Click **Access management** to go to the **Access management** tab, where you can modify the name and description of the accessed log application. |
   |Cancel access |Click **Cancel access**, confirm the information in the cancel access dialog box, and then click **Cancel access** again. |
   |View in dashboard |Click **View in dashboard** to go to the corresponding dashboard page and view related monitoring information in the dashboard. You can add charts and perform other operations. For details, see [Common dashboard actions](https://docs.byteplus.com/docs/tls/Managing_dashboards). |
