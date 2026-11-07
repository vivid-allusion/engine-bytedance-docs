---
title: "JuiceFS access analysis"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/JuiceFS_access_analysis"
---

This section introduces JuiceFS access analysis, a basic service monitoring log application provided in the TLS application marketplace.

<span id="8eac7c9f"></span>
## Overview

Log observability capabilities built on JuiceFS support the detection and analysis of attacks on JuiceFS.


* Access log analysis overview: Performs in\-depth analysis and visualization of JuiceFS access logs, extracting key metrics for read, write, and delete operations, such as IO size distribution and repeated read/write information.

* Access log analysis details: Performs in\-depth analysis and visualization of JuiceFS access logs, covering statistics for read and write operations, repeated read/write, delete size, and other key metrics including their proportions and size information.


<span id="5ae6b422"></span>
## Monitoring chart details

The chart details for JuiceFS access analysis in TLS are as follows:


* Access log analysis overview

   
   |Type |Chart |
   |---|---|
   |Write IO |* Actual write size—including Cover write, write IO size distribution, Cover write size<br><br>* File sequential write ratio—distribution (operation count), Cover write time ratio |
   |Read IO |* Total read size, read IO size distribution, total repeated read size<br><br>* Repeated read time ratio, file sequential read ratio—distribution (operation count) |
   |Deletion status |* Total deletion size<br><br>* File lifecycle distribution<br><br>* Summary of read, write, and delete operations |
   

* Access log analysis details

   
   |Type |Chart |
   |---|---|
   |Overview |* Proportion of cover writes to actual writes<br><br>* Proportion of repeated reads to total read size<br><br>* Proportion of deletion size to actual write size (excluding cover writes) |
   |Write IO |* Actual write size – including cover writes, actual write size – excluding cover writes<br><br>* Cover write size, proportion of cover write size, proportion of cover write time<br><br>* Write operation statistics, write IO size distribution, write IO duration distribution, write operation details, file write size<br><br>* Flush operation statistics excluding operations with duration less than 20 ms, flush IO duration distribution (excluding operations less than 20 ms), flush operation details<br><br>* File sequential write ratio – distribution (data size), file sequential write ratio – distribution (operation count)<br><br>* Sequential write ratio by file ID – data size, sequential write ratio by file ID – operation count |
   |Read IO |* Total read size, read operation statistics, read IO size distribution, read IO duration distribution, read operation details, file read size<br><br>* Total repeated read size, proportion of repeated read size, proportion of repeated read time, repeated read size<br><br>* File sequential read ratio – distribution (data size), file sequential read ratio – distribution (operation count)<br><br>* Sequential read ratio by file ID – data size, sequential read ratio by file ID – operation count |
   |Deletion status |* Total deletion size, deletion operation statistics, deletion IO size distribution, deletion duration distribution, deleted file size<br><br>* Number of files deleted but not created, details of files deleted but not created<br><br>* File lifecycle distribution |
   |Summary of read, write, and delete |Top operations |
   


<span id="df9e1b83"></span>
## Integrate log applications


1. Log in to [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. On the **Application marketplace** tab, select the log application card to be integrated. For example, on the **JuiceFS access analysis** card, click **Integrate application**.

5. Configure the integration application parameters, then click **Integrate application**.

   
   |Parameters |Description |
   |---|---|
   |Name |Name of the integrated log application. |
   |Description |Description of the integrated log application. |
   |Region |Region of the integrated log application. |
   |Log project |Select the log project to store the data. |
   |Report center |Select the reports to generate. For example, in this case, select **Access log analysis overview**, **Access log analysis details**, then set the following parameters:<br><br><br>* Dashboard name: Set the dashboard name corresponding to the report.<br><br>* Log topic: Select the log topic as the data source.<br><br>* Field validation:<br><br>   * The system automatically matches the corresponding index fields in the log topic based on the log application type.<br><br>   * If some fields are missing, field types differ, or statistics are not enabled, manually replace the fields.<br><br>   * Dashboard field description. For details, see [Log field description for preset dashboard](https://docs.byteplus.com/docs/tls/Description_of_preset_template_dashboard_log_fields). |
   

6. After successful integration, the dashboard page is displayed by default.


<span id="b60c2d9b"></span>
## Manage my applications

After successfully integrating a log application, you can perform management operations on the integrated log applications:


1. Log in to [TLS console](https://console.byteplus.com/tls/).

2. In the top navigation bar, select the region where TLS is located.

3. In the left navigation bar, select **Common features** \> **Log applications**.

4. Go to the **My applications** tab. In the **Actions** column for the corresponding log application, the following management operations are supported:

   
   |Operation |Description |
   |---|---|
   |Access management |Click **Access management** to enter the **Access management** tab, where you can modify the name and description of the connected log application. |
   |Cancel access |Click **Cancel access**, confirm the information in the cancel access pop\-up window, and then click **Cancel access** again. |
   |View in dashboard |Click **View in dashboard** to enter the corresponding dashboard page and view related monitoring information in the dashboard. You can perform operations such as Add chart. For details, see [Common dashboard actions](https://docs.byteplus.com/docs/tls/Managing_dashboards). |
