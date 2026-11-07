---
title: "Reference: Methods for Obtaining Resource IDs"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Reference_Methods_for_Obtaining_Resource_IDs"
---

**A resource ID (Resource ID) is an identifier used to uniquely identify various types of "resources" in a computer system. Its primary function is to accurately locate and distinguish different resource entities through standardized strings or numbers**. This article introduces how to obtain resource IDs for projects, datasets, dashboards, charts, and screens, and more.

<span id="74d7b558"></span>
# Project (app)

<span id="c5a6072e"></span>
## appId

Project ID. You can obtain it by opening any URL under a project. As shown in the figure, open any link under a project; the URL is as follows, and the app_Id value is 1010681.

```plaintext
https://console.volcengine.com/bi#/dashboard/47610?appId=1010681
```


<span id="a7ed1b24"></span>
# Agent

<span id="6c63d736"></span>
## agentId

Agent ID. After creating an agent, you can view the corresponding agent ID on the agent list page, as shown below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a2da930e05440fc8e096d6f61f624a4~tplv-goo7wpa0wc-image.image) </span>

<span id="d5a0e4b8"></span>
# Dataset

<span id="67395b57"></span>
## dataSetId

Dataset ID. You can obtain it by opening any URL under a dataset. As shown in the figure, open any link for a dataset; the URL is as follows, and the dataSetId value is 10285362.

```plaintext
https://console.volcengine.com/bi/datawind#/dataManage/detail/10285362?appId=20058765&belong=1&region=cn-beijing
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19357e8f0ba642088aaa8f9bc5039b0a~tplv-goo7wpa0wc-image.image) </span>

<span id="1c82a3ec"></span>
# Knowledge configuration

<span id="06ef8660"></span>
## Forced recall template ID

To use a specific template for forced recall when working with Deep Research OpenAPI, upload the recall template to the agent's knowledge configuration. Once completed, open the knowledge configuration page and use F12 to open the page console. In docknowledge, locate the ID for the corresponding recall template.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/590330296eb54b459afe60a4037fb432~tplv-goo7wpa0wc-image.image) </span>

<span id="2226aea2"></span>
# Dashboard

<span id="48db6b9d"></span>
## dashboardid

When using Intelligent Data Insight together with the Intelligent Analysis Agent, you can view the corresponding dashboardid value in the URL of the dashboard page in Intelligent Data Insight.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e41e04eb6564a92a8df344897574e0d~tplv-goo7wpa0wc-image.image) </span>

<span id="9d7e39e7"></span>
## sheetid

When using Intelligent Data Insight together with the Intelligent Analysis Agent, if your dashboard contains multiple sheet pages for charts, click the corresponding chart sheet. You can then view the sheetid value in the URL of the dashboard page in Intelligent Data Insight.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/67979c95645841d3a67f7548b2b29a66~tplv-goo7wpa0wc-image.image) </span>

<span id="267a3cdd"></span>
# Visual query

<span id="af7185c7"></span>
## rid（reportid）

When using Intelligent Data Insight together with the Intelligent Analysis Agent, after saving the visual query result as a dashboard, you can view the reportid for the corresponding dashboard in the URL of the visual query editing page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a081073355b543c2a995c5263265f745~tplv-goo7wpa0wc-image.image) </span>
