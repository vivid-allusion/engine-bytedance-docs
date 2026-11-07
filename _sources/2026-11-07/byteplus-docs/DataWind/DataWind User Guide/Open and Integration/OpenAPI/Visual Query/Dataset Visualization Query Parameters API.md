---
title: "Dataset Visualization Query Parameters API"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dataset_Visualization_Query_Parameters_API"
---

This document introduces the "Dataset Visualization Query Parameters API" and explains how to view and update visualization query parameter configurations through the API.

<span id="90275713"></span>
# Function overview

The Dataset Visualization Query Parameters API allows users to view and update dataset visualization query parameter configurations via the API.

The entry point is as follows:


1. Go to the "Data Preparation" \- "Dataset" page, select the dataset for which you want to configure visualization query parameters, right\-click and select "More", then click "Visualization Query Configuration".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cb9ff812e614787964884cd276333d3~tplv-goo7wpa0wc-image.image) </span>

2. On the "Visualization Query Configuration" page, configure the relevant visualization query parameters for the dataset, including push, query, default settings, and so on.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73a83d808c5c4d27863089aaf2660b7e~tplv-goo7wpa0wc-image.image) </span>


<span id="4dccbfe0"></span>
# Prerequisites

Before using the API described in this document, you must complete the preliminary steps of integrating JWT\-Token and applying for a Token. Please first review how to use the API. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="f9f95441"></span>
# View dataset visualization query parameter configuration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The user must have at least permission to view the dataset.</div>


<span id="f694aae7"></span>
## Request description


* Request method: GET

* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/vqsParams`


<span id="23f31fc8"></span>
## Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|dataSetId |integer |Yes |123 |Dataset ID. For how to obtain it, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |


<span id="d9b82157"></span>
## Request example

```bash
curl --location --request GET '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/vqsParams' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}'
```


<span id="00c10442"></span>
## Response parameters


|Parameter |Type |Example value |Description |
|---|---|---|---|
|detailedFields |bool |true | |
|enableReportMonitor |bool |false |Filter search optimization. true means allowed, false means not allowed. When enabled, the filter will prioritize using front\-end cache when searching for data items in the exact search list |
|enableSubscription |bool |false |Dataset subscription. true means allowed, false means not allowed. When enabled, after subscribing to the dataset, chart data can be displayed in dashboard subscription snapshots, but this will put pressure on the cluster |
|queryPartitionLimit |bool |true |Auto query. true means allowed, false means not allowed. When enabled, auto\-triggering queries is allowed in the visualization query interface, but this will put pressure on the cluster |
|vqsAutoQuery |bool |true | |
|vqs_auto_query |bool |true | |


<span id="1befe8e0"></span>
## Response example

```json
{
    "code": "aeolus/ok",
    "data": {
        "detailedFields": [],
        "enableReportMonitor": true,
        "enableSubscription": true,
        "queryPartitionLimit": null,
        "vqsAutoQuery": true,
        "vqs_auto_query": true
    },
    "msg": "成功"
}
```


<span id="_3-2-更新数据集可视化查询参数配置"></span>
# Update dataset visualization query parameter configuration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The user must have at least permission to edit the dataset.</div>


<span id="f7a684bb"></span>
## Request description


* Request method: PUT

* Request URL: `{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/vqsParams`


<span id="94d07c21"></span>
## Request parameters


|Parameter |Type |Required |Description |
|---|---|---|---|
|enableReportMonitor |string |Yes |Create new monitoring<br><br>After enabling, this dataset can create new monitoring, but it will put pressure on the cluster. |
|enableSubscription |bool |Yes |The default lookback period after the first creation of the dataset subscription<br><br>After enabling, once the dataset is subscribed, chart data can be displayed in the dashboard subscription screenshot, but it will put pressure on the cluster. |
|vqsAutoQuery |bool |Yes |Automatic query<br><br>After enabling, queries can be triggered automatically in the visual query interface, but it will put pressure on the cluster. |
|enableSearchOptimizationStrategy |bool |Yes |Search optimization for filtering<br><br>If disabled, searching for data items in the list will query all backend data from the past 30 days to ensure data integrity. |


<span id="c10d363c"></span>
## Request example

```bash
curl --location --request PUT '{{domain}}/aeolus/api/v4/open/dataset/{{dataSetId}}/vqsParams' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {{jwtToken}}' \
--data-raw '{
    "vqsParams": {
        "vqsAutoQuery": false,
        "enableSubscription": false,
        "enableReportMonitor": false,
        "enableSearchOptimizationStrategy": false
    }
}'
```


<span id="fa62f9cf"></span>
## Response parameters


|Parameter |Type |Required |Description |
|---|---|---|---|
|enableReportMonitor |string |Yes |Create new monitoring<br><br>After enabling, this dataset can create new monitoring, but it will put pressure on the cluster. |
|enableSubscription |bool |Yes |The default lookback period after the first creation of the dataset subscription<br><br>After enabling, once the dataset is subscribed, chart data can be displayed in the dashboard subscription screenshot, but it will put pressure on the cluster. |
|vqsAutoQuery |bool |Yes |Automatic query<br><br>After enabling, queries can be triggered automatically in the visual query interface, but it will put pressure on the cluster. |
|enableSearchOptimizationStrategy |bool |Yes |Search optimization for filtering<br><br>If disabled, searching for data items in the list will query all backend data from the past 30 days to ensure data integrity. |


<span id="f0074082"></span>
## Response example

```json
{
    "code": "aeolus/ok",
    "data": null,
    "msg": "成功"
}
```
