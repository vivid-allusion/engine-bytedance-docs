---
title: "CloudLens for TLS"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/CloudLens_for_TLS"
---

This section introduces the CloudLens for TLS log application available in the TLS application marketplace.

<span id="434da20b"></span>
## Overview

Leveraging TLS's self\-monitoring and data insight capabilities, CloudLens for TLS provides usage analysis, performance monitoring, and operation analysis services.

<span id="d72dc2fe"></span>
## Monitoring chart details

The details of billing resource monitoring charts for CloudLens for TLS are as follows:

<span id="19c1bbc2"></span>
### Billing resource monitoring


|Type |Chart |
|---|---|
|Resource monitoring |* <div style="text-align: start-_pOwxG"><br>Index traffic</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Read traffic</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Raw log write traffic</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Compressed write traffic</div><br> |
|Usage details |* <div style="text-align: start-_pOwxG"><br>Year\-on\-year comparison of current total billable storage</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Year\-on\-year comparison of current total billable log storage</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Year\-on\-year comparison of current total billable index storage</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Summary of log storage</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Summary of index storage</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Top 10 topics by raw write traffic</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Top 10 topics by read traffic</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Current top projects by billable usage details</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Current top topics by billable usage details</div><br> |


<span id="b3069d76"></span>
### LogCollector collection monitoring


|Type |Chart |
|---|---|
|Overall status |* <div style="text-align: start-_pOwxG"><br>Raw data traffic</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Memory usage distribution</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>CPU consumption distribution</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Number of active LogCollectors</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Overall status</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>CPU trend</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Memory trend</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Data sending traffic</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Processing and sending status</div><br> |
|Exception monitoring |* <div style="text-align: start-_pOwxG"><br>Number of active clients</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Number of restarted clients</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Restart client list</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Full error information</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Duplicate log file configuration issue</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Time parsing error</div><br><br><br>* <div style="text-align: start-_pOwxG"><br>Collection delay</div><br> |
|File collection monitoring |* Collection directory details<br><br>* Collection details<br><br>* Trend of collected file count changes<br><br>* Number of delayed collected files<br><br>* File collection delay<br><br>* Number of LogCollector instances collecting |


&nbsp;

<span id="c68bff16"></span>
## Steps to integrate a log application

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div>


<div data-tips="true" data-tips-type="default">After a CloudLens for TLS log application is successfully created, you cannot modify or cancel billing resource monitoring access. You can enable or disable LogCollector collection monitoring.</div>



1. Log in to [TLS console](https://console.byteplus.com/tls/).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. On the **Marketplace** tab, select the log application card to be integrated. For example, on the **CloudLens for TLS** card, click **Integrate application**.

5. According to the prompts on the interface, confirm the following information, and then click **Submit**.

   
   |Parameters |Description |
   |---|---|
   |Billing notes |Log storage and query analysis for CloudLens for TLS are free of charge. |
   |Authorize RAM access |Grant cross\-service access permissions. |
   |Log storage region |Confirm log storage region. |
   

6. After successful integration, you will enter the dashboard page by default.


<span id="4790e61e"></span>
## Manage LogCollector collection monitoring

After the log application is successfully integrated, you can perform management operations on the integrated log application:


1. Log in to [TLS console](https://console.byteplus.com/tls/).

2. Select the region where log service is located from the top navigation bar.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. Go to the **My applications** tab, and in the **Actions** column of the corresponding log application, click **Access management**.

5. Click **Collection monitoring access** to perform the following management operations:

   
   |Actions |Description |
   |---|---|
   |View collection status |In the collection monitoring access list, you can check whether the corresponding host group has enabled LogCollector service log collection. You can search for the corresponding host group by host group name or host group ID. |
   |Disable collection monitoring |Click **Disable** in the **LogCollector service log** column of the corresponding host group row to disable collection. |
   |Enable collection monitoring |Click **Enable** in the **LogCollector service log** column of the corresponding host group row to enable collection. |
