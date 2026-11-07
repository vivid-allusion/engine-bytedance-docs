---
title: "ListQueryStats"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/ListQueryStats"
---

Gets DNS query statistics of an GTM instance.

The DNS query statistics can be grouped by DNS record type, ISP or geolocation.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=ListQueryStats&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/en/docs/36/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListQueryStats` |The name of the API. The value of this parameter is `ListQueryStats`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |
|GtmId |String |Yes |`GtmId` |The UUID of the BytePlus GTM instance. You can obtain the `GtmId` through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|Group |String |Yes |`all` |Group of the DNS query statistics.<br><br><br>* all: All DNS queries.<br><br><br> |
|PageNumber |Integer |No |`1` |The page number. Default is 1. The number of pages is determined by the total number of data items retrieved and the `PageSize`. |
|PageSize |Integer |No |`10` |The number of GTM instances per page. Default is 10. Maximum value is 500.<br><br>BytePlus GTM will display the data groups in pages. The number of pages is determined by the total number of data groups retrieved and the `PageSize`. |
|StartTime |Integer |No |`1639548697` |The start time. The format is Unix timestamp in seconds. For example, `1639548697`.<br><br>If you don't set this parameter, the start time defaults to three days ago. |
|EndTime |Integer |No |`1639548697` |The end time. The format is Unix timestamp in seconds. For example, `1639548697`.<br><br>If you don't set this parameter, the end time defaults to the current time. |
|SortOrder |String |No |`Desc` |The order of the results.<br><br><br>* Asc: Ascending order.<br><br>* Desc (default): Descending order. |
|SortBy |String |No |Total |The sorting key for the results:<br><br><br>* GroupName: Group name.<br><br>* Total (Default): Number of DNS queries. |

## Response

### ResponseMetadata object

|Name |Type |Description |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The API version. |
|Service |String |The service type. |
|Region |String |The region where the service is located. |

### Result object

|Name |Type |Description |
|---|---|---|
|Total |Integer |The total number of DNS queries. |
|PageSize |Integer |The number of DNS queries included on each page. |
|PageNumber |Integer |The page number where the grouped data is displayed in `Data`. |
|Data |JSON Object |Statistical data. |
|GroupName |String |The name of the group. |
|Total |Integer |Number of DNS queries. |
|Percent |Float |The percentage of the number of DNS queries of the current data group to the total number of DNS queries. 1 indicates 100%. |

## Example

### Request example

```HTTP
POST https://gtm.byteplusapi.com/?Action=ListQueryStats&GtmId=f3fac9ba-c7ed-******-65d44725768e&Group=all&StartTime=1733372558
```

### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "202412181107330AF089786DAC5F26BB55",
        "Action": "ListQueryStats",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Total": 1,
        "PageSize": 100,
        "PageNumber": 1,
        "Data": [
            {
                "GroupName": "www.example.com",
                "Total": 42,
                "Percent": 1
            }
        ]
    }
}
```
