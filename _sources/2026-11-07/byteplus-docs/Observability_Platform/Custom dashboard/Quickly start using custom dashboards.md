---
title: "Quickly start using custom dashboards"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Quickly_start_using_custom_dashboards"
---

A custom dashboard is a personalized data visualization panel focused on system observability. You can use it to integrate, display, and analyze system observability data, to comprehensively understand the system status and quickly locate issues. This topic describes how to quickly start using custom dashboards.

<span id="eM5vLUT9"></span>
## Background

Custom dashboards enable users and teams to independently design and configure custom data visualization panels based on their specific needs, delivering intuitive data visualization. Based on integrated data from multiple sources, key information is displayed in formats such as time series charts, metric cards, pie charts, bar charts and tables. These dashboards support flexible adjustments to layout, data dimensions, and display styles, facilitating on\-demand data visualization. The core features are as follows:


* **Multiple data sources**: Supported types of data sources include Server\-side Monitoring, VMP, Cloud Monitor, TLS, and Metrics. The three elements of observability and business data are covered.

* **Open ecosystem**: Fully compatible with Grafana and Grafana JSON and supports exporting to GrafanaModel.


<span id="QCPelrHz"></span>
## Prerequisites

The relevant monitoring services for data sources have been activated, and observability data can be obtained normally.

<span id="HfNpDNME"></span>
## Procedure

Follow the steps below to quickly start using custom dashboards.

<span id="iVqJF12r"></span>
### Step 1: Create a folder


1. Log in to the[ Observability Platform console](https://console.byteplus.com/observe/dashboard/dashboard), and in the left navigation bar, select **Custom Dashboard**.

2. On the dashboard management page, click **Create Folder**. Enter a name for the folder to manage dashboards.


<span id="MWvSelcW"></span>
### Step 2: Create a dashboard

Currently, three methods are available for creating a dashboard. Choose the one that best fits your scenario and needs.


<Tabs>
<Tab zoneid="jRL8WTYP8z" title="Directly create">
<TabTitle>Directly create</TabTitle>

On the dashboard management page, click **Create dashboard** and select **Directly create ** to create a new dashboard.


|Parameter |Description |
|---|---|
|Name |Specify a name for the custom dashboard. The name must be unique. |
|Own folder |Select a folder to which the dashboard belongs to facilitate dashboard management. |





</Tab>
<Tab zoneid="QZ5iWF6Nsm" title="JSON import">
<TabTitle>JSON import</TabTitle>

On the dashboard management page, click **Create dashboard**, select the **JSON import ** option, and provide the JSON configuration of an existing dashboard to quickly create a new one. This is applicable for cross\-platform scenarios or for quickly copying dashboards from Grafana.


|Parameter |Description |
|---|---|
|JSON file |Click to upload a file, or drag and drop it directly.<br><br><br>* Currently, only JSON files under 10 MB can be uploaded.<br><br>* Currently, JSON files exported from this platform or from Grafana are supported. |
|Name |The name for the custom dashboard. The name cannot exceed 120 characters and must be unique. |
|Own folder |Select a folder to which the dashboard belongs to facilitate dashboard management. |





</Tab>
<Tab zoneid="gca43GpoCM" title="Copy dashboard">
<TabTitle>Copy dashboard</TabTitle>

On the dashboard management page, click **Copy** in the Actions column of an existing dashboard to quickly create a new dashboard based on the current one. This allows you to quickly create dashboards within the same platform.


|Parameter |Description |
|---|---|
|Name |The name for the custom dashboard. The name cannot exceed 120 characters and must be unique. |
|Own folder |Select a folder to which the dashboard belongs to facilitate dashboard management. |





</Tab>
</Tabs>


<span id="8RQ6LMlt"></span>
### Step 3: Add and edit charts

After creating the dashboard, you will be redirected to the dashboard configuration page. Click the **Click to add chart** option to add charts to the dashboard as needed. After configuration, click **Save** and **Back dashboard** in sequence. You can repeat this step to add multiple charts as needed.


|Parameter |Description |
|---|---|
|Preview area |Chart preview (top\-left): Displays a real\-time preview of the chart based on your chart and data settings. |
|Chart settings |Chart settings (right): You can configure the appropriate chart type and chart configurations as needed. For details, see [Chart settings](https://docs.byteplus.com/en/docs/Observability_Platform/Chart_settings). |
|Data settings |Data settings (bottom\-left): This is where you configure the data source and how the data is presented as needed. For details, see [Data query](https://docs.byteplus.com/en/docs/Observability_Platform/Data_query) and [Data conversion](https://docs.byteplus.com/en/docs/Observability_Platform/Data_conversion). |


<span id="qHs9yMJd"></span>
### Step 4: Chart layout

Hover over the top of the chart until the cursor changes to a plus sign (+), and drag the chart to adjust its position. Hover over the bottom\-right corner until the cursor changes to an arrow, then drag to scale the chart. Adjust the chart layout as needed. After configuration, click **save** and **Quit editing** in sequence.

<span id="igecDgu7"></span>
### Step 5: View the dashboard

After all configurations are complete, return to the dashboard page to view the data dashboard. You can customize the time range and refresh frequency, or manually refresh the data.

<span id="XIktxSXr"></span>
## What to do next


* When configuring data queries or query variables, you can use global variables for interpolation. For details, see [Global variables](https://docs.byteplus.com/en/docs/Observability_Platform/Global_variables).

* After adding charts, you can group them to facilitate management. For more details, see [Chart grouping](https://docs.byteplus.com/en/docs/Observability_Platform/Chart_grouping).

* For lifecycle management of custom dashboards and related resources, as well as other management operations, see [Managing charts](https://docs.byteplus.com/en/docs/Observability_Platform/Managing_charts), [Managing dashboards](https://docs.byteplus.com/en/docs/Observability_Platform/Managing_dashboards), and [Managing folders](https://docs.byteplus.com/en/docs/Observability_Platform/Managing_folders).
