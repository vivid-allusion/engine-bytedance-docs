---
title: "Visualization - Data Subscription Open API"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Visualization_-_Data_Subscription_Open_API"
---

<span id="aac474bc"></span>
# Prerequisites

Before using the interfaces described in this document, please make sure to understand the invocation methods. For details, see [Invocation Methods](https://docs.byteplus.com/docs/DataWind/Invocation_Methods).

<span id="_3-获取订阅列表"></span>
# Retrieve Subscription List

Used to obtain the list of dashboard subscription configurations for which you have permission. Project administrators and system administrators can retrieve all subscriptions; dashboard administrators can retrieve all subscriptions for the dashboard; users with other permissions can retrieve subscriptions where they are the creator, recipient, or where the permission is based on themselves.

<span id="_3-1-请求"></span>
## Request Description


* Request Method: GET

* Request URL: `{{domain}}/aeolus/api/open/v2/subscription/subscriptions`


<span id="_3-3-请求参数"></span>
## Request Parameters


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|appId |int |Yes |1 |Project ID. For information on how to obtain it, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |
|dashboardId |int |No |1 |Dashboard ID. For information on how to obtain it, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |
|subscriber |string |No |"xiaoming" |The recipient's email prefix, that is, the part before the `@` symbol in the email address. If the email address is `xiaoming@example.com`, then `subscriber` is `xiaoming`. |
|pageSize |int |No |20 |Number of records per page. Default value: 20 |
|pageNumber |int |No |1 |Page number. Default value: 1 |


<span id="_3-4-响应"></span>
## Response Parameters


|Parameter |Type |Example Value |Description |
|---|---|---|---|
|data.pageNumber |int |20 |Current page number |
|data.pageSize |int |1 |Number of records displayed per page |
|data.results |array |*  |Result list, containing specific subscription information |
|data.results.id |int |1000 |Unique subscription ID |
|data.results.owner |string |“xiaoming” |Owner of the subscription |
|data.results.status |int |0 |Status of the subscription: 0 means active, 1 means deleted, 2 means paused |
|data.results.title |object |*  |Information related to the subscription title |
|data.results.title.offset |int |0 |Date offset value, effective only when withDate is true |
|data.results.title.title |string |"datawind subscription" |Title name |
|data.results.title.withDate |boolean |true |Whether the title includes the date |
|data.results.content |object |*  |Push content\-related settings |
|data.results.content.dashboardContentFormat |string |img |Dashboard push format: img for image, pdf for PDF file |
|data.results.content.dashboardContentVisible |boolean |true |Whether to display dashboard content |
|data.results.content.dashboardLinkVisible |boolean |true |Whether to display the dashboard link |
|data.results.description |string |“description” |Description of the subscription |
|data.results.dashboard |object |*  |Associated dashboard information |
|data.results.dashboard.id |int |144250 |Dashboard ID, the unique identifier of the dashboard |
|data.results.dashboard.name |string |"datawind dashboard" |Dashboard name |
|data.results.noticeType |int |0 |Notification method for creation/modification: 0 for pushing to recipients, 1 for pushing to the creator |
|data.results.pushTime |object |*  |Push time\-related settings |
|data.results.pushTime.frequency |int |3 |Push frequency: 0 for daily, 3 for weekly, 5 for monthly |
|data.results.pushTime.offset |int |2 |Dataset synchronization date offset. For example, 1 means the T\-1 data partition. Effective only when untilDataReady is true |
|data.results.pushTime.time |array |["10:00"] |List of push times, format: HH:MM. For example, 10:00 means 10:00 AM |
|data.results.pushTime.timezone |string |“UTC\-08:00” |Time zone, format: UTC\-08:00 |
|data.results.pushTime.untilDataReady |boolean |true |Whether to wait for dataset synchronization to complete before pushing |
|data.results.pushTime.weekdays |array |[1,2] |List of push weekdays, indicating which days of the week to push. [0,6] (Monday to Sunday) |
|data.results.pushType |string |lark |Push method: lark, lark_group, email, email_group, dingtalk, dingtalk_group, webcom, webex |
|data.results.subscribers |array |*  |List of recipients |
|data.results.subscribers.agent |string |“agent” |The email prefix of the permission reference user, that is, the part before the `@` symbol in the email address. If the email is `agent@example.com`, then `subscriber` is `agent`.<br><br>The permission reference user is the one whose permissions are used for the push content. For example, if a chart in the dashboard has row\-level permissions set for its dataset, selecting different permission reference users may result in different data being generated and pushed. |
|data.results.subscribers.subscriber |string |”xiaoming“ |The recipient's email prefix, that is, the part before the `@` symbol in the email address. If the email is `xiaoming@example.com`, then `subscriber` is `xiaoming`. |
|data.results.urls |array |*  |List of related URLs |
|data.results.urls.title |string |"Dashboard sheet\-01" |Title of the URL |
|data.results.urls.url |string |“https://www.example.com“ |Specific URL address |
|data.results.remark |object |*  |Remark\-related information |
|data.results.remark.content |string |"Subscription description" |Remark content |
|data.results.remark.manageLinkVisible |boolean |true |Whether to display the subscription management entry address in the push information |
|data.results.remark.screenshotTimeVisible |boolean |true |Whether to display the screenshot time in the push message |
|data.results.config |object |*  |Subscription configuration information |
|data.results.config.autoRetry |boolean |false |Whether to retry automatically |
|data.results.config.autoSyncSheets |boolean |false |Whether the subscription scope automatically synchronizes dashboard configuration |
|data.results.config.language |string |auto |Language: auto (automatic), zh_CN (Chinese), en_US (English) |
|data.results.config.manageUrl |string |““https://www.example.com“” |Subscription management link |
|data.results.config.noPushIfAbnormal |boolean |false |Whether to skip push if the chart is abnormal |
|data.total |int |1 |Total number of results |


<span id="_3-5-响应示例"></span>
## Response Example

```json
{
    "code":"aeolus/ok",
    "data":{
        "pageNumber":20,
        "pageSize":1,
        "results":[
            {
                "id":1000,
                "owner":"***********",
                "status":0,
                "title":{
                    "offset":1,
                    "title":"datawind订阅",
                    "withDate":true
                },
                "content":{
                    "dashboardContentFormat":"img",
                    "dashboardContentVisible":true,
                    "dashboardLinkVisible":false
                },
                "description":"description",
                "dashboard":{
                    "id":144250,
                    "name":"datawind仪表盘"
                },
                "noticeType":0,
                "pushTime":{
                    "frequency":3,
                    "offset":2,
                    "time":[
                        "10:00"
                    ],
                    "timezone":"UTC+08:00",
                    "untilDataReady":true,
                    "weekdays":[
                        1,
                        2
                    ]
                },
                "pushType":"lark",
                "subscribers":[
                    {
                        "agent":"***********",
                        "subscriber":"***********"
                    }
                ],
                "urls":[
                    {
                        "title":"仪表盘sheet-01",
                        "url":"仪表盘URL"
                    }
                ],
                "remark":{
                    "content":"订阅说明",
                    "manageLinkVisible":true,
                    "screenshotTimeVisible":true
                },
                "config":{
                    "autoRetry":false,
                    "autoSyncSheets":false,
                    "language":"auto",
                    "manageUrl":"订阅管理URL",
                    "noPushIfAbnormal":false
                }
            }
        ],
        "total":1
    },
    "msg":"成功"
}
```


<span id="_4-创建订阅"></span>
# Create Subscription

Used to create a dashboard subscription configuration.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only subscriptions for dashboards with the corresponding permissions can be created.</div>


<span id="_4-1-请求"></span>
## Request Description


* Request Method: POST

* Request URL: `{{domain}}/aeolus/api/open/v2/subscription/subscriptions`


<span id="_4-4-body-参数"></span>
## Request Parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|config |object |No |*  |Subscription configuration information |
|config.autoRetry |boolean |No |true |Whether to retry on failure. Default value: false |
|config.autoSyncSheets |boolean |No |false |Whether to automatically synchronize the dashboard configuration for the subscription scope.<br><br><br>* When urls is empty, the default value is true; otherwise, the default value is false.<br><br>* When autoSyncSheets is true, the urls parameter is ignored. |
|config.language |string |No |"auto" |Language. Optional values: auto (automatic), zh_CN (Chinese), en_US (English) |
|config.manageUrl |string |No |"“https://www.example.com“" |Subscription management link. If not provided, it is set to the DataWind project center subscription management page address. |
|config.noPushIfAbnormal |boolean |No |true |Whether to do not push when the chart is abnormal. Default value: false |
|content |object |Yes |*  |Push content configuration |
|content.dashboardContentFormat |string |No |"img" |Dashboard push content format. img: image, pdf: PDF file. Default value: img |
|content.dashboardContentVisible |boolean |No |true |Whether to display dashboard content. Default value: true |
|content.dashboardLinkVisible |boolean |No |true |Whether to display the dashboard link. Default value: true |
|appId |int |Yes |1 |Project ID. For how to obtain, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |
|dashboardId |int |Yes |1 |Dashboard ID, indicating the subscribed dashboard ID. Effective when urls is empty or not provided, indicating subscription to all sheets of the dashboard. For how to obtain, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |
|pushTime |object |Yes |*  |Push time |
|pushTime.frequency |int |Yes |3 |Push frequency. 0: daily, 3: weekly, 5: monthly |
|pushTime.offset |int |No |2 |Dataset synchronization date offset. For example, 1 means the T\-1 data partition. Only effective when untilDataReady is true. Default value: 1 |
|pushTime.weekdays |array[int] |No |[1,2] |List of push weekdays, indicating which days of the week to push. Required and only effective when push frequency is weekly. Optional value range: [0,6] (Monday to Sunday) |
|pushTime.days |array[int] |No |*  |List of push dates. Required and only effective when push frequency is monthly. Optional value range: [1,31] |
|pushTime.time |array[string] |Yes |["10:00"] |List of push times. Format: HH:MM. For example, 10:00 means 10:00 AM |
|pushTime.timezone |string |Yes |"UTC\-08:00" |Time zone. Format: UTC\-08:00 |
|pushTime.untilDataReady |boolean |No |true |Whether to wait for dataset synchronization to complete before pushing. Default value: false |
|pushType |string |Yes |"lark" |Push method. Optional values: 飞书 (飞书), lark_group (飞书群), email (email), email_group (email group), dingtalk (钉钉), dingtalk_group (钉钉群), webcom (WeCom), webex (webex) |
|remark |object |No |*  |Remark information |
|remark.content |string |No |"Subscription description" |Remark content |
|remark.manageLinkVisible |bool |No |true |Whether to display the subscription management entry address in the push message. Default value: true |
|remark.screenshotTimeVisible |bool |No |true |Whether to display the screenshot time in the push message. Default value: true |
|subscribers |array[object] |Yes |*  |Recipient list |
|subscribers.agent |string |Yes |“agent” |The user whose permissions are used: the email prefix, that is, the part before the `@` symbol in the email address. If the email is `agent@example.com`, then the `subscriber` is `agent`.<br><br>The user whose permissions are used is the user whose permissions are applied to the push content. For example, when the dataset corresponding to a chart in the dashboard has row\-level permissions configured, selecting different permission\-based users may result in different data being generated and pushed. |
|subscribers.subscriber |string |Required |”xiaoming“ |The prefix of the recipient's email address, that is, the part before the `@` symbol in the email address. If the email address is `xiaoming@example.com`, then `subscriber` is `xiaoming`. |
|title |object |Required |*  |Title information |
|title.offset |int |Optional |0 |Date offset value, effective when withDate is true. The default value is 0. |
|title.title |string |Required |"DataWind Subscription" |Title name |
|title.withDate |bool |Optional |true |Whether the title includes the date. The default value is false. |
|urls |array[object] |Required |*  |List of subscribed sheets |
|urls.url |string |Required |"“https://www.example.com“" |Subscription sheet address. See **Get subscription list** for how to obtain it. |


<span id="b0e4d25b"></span>
## Request Example

```json
{
    "config": {
        "autoRetry": true,
        "autoSyncSheets": false,
        "language": "auto",
        "manageUrl": "订阅管理URL",
        "noPushIfAbnormal": true
    },
    "content": {
        "dashboardContentFormat": "img",
        "dashboardContentVisible": true,
        "dashboardLinkVisible": false
    },
    "appId": 555371,
    "dashboardId": *******,
    "description": "description",
    "noticeType": 0,
    "pushTime": {
        "frequency": 3,
        "offset": 2,
        "weekdays": [
            1,
            2
        ],
        "time": [
            "10:00"
        ],
        "timezone": "UTC-08:00",
        "untilDataReady": true
    },
    "pushType": "lark",
    "remark": {
        "content": "",
        "manageLinkVisible": true,
        "screenshotTimeVisible": true
    },
    "subscribers": [
        {
            "agent": "***********",
            "subscriber": "***********"
        }
    ],
    "title": {
        "offset": 1,
        "title": "DataWind订阅",
        "withDate": true
    },
    "urls": [
        {
            "url": "仪表盘链接URL"
        }
    ]
}
```


<span id="_4-6-响应"></span>
## Response Parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|code |string |“aeolus/ok” |Return code. See [Error Codes](https://docs.byteplus.com/docs/DataWind/Visualization_-_Data_Subscription_Open_API#b3617d76) for reference. |
|data |object |*  |Data content |
|data.subscriptionId |int |1000 |Created subscription ID |
|msg |string |“成功” |Prompt message |


<span id="_4-7-响应示例"></span>
## Response Example

```json
{
    "code": "aeolus/ok",
    "data": {
        "subscriptionId": 1000
    },
    "msg": "成功"
}
```


<span id="_5-更新订阅"></span>
# Update Subscription

Used to modify an existing dashboard subscription.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only subscriptions with permission can be modified. Project administrators and system administrators can modify any subscription. Dashboard administrators can modify subscriptions for their respective dashboards. Subscription owners can modify subscriptions they created.</div>


<span id="_5-1-请求"></span>
## Request Description


* Request Method: PATCH

* Request URL: `{{domain}}/aeolus/api/open/v2/subscription/subscriptions`


<span id="d32b257a"></span>
## Request Parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|id |int |Required |1000 |Subscription ID. See **Get subscription list** for how to obtain it. |
|status |int |Optional |0 |Status: 0 \- Normal, 2 \- Paused |
|config |object |Optional |*  |Subscription configuration information |
|config.autoRetry |boolean |Optional |true |Whether to retry on failure. The default value is false. |
|config.autoSyncSheets |boolean |Optional |false |Whether the subscription scope automatically synchronizes with the dashboard configuration.<br><br><br>* When urls is empty, the default value is true; otherwise, the default value is false.<br><br>* When autoSyncSheets is true, the urls parameter is ignored. |
|config.language |string |Optional |"auto" |Language. Optional values: auto (automatic), zh_CN (Chinese), and en_US (English). |
|config.manageUrl |string |Optional |"“https://www.example.com“" |Subscription management link. If not provided, it is set to the DataWind project center subscription management page address. |
|config.noPushIfAbnormal |boolean |Optional |true |Whether to skip push when the chart is abnormal. The default value is false. |
|content |object |Required |*  |Push content configuration |
|content.dashboardContentFormat |string |Optional |"img" |Dashboard push format: img for image, pdf for PDF file. The default value is img. |
|content.dashboardContentVisible |boolean |Optional |true |Whether to display dashboard content. The default is true. |
|content.dashboardLinkVisible |boolean |Optional |true |Whether to display the dashboard link. The default value is true. |
|appId |int |Required |1 |Project ID. See [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for how to obtain it. |
|dashboardId |int |Required |1 |Dashboard ID, indicating the subscribed dashboard ID. Effective when urls is empty or not provided, indicating that all sheets of the dashboard are subscribed. See [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) for how to obtain it. |
|description |string |Optional |“description” |Subscription description |
|noticeType |int |Optional |1 |Create/modify notification method: 0 \- push to recipient, 1 \- push to creator |
|pushTime |object |Required |*  |Push time. Modifying individual fields of pushTime is not supported. |
|pushTime.frequency |int |Required |3 |Push frequency: 0 \- daily, 3 \- weekly, 5 \- monthly |
|pushTime.offset |int |No |2 |Dataset synchronization date offset. For example, 1 indicates the T\-1 data partition. Only effective when untilDataReady is true. The default value is 1. |
|pushTime.weekdays |array[int] |No |[1,2] |List of push weekdays, indicating which days of the week to push. Required and only effective when the push frequency is weekly. Optional values: [0,6] (Monday to Sunday). |
|pushTime.days |array[int] |No |*  |List of push dates. Required and only effective when the push frequency is monthly. Optional values: [1,31] |
|pushTime.time |array[string] |Yes |["10:00"] |List of push times. Format: HH:MM. For example, 10:00 means 10:00 AM. |
|pushTime.timezone |string |Yes |"UTC\-08:00" |Time zone. Format: UTC\-08:00 |
|pushTime.untilDataReady |boolean |No |true |Whether to wait for dataset synchronization to complete before pushing. The default value is false. |
|pushType |string |Yes |"lark" |Push method. Optional values: 飞书 (飞书), lark_group (飞书 group), email (email), email_group (email group), dingtalk (钉钉), dingtalk_group (钉钉 group), webcom (WeCom), webex (webex). |
|remark |object |No |*  |Remark information |
|remark.content |string |No |"Subscription description" |Remark content |
|remark.manageLinkVisible |bool |No |true |Whether the push message displays the subscription management entry address. The default value is true. |
|remark.screenshotTimeVisible |bool |No |true |Whether the push message displays the screenshot time. The default value is true. |
|subscribers |array[object] |Yes |*  |Recipient list |
|subscribers.agent |string |Yes |“agent” |The permission reference person's email prefix, that is, the part before the `@` symbol in the email. If the email is `agent@example.com`, then `subscriber` is `agent`.<br><br>The permission reference person is the one whose permissions are used for the push content. For example, when a chart in the dashboard has row\-level permissions set for its dataset, selecting different permission reference persons may result in different data being pushed. |
|subscribers.subscriber |string |Yes |”xiaoming“ |Recipient email prefix, that is, the part before the `@` symbol in the email. If the email is `xiaoming@example.com`, then `subscriber` is `xiaoming`. |
|title |object |Yes |*  |Title information |
|title.offset |int |No |0 |Date offset value. Only effective when withDate is true. The default value is 0. |
|title.title |string |Yes |"DataWind subscription" |Title name |
|title.withDate |bool |No |true |Whether the title includes the date. The default value is false. |
|urls |array[object] |Yes |*  |Subscription sheet list |
|urls.url |string |Yes |"“https://www.example.com“" |Subscription sheet address. For how to obtain, see **Get subscription list** |


<span id="_5-5-body-示例"></span>
## Request Example

```json
{
    "id": 1000,
    "status": 0,
    "config": {
        "autoRetry": true,
        "autoSyncSheets": false,
        "language": "auto",
        "manageUrl": "订阅管理URL",
        "noPushIfAbnormal": true
    },
    "content": {
        "dashboardContentFormat": "img",
        "dashboardContentVisible": true,
        "dashboardLinkVisible": false
    },
    "appId":{appId},
    "dashboardId": ******,
    "description": "description",
    "noticeType": 0,
    "pushTime": {
        "frequency": 3,
        "offset": 2,
        "weekdays": [
            1,
            2
        ],
        "time": [
            "10:00"
        ],
        "timezone": "UTC-08:00",
        "untilDataReady": true
    },
    "pushType": "lark",
    "remark": {
        "content": "",
        "manageLinkVisible": true,
        "screenshotTimeVisible": true
    },
    "subscribers": [
        {
            "agent": "***********",
            "subscriber": "***********"
        }
    ],
    "title": {
        "offset": 1,
        "title": "DataWind订阅",
        "withDate": true
    },
    "urls": [
        {
            "url": "仪表盘URL"
        }
    ]
}
```


<span id="_5-6-响应"></span>
## Response Parameters


|Parameter |Type |Sample value |Description |
|---|---|---|---|
|code |string |“aeolus/ok” |Return code. See [Error Codes](https://docs.byteplus.com/docs/DataWind/Visualization_-_Data_Subscription_Open_API#b3617d76) |
|data |object |*  |Data content |
|data.subscriptionId |int |1000 |Created subscription ID |
|msg |string |"Success" |Message |


<span id="_5-7-响应示例"></span>
## Response Example

```json
{
    "code": "aeolus/ok",
    "data": {
        "subscriptionId": 1000
    },
    "msg": "成功"
}
```


<span id="_6-删除订阅"></span>
# Delete Subscription

Used to batch delete dashboard subscriptions for which you have permission.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only subscriptions for which you have permission can be deleted. Project administrators and system administrators can delete any subscription. Dashboard administrators can delete subscriptions for their dashboards. Subscription owners can delete subscriptions they created.</div>


<span id="_6-1-请求"></span>
## Request Description


* Request Method: DELETE

* Request URL: `{{domain}}/aeolus/api/open/v2/subscription/subscriptions`


<span id="_6-4-body-参数"></span>
## Request Parameters


|Parameter |Type |Required |Sample value |Description |
|---|---|---|---|---|
|subscriptions |array[int] |Required |「1000, 1002」 |List of subscription IDs to be deleted. For details on how to obtain them, see **Get subscription list** |


<span id="_6-5-响应"></span>
## Response Parameters


|Name |Type |Example value |Description |
|---|---|---|---|
|code |string |“aeolus/ok” |Return code. For reference, see [Error Codes](https://docs.byteplus.com/docs/DataWind/Visualization_-_Data_Subscription_Open_API#b3617d76) |
|data |object |*  |Data content |
|data.deletedSubscriptions |array[int] |「1000, 1002」 |List of successfully deleted subscriptions |
|data.totalCount |int |1 |Total number of deleted subscriptions |
|msg |string |"Success" |Message |


<span id="_6-6-响应示例"></span>
## Response Example

```json
{
    "code": "aeolus/ok",
    "data": {
        "deletedSubscriptions": [
            10827
        ],
        "totalCount": 1
    },
    "msg": "成功"
}
```


<span id="_7-退订订阅"></span>
# Unsubscribe Subscription

Unsubscribe a specified user's subscription. Also supports unsubscribing all subscriptions by dashboard ID and unsubscribing a specific subscription by subscription ID.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only subscriptions with modify or delete permissions can be unsubscribed.</div>


<span id="_7-1-请求"></span>
## Request Description


* Request Method: DELETE

* Request URL: `{{domain}}/aeolus/api/open/v2/subscription/unsubscribe`


<span id="_7-4-body-参数"></span>
## Request Parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|subscriptions |array[int] |Required |「1000, 1002」 |List of subscription IDs to be unsubscribed. For details on how to obtain them, see **Get subscription list** |
|subscriber |string |Required |”xiaoming“ |The prefix of the recipient's email address, that is, the part before the `@` symbol in the email address. If the email address is `xiaoming@example.com`, then `subscriber` is `xiaoming`. |
|dashboardId |int |Optional |1 |The dashboard ID of the subscriptions to be unsubscribed. All subscriptions for this dashboard will be unsubscribed. For details on how to obtain it, see [How to Obtain Resource IDs](https://docs.byteplus.com/docs/DataWind/How_to_Obtain_Resource_IDs) |


<span id="_7-5-响应"></span>
## Response Parameters


|Parameter |Type |Example |Description |
|---|---|---|---|
|code |string |“aeolus/ok” |Return code. For reference, see [Error Codes](https://docs.byteplus.com/docs/DataWind/Visualization_-_Data_Subscription_Open_API#b3617d76) |
|data |object |*  |Data content |
|totalCount |int |5 |Number of deleted subscriptions |
|unsubscribedSubscriptions |array[int] |「1000, 1002」 |List of successfully unsubscribed subscriptions |
|msg |string |"Success" |Message |


<span id="_7-6-响应示例"></span>
## Response Example

```json
{
    "code": "aeolus/ok",
    "data": {
        "totalCount": 5,
        "unsubscribedSubscriptions": [
            10825
        ]
    },
    "msg": "成功"
}
```


<span id="c3bda0da"></span>
# Related References

<span id="b3617d76"></span>
## Error Codes


|Error code |Error message |Explanation |
|---|---|---|
|aeolus/ok |Success |Request succeeded |
|aeolus/validation/validationFailed |API parameter validation failed. Parameters do not meet the validation rules. |Request parameter error |
|aeolus/user/unauthorized |User does not have permission |User does not have the required resource permissions (dashboard, subscription) |
