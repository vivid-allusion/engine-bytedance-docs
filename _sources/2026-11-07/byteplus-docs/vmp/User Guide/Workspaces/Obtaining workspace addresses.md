---
title: "Obtaining workspace addresses"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Obtaining-the-Remote-Write-URL-and-Query-URL"
---

A Vital Managed Service for Prometheus (VMP) workspace provides multiple standard addresses such as the remote write URL and the query URL for writing or querying data. This topic describes how to obtain the addresses of a VMP workspace.

<span id=".5Zyw5Z2A5L-h5oGv5LuL57uN"></span>
## Address information description

A VMP workspace provides multiple standard addresses such as the remote write URL and the query URL. The following table describes the meanings and features of different addresses.


|Address name |Address description |
|---|---|
|Remote write URL |This address is used to store the collected data in the workspace. |
|Query URL |This address is used to read data stored in the workspace. You can use Grafana or third\-party platforms to visualize and analyze the data. For more details, see [Deploying Grafana and connecting to a workspace in the VKE cluster](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster). |
|Push gateway URL |This address is used to push data to the server. For more details, see [Pushing data by using Pushgateway](https://docs.byteplus.com/en/docs/vmp/Pushing_data_by_using_Pushgateway). |
|Federated query URL |The upper\-layer Prometheus system uses this address to scrape selected data from the VMP workspace and aggregate data from multiple Prometheus services. This enables a scalable Prometheus monitoring system. For more details, see [Scraping workspace time series by using the federate endpoint](https://docs.byteplus.com/en/docs/vmp/Scraping_selected_time_series_using_the_federate_endpoint).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature is currently in <strong>beta</strong>. If you want to use it, contact your account manager.</div><br> |


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A workspace has been created. For more details, see [Creating a workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

* To obtain the public endpoints of the workspace, you need to enable **Public network access** and configure a valid certificate public key when you create the workspace. For more details, see [Creating a workspace](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus).

2. Click **Workspace** in the left navigation bar to go to the workspace list page.

3. In the workspace list, find the workspace for which you want to view addresses and click the workspace name to go to the Overview page of the workspace.

4. In the **Address information** section, you can view the addresses of the workspace.
