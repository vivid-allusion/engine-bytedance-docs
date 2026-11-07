---
title: "GetActivityMenuAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivitymenuapi"
---

This API is used to get the list of menus in a live room. The response includes the name, type, and display order of each menu.

<span id="11f1c7f4"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="efb823e7"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetActivityMenuAPI&Version=2020-06-01`

* Method: GET


<span id="4436b24c"></span>
## Request parameters

Not all shared request parameters are included in the following table. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Request"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetActivityMenuAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`178398113630****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="37718e59"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Menu |Array of [Menu](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi#d6851f47) |`-` |An array of menu objects. |


<span id="d6851f47"></span>
### Menu


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`Chat` |The menu name. |
|Type |Integer |`3` |The menu type.<br><br><br>* `1`: Graphics.<br><br>* `2`: Product cards.<br><br>* `3`: Chat interaction.<br><br>* `4`: Interaction tools.<br><br>* `5`: Aggregated live streams.<br><br>* `6`: Q&A.<br><br>* `7`: Embedded link. |
|Location |Integer |`1` |The display order of the menu. The value starts from `1`. |


<span id="abfcc133"></span>
## Samples

<span id="951902d9"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityMenuAPI&Version=2020-06-01&ActivityId=178398113630****
```


<span id="f7900aaf"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityMenuAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1714653986
    },
    "Result": [
        {
            "Name": "Chat",
            "Type": 3,
            "Location": 1
        },
        {
            "Name": "Interactions",
            "Type": 4,
            "Location": 2
        }
    ]
}
```


<span id="9d6706a4"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
