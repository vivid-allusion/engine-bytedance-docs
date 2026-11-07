---
title: "UpdateFloatingAdvertisementAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateFloatingAdvertisement"
---

Call `UpdateFloatingAdvertisementAPI` to update the status, link, and other configuration details of a floating advertisement in a specified live room.

<span id="Requirements"></span>
## Requirements


* Quota: 10 queries per second per account.

* Prerequisite: A BytePlus account or an IAM user with **Marketing toolkits** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=UpdateFloatingAdvertisementAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdateFloatingAdvertisementAPI` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="Body parameters"></span>
### Body parameters


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ActivityId |Long |Yes |1798615803\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|IsEnable |Integer |No |`1` |Specifies whether to enable the floating ad. Supports the following values; the default value is `0`.<br><br><br>* `0`: Disable<br><br>* `1`: Enable |
|ImageUrl |String |No |https://p.example.org/6ed59yyum2\-z75.png |Floating ad image URL. The address must include the https protocol header.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when you first configure the floating ad using this API.</div><br> |
|HomeUrl |String |No |`https://example.com` |The embedded link for the floating ad must include the https protocol header. |
|IsCloseEnable |Integer |No |`1` |Specifies whether the audience can close the floating ad. Supports the following values; the default is `0`.<br><br><br>* `0`: The ad can be closed<br><br>* `1`: The ad cannot be closed |
|EnableFloating |Boolean |No |true |Specifies whether to enable floating display. Supports the following values; the default value is `false`.<br><br><br>* `true`: When set to `true`, clicking the floating ad expands it on the current live stream page, allowing the audience to view the ad while watching the live stream. This option only takes effect on the mobile viewing page.<br><br>* `false`: When set to `false`, clicking the floating ad opens a new browser tab to display the ad. As a result, the audience cannot watch the live stream and the ad at the same time. |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Status |Boolean |`true` |Returns `true` if the configuration was updated successfully. |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateFloatingAdvertisementAPI&Version=2023-08-01
{
    "ActivityId": 1798615803****,
    "ImageUrl": "https://p.example.org/6ed59yyum2-z75.png",
    "HomeUrl": "https://example.com",
    "IsCloseEnable": 1,
    "IsEnable": 1,
    "EnableFloating": true
}
```


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateFloatingAdvertisementAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true
    }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
