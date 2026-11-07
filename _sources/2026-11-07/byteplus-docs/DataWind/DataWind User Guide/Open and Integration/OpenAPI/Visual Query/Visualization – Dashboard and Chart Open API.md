---
title: "Visualization – Dashboard and Chart Open API"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Visualization_Dashboard_and_Chart_OpenAPI"
---

<span id="_1-仪表盘-图表嵌入"></span>
# 1. Dashboard & Chart Embedding

<span id="_1-1-概述"></span>
## 1.1 Overview

When embedding dashboards externally, authentication is supported via OpenAPI. The embedding party controls the application for an OpenAPI token to achieve custom permission management, and this also avoids the issue of repeated login when accessing the system via the dashboard.

Caution: Before using the interfaces described in this document, please familiarize yourself with the invocation method. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="_1-2-方案介绍"></span>
## 1.2 Solution Introduction

First, refer to the OPEN API overview to apply for a `clientID` and `secret`, and use the `clientID` and `secret` to obtain a `jwtToken`.

<span id="_1-2-1-前端接入"></span>
### 1.2.1 Front\-End Integration

**Embed in desktop page**

```Plain
// 在嵌入的iframe url上带上jwtToken；
// 注意OpenAPI鉴权路由前缀使用/bi-open/而不是/bi/；
// SaaS环境
<iframe src=`uri/bi/datawind-open/.......?a=b&jwtToken=${jwtToken}` />
// 私有化部署
<iframe src=`uri/bi-open/.......?a=b&jwtToken=${jwtToken}` />
```


**Embed in mobile web page**

```Plain
// 在移动端嵌入的iframe url上带上jwtToken；
// SaaS环境
<iframe src=`uri/bi/datawind-h5/.......?a=b&jwtToken=${jwtToken}` />
// 私有化部署
<iframe src=`uri/bi-h5/.......?a=b&jwtToken=${jwtToken}` />
```


<span id="_1-2-2-整体交互时序图"></span>
### 1.2.2 Overall Interaction Sequence Diagram

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2758df2d67c94e088877124bc53b0488~tplv-goo7wpa0wc-image.image" width="549px" /></div>


<span id="_1-3-使用示例"></span>
## 1.3 Usage Example

<span id="_1-3-1-相关术语"></span>
### 1.3.1 Related Terminology

Embedding party: The platform that embeds the system dashboard (including but not limited to using an iframe) and exposes it to users for access on its own platform.

Browsing user: The user who views the embedding party's page and may see the embedded dashboard page.

Intelligent Data Insight user: The user entity on the Intelligent Data Insight platform.

System administrator: The system administrator of Intelligent Data Insight (with the highest level of permissions across the site).

<span id="_1-3-2-案例一"></span>
### 1.3.2 Case

**Requirement Description**

The embedding party needs to display the dashboard of the Intelligent Data Insight product on its own platform, and independently manages permission control (or does not implement permission control). For example, the embedding party has a BI display page, and the product dashboard is embedded in that page. When a browsing user accesses the display page, if the embedding party determines that the user has access permission for that page, the dashboard on that page is displayed unconditionally, regardless of the user's actual permissions in the Intelligent Data Insight product (or the user may not even exist on the Intelligent Data Insight platform).

**Usage Process**

(1) The system administrator applies for a `clientID` and `secret` with the binding type set to system.

(2) When a browsing user visits the embedding party, the embedding party applies for an Intelligent Data Insight system token and sets `proxyUser` to the Intelligent Data Insight system user corresponding to the current browsing user.


* Caution: The corresponding Smart Data Insight users do not need to have a one\-to\-one mapping with browsing users.

* Example 1: To display the product dashboard to personnel in a specific region, the embedding platform only needs to create a “virtual user” in the Smart Data Insight system corresponding to that region and grant the virtual user the appropriate permissions (such as resource access permissions, data row and column permissions, and so on). The embedding party can set proxyUser to the corresponding virtual user based on different attributes of the browsing user (for example, different regions).

* Example 2: To display the embedded product dashboard unconditionally, that is, any browsing user accessing the embedding platform can view the embedded dashboard without restriction, proxyUser can be set to a user who has permission for the embedded dashboard (or a user with higher permissions).

   (3) Then embed the token in the product dashboard Iframe.

   (4) (This step is performed automatically by the product dashboard) The Smart Data Insight system dashboard Iframe sends a query to the product backend, and the Smart Data Insight system backend parses the user identity from the token, determines whether the user has permission, as well as the corresponding data row and column permissions, and returns the query result.

   (5) (This step is performed automatically by the product dashboard) The product dashboard Iframe receives the data returned by the Smart Data Insight system backend and renders the data.

   (6) The process is complete.


<span id="_2-仪表盘删除"></span>
# 2. Delete dashboards

<span id="50f6d271"></span>
#### 2.1 Request description

DELETE /aeolus/api/open/v2/dashboard/dashboards

Permissions: Only dashboards with management permissions can be deleted. Deleting another user's personal dashboard or deleting directories is not supported.

<span id="请求头"></span>
#### 2.2 Request headers


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|Authorization |string |Yes |xxx |Used for backend authentication and authorization. Format: Bearer jwt_token, where jwt_token is obtained through the JWT application API. |


<span id="请求参数"></span>
#### 2.3 Request parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|dashboards |array[int] |No |[1, 2] |List of dashboard IDs to be deleted |


<span id="响应"></span>
#### 2.4 Response parameters


|Parameter |Level |Type |Description |Example value |
|---|---|---|---|---|
|code |1 |string |Return code. See "Error codes" for definitions. |aeolus/ok |
|msg |1 |string |Message |Success |
|data |1 |object |Data content |*  |
|results |2 |array[object] |Deletion result information |*  |
|dashboard |3 |int |Dashboard ID |1 |
|success |3 |bool |Whether the deletion was successful |true/false |
|reason |3 |string |Failure reason, only applicable when success is False |The resource has been deleted |


<span id="响应示例"></span>
#### 2.5 Response example

```json
{
    "code": "aeolus/ok",
    "data": {
        "results": [
            {
                "dashboard": ******,
                "reason": "资源已被删除",
                "success": false
            },
            {
                "dashboard": ******,
                "reason": null,
                "success": true
            }
        ]
    },
    "msg": "成功"
}
```


<span id="_3-第三方刷新仪表盘-关闭内容弹窗"></span>
# 3. Third\-party dashboard refresh & close content pop\-up

Background: Users use a third\-party information entry webpage to fill in information into a Feishu spreadsheet, and use this Feishu spreadsheet to create a dataset directly, which is then analyzed on the dashboard.

Based on this context, users can navigate from the dashboard to the data entry web page, fill in data into the Feishu sheet on the web page, and after clicking "Complete" on the web page, close the pop\-up window and refresh the dashboard according to the updated Feishu sheet. (The following two images are for illustration only. Please refer to the actual situation for specific content.)
