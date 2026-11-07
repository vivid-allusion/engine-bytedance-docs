---
title: "Bill splitting by labels"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Bill_splitting_by_labels"
---

Vital Managed Service Prometheus supports identification and classification by configuring labels (tags) for workspace, and performs bill splitting based on label dimensions to address financial cost sharing issues.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Resource tag consists of a set of KV key\-value pairs. You can categorize and aggregate cloud resources from various dimensions using resource tags, which are also used in scenarios such as tag\-based authorization and bill splitting by labels.

<span id=".5Yib5bu65bel5L2c5Yy65bm25re75Yqg5qCH562-"></span>
## Create a workspace and add labels


1. Log in to the [VMP Console](https://console.byteplus.com/observe/prometheus).

2. On the top navigation bar, select the target region.

3. Click **Workspace** on the left navigation bar to go to the workspace list page.

4. Click **Create Workspace**, configure the workspace, and add bill splitting labels.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For configuration details of the workspace, please refer to <a href="https://docs.byteplus.com/en/docs/vmp/Creating-workspaces">Create Workspace</a>.   </div>
   

<span id=".5p-l55yL57uT5p6c"></span>
## View results

<span id=".5p-l55yL5qCH562-6LWE5rqQ"></span>
### View label resources


1. Log in to [Resource Management](https://console.byteplus.com/resourcemanager).

2. Select **Label Management** \> **Label List** in the left navigation bar, and select the **Custom Labels** tab.

3. Select the target label from the label list, click **View Resources** from the **Operation** column to view the resource details under this label.


<span id=".5p-l55yL5YiG6LSm6LSm5Y2V"></span>
### View splitting bills

After adding bill splitting label to the Vital Managed Service for Prometheus workspace, the information of this label will be displayed in the bill. You can use this label to filter splitting bills.


1. Log in to [Cost Center](https://console.byteplus.com/finance).

2. Select **Bill Management** \> **Splitting Bills** in the left navigation bar.

3. On the **Splitting Bills** page, it supports filtering bills by bill splitting labels.
