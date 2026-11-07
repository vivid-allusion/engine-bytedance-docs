---
title: "ModifyAppStatus"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-74488"
---

After you have created an app, you can enable or disable the app. You can call the `ModifyAppStatus` OpenAPI to do this.

<span id="usage-scenario"></span>
## Usage scenario

You can call `ModifyAppStatus` to enable or disable the App corresponding to the AppId.


* Enable: Normal state, the default state for newly created AppID.

* Disable: current AppID function is not available" means that the basic functions and value\-added functions of RTC are not available. For example the user can not join the room. cloud media processing can not be turned on.

> Whether the current AppID is enabled or disabled, the information on AppID is always displayed on the console.


<span id="requirements"></span>
## Requirements

QPS must not exceed 20.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=ModifyAppStatus&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ModifyAppStatus` |Interface name. The value of this interface: `ModifyAppStatus` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app. |
|Status |Integer |Yes |`1` |`1` : Set App Status to Enable;<br><br>&nbsp;<br><br>`2` : Set App Status to disable |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "success" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=ModifyAppStatus&Version=2020-12-01
{
    "AppId": "You****pId",
    "Status": 1
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "ModifyAppStatus",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "message": "success"
    }
}
```


&nbsp;
