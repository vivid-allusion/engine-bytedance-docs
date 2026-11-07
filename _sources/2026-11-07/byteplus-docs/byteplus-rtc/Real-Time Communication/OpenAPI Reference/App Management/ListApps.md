---
title: "ListApps"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-74489"
---

After you created an app, you can query for information about the app that corresponds to an AppId. You can call `ListApps` to do this.

<span id="usage-scenario"></span>
## Usage scenario

You can call the OpenAPI of `ListApps` to get information about the apps created by the current account:


* If the parameter `AppId` is passed, the information of the `AppId` is queried (only one `AppId` is passed);

* If the parameter `AppId` is not passed, the information for all `AppId` under the current account is queried.


<span id="caution"></span>
## Caution

QPS must not exceed 20.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=ListApps&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListApps` |Interface name. The value of this interface: `ListApps` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |No |`You****pId` |The ID of the app you created |
|Reverse |Integer |No |`1` |`0`: Return in ascending order according to the time of App creation;<br><br>`1`: return in descending order according to the time of App creation.<br><br>It's default value is `0`. |
|Offset |String |No |`50` |The starting position of querying. |
|Limit |String |No |`100` |Page size.<br><br>The default is 50, and the maximum is 100. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Total |Integer |`10` |The number of apps queried |
|Offset |Integer |`50` |The starting position of querying. |
|Limit |Integer |`10` |The maximum of the number of return results |
|AppList |Array of [AppList](https://docs.byteplus.com/en/docs/12/14244#applist) |`-` |An array containing the details of the applications queried using the `ListApps` interface. |


<span id="applist"></span>
### AppList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|AppId |String |`You****pId` |Application ID |
|AppName |String |`myApp` |Application name |
|CreateAt |String |`2021-08-17T17:48:41.973243689+08:00` |The time when app is created. |
|Status |Integer |`1` |Service status.<br><br>`0` : Creating \- AppID is in initialization.<br><br>`1` : Running \- AppID is in normal service status.<br><br>`6` : App is disabled because of arrearage.<br><br>`98`: API is disabled by server. The current AppID is set to be unavailable |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=ListApps&Version=2020-12-01
{
    "AppId": "You****pId",
    "Reverse": "Your_Reverse",
    "Offset": "Your_Offset",
    "Limit": "Your_Limit"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "ListApps",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "AppList": [
            {
                "AppId": "You****pId",
                "AppName": "Your_Name",
                "CreateAt": "",
                "Status": 1
            }
        ],
        "Limit": 20,
        "Offset": 10,
        "Total": 1
    }
}
```


&nbsp;
