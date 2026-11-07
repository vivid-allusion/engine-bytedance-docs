---
title: "CloudLens for VKE"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/CloudLens_for_VKE"
---

This section introduces the CloudLens for VKE log application for cloud product observability, available in the TLS application marketplace.

<span id="cde39a6e"></span>
## Overview

Cloud product log observability capabilities built on VKE clusters support displaying event information throughout the entire lifecycle of a Pod.

Display event information for the entire lifecycle of a Pod, and view Pod event details, such as event level, event source, event type, and more.

<span id="e60f2e83"></span>
## Monitoring dashboard details

The monitoring dashboard details for TLS CloudLens for VKE are as follows:


|Type |Chart |
|---|---|
|VKE observability |Pod lifecycle |
||Event list |


<span id="99bf7940"></span>
## Integrate log application

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div>


<div data-tips="true" data-tips-type="default">After the CloudLens for VKE log application is created, modification and cancellation of integration are not supported.</div>



1. Log in to the [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. On the **Application marketplace** tab, select the log application card to be integrated. For example, on the **CloudLens for VKE** card, click **Integrate application**.

5. Configure the integration parameters, then click **Integrate application**.

   
   |Parameters |Description |
   |---|---|
   |Name |Name of the integrated log application. |
   |Description |Description information for the integrated log application. |
   |Region |Region of the integrated log application. |
   |Project |Select the project for storing data. |
   |Report center |Select the reports to be generated. For example, in this case, select **Pod event monitoring**, then set the following parameters:<br><br><br>* Dashboard name: Set the dashboard name corresponding to the report.<br><br>* Log topic: Select the log topic as the data source.<br><br>* Field validation:<br><br>   * The system automatically matches the corresponding index fields in the log topic based on the log application type.<br><br>   * If some fields are missing, field types differ, or statistics are not enabled, manually replace the fields.<br><br>   * For dashboard field descriptions, see [Log field description for preset dashboard](https://docs.byteplus.com/docs/tls/Description_of_preset_template_dashboard_log_fields). |
   

6. After successful integration, you will be directed to the dashboard page by default.
