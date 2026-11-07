---
title: "GetAdvertisementDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getadvertisementdataapi"
---

Gets the marketing data for a live\-streaming activity. The data is updated every five minutes.

<span id="d4dafd6e"></span>
## Request

<span id="9623f49a"></span>
### Details


* API operation: `GetAdvertisementDataAPI`

* Request method: GET

* Request URI: `http://livesaas.byteplusapi.com/?Action=GetAdvertisementDataAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="be58fd4e"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. |
|Version |String |Yes |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Integer |Yes |The ID of the live\-streaming activity. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi). |
|Source |Integer |No |Specifies the source of the data to return. Default value: `0`.<br><br>Valid values:<br><br><br>* `-1`: Returns data from all addresses.<br><br>* `0`: Returns data from the default address only.<br><br>* `1`: Returns data from address A only.<br><br>* `2`: Returns data from address B only.<br><br>* `3`: Returns data from address C only.<br><br>* `4`: Returns data from address D only. |


<span id="f1bb0c6c"></span>
### Sample request

```JSON
Get http://livesaas.byteplusapi.com/?Action=GetAdvertisementDataAPI&Version=2020-06-01&ActivityId=1231231231&Source=0
```


<span id="ff6e95c8"></span>
## Response

<span id="6d62ca05"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|ActivityId |Integer |The ID of the live\-streaming activity. |
|AccountClicks |[ClicksStruct](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi#ClicksStruct) |Click data for the brand account. |
|AdvertisingClicks |[ClicksStruct](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi#ClicksStruct) |Click data for advertisements. |
|AdInfo |Array of [AdInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getadvertisementdataapi#AdInfo) |Detailed data for advertisements. |
|ShowThumbUpNumber |Integer |The virtual number of likes for the live\-streaming activity, which is displayed on the viewing page. |
|ActualThumbUpNumber |Integer |The actual number of likes for the live\-streaming activity. |


<span id="b664a990"></span>
#### ClicksStruct


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|PV |Integer |Page views. |
|UV |Integer |Unique visitors. |
|TotalTime |Integer |Deprecated. |


<span id="f8766d4b"></span>
#### AdInfo


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|PageAdvertiseType |Integer |Indicates the type of advertisement.<br><br>Valid values:<br><br><br>* `1`: Header ads.<br><br>* `2`: In\-page ads.<br><br>* `3`: Floating ads.<br><br>* `4`: Product card ads. |
|Content |String |The content of the advertisement. |
|Link |String |The link for the advertisement. |
|Title |String |The title of the advertisement. |
|PV |Integer |Page views of the advertisement. |
|UV |Integer |Unique visitors of the advertisement. |


<span id="d7e7b340"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetAdvertisementDataAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1681977443
    },
    "Result": {
        "ActivityId": 1231231231,
        "AccountClicks": {
            "PV": 6,
            "UV": 2,
            "TotalTime": 0
        },
        "AdvertisingClicks": {
            "PV": 6,
            "UV": 1,
            "TotalTime": 0
        },
        "AdInfo": [
            {
                "PageAdvertiseType": 3,
                "Content": "//p16-live-sg.ibyteimg.com/xxx/xxx-image.image",
                "Link": "www.example.com",
                "PV": 1,
                "UV": 1,
                "Title": ""
            },
            {
                "PageAdvertiseType": 1,
                "Content": "",
                "Link": "www.example.com",
                "PV": 1,
                "UV": 1,
                "Title": ""
            },
            {
                "PageAdvertiseType": 2,
                "Content": "//p16-live-sg.ibyteimg.com/xxx/xxx-image.image",
                "Link": "www.example.com",
                "PV": 0,
                "UV": 0,
                "Title": ""
            },
            {
                "PageAdvertiseType": 4,
                "Content": "//p16-live-sg.ibyteimg.com/xxx/xxx-image.image",
                "Link": "www.example.com",
                "PV": 3,
                "UV": 1,
                "Title": "Product A"
            }
        ],
        "ShowThumbUpNumber": 30,
        "ActualThumbUpNumber": 20
    }
}
```


<span id="7155c925"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
