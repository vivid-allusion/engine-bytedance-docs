---
title: "CreateApp"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-74487"
---

You have call CreateApp to create an RTC App location and get the AppID.

<span id="Requirements"></span>
## Requirements

Before proceeding, ensure that you have enabled the RTC service on the console, completed the authorization process, and selected the desired billing type.

<span id="HTTP request"></span>
## HTTP request


* Method：POST

* Endpoint：https://open.byteplusapi.com?Action=CreateApp&Version=2020\-12\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="Query"></span>
### Query


|**Parameter**  |**Data Type**  |**Required**  |**Sample Value**  |**Description**  |
|---|---|---|---|---|
|Action |String |Yes |`CreateApp` |Interface name. The value of this interface: `CreateApp` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="Body"></span>
### Body


|**Parameter**  |**Data Type**  |**Required**  |**Sample Value**  |**Description**  |
|---|---|---|---|---|
|AppName |String |Yes |`myApp` |Application name<br><br>Naming rule: string can only contain Chinese characters, English upper and lower case characters, numbers or underscores. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|AppId |String |`Your_AppId` |The only identifier for your audio & video app |
|AppKey |String |`Your_AppKey` |The AppKey used to generate a Token |
|Name |String |`myApp` |App Name |
|Owner |String |`Your_Owner` |Account ID |
|InstanceStatus |Integer |`1` |Service status. Possible values are `0`, `1`, `6`, and `98`:<br><br><br>* `0`: Creating \- AppID is initializing<br><br>* `1`: Running \- the current AppID is in operation<br><br>* `6`: Shut down due to overdue<br><br>* `98`: Disabled \- this AppId has been disabled by OpenAPI |
|CreateDate |String |`2021-08-17T17:48:41.973243689+08:00` |The date and time when the AppID was created |
|InstanceId |String |`Your_InstanceId` |Billing instance ID |


<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=CreateApp&Version=2020-12-01
{
    "AppName": "Your_AppName"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "CreateApp",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "AppId": "You****pId",
        "AppKey": "You****pKey",
        "Name": "Your_Name",
        "Owner": "1****0",
        "InstanceStatus": 1,
        "CreateDate": "2021-08-17T17:48:41.973243689+08:00",
        "InstanceId": "Your_InstanceId"
    }
}
```
