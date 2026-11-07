---
title: "ListZoneStatistics"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-listzonestatistics"
---

Lists the number of DNS queries for specified root domains. The statistics include the DNS queries for the root domain and all subdomains. There may be a delay in the statistics of DNS queries in the last hour. In general, the delay is up to one hour.

## Usage

Rate limit: Maximum 5 calls per second.

## Request

* Method: GET

* URL: https://dns.byteplusapi.com/?Action=ListZoneStatistics&Version=2018\-08\-01

## Request method

GET

## Rate limit

Maximum 5 calls per second.

## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

### Query

|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListZoneStatistics` |The name of the API. The value of this parameter is `ListZoneStatistics`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|Name |String |No |`example.com` |The domain name for which you want to count DNS queries, or a keyword contained in the domain name. BytePlus DNS determines these domains based on `Name` and `SearchMode`, and counts DNS queries for each domain. |
|PageSize |Integer |No |`10` |The number of domain names per page. The system displays the statistics of the domains in pages. The number of pages is determined by the total number of domains being counted and the `PageSize`. The default value of this parameter is `10`, and the maximum value is `500`. |
|PageNumber |Integer |No |`1` |The page number. The API returns the statistical data for each domain name on this page. The default value of this parameter is `1`. |
|SearchMode |String |No |`like` |The matching mode for `Name`. This parameter has the following values:<br><br><br>* `like` (default): Indicates fuzzy matching.<br><br>* `exact`: Indicates exact matching. |
|Start |Integer |No |`1639540000` |The start time of the statistics period. The format is Unix timestamp (seconds). If you do not specify the `Start` parameter, the default statistics period starts from 3 days before the time you call the API. For example, if you call this API at 14:00:00 on June 8, 2023, the default statistics period is from 14:00:00 on June 5, 2023, to 14:00:00 on June 8, 2023. |
|End |Integer |No |`1639550000` |The end time of the statistics period. The format is Unix timestamp (seconds). If you do not specify the `End` parameter, the default statistics period ends at the time you call the API. |
|Threshold |Integer |No |`100` |The threshold for the number of requests. If you specify this parameter, the API filters out domain names with a number of requests greater than this parameter. |
|SearchOrder |String |No |`asc` |The order of the query results.<br><br><br>* asc: Ascending order.<br><br>* desc: (Default) Descending order. |
|OrderKey |String |No |`Total` |The key value for sorting the query results.<br><br><br>* ZoneName: (Default) Sort by the value of the `ZoneName` parameter.<br><br>* Total: (Default) Sort by the value of the `Total` parameter. |

## Response body

### ResponseMetadata object

|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |

### Result object

|Name |Type |Description |
|---|---|---|
|Total |Integer |The total number of returned domain names. This parameter value is not affected by the `PageNumber` parameter. Suppose the `PageNumber` you specified does not contain any domain names. In this case, the `Data` parameter will not display statistical data for any domain names. However, `TotalCount` will still show the actual total number of domain names counted by this API. |
|PageSize |Integer |The number of domain names contained in each page. |
|PageNumber |Integer |The page number of the domain names displayed in `Data`. |
|Data |Array of Objects |The list of domain names. |
|Name |String |A root domain. |
|Timestamp |Integer |This parameter has no practical meaning for this API. You can ignore it. |
|Success |Integer |Indicates the number of successful DNS resolutions for this root domain and its subdomains within the specified time period. |
|NotExists |Integer |Indicates the number of times the DNS resolution response for this root domain and its subdomains was `NXDOMAIN` within the specified time period. `NXDOMAIN` means the domain name does not exist. A common reason is that the domain name has no corresponding DNS record. |
|Error |Integer |Indicates the number of internal errors that occurred while BytePlus DNS was processing DNS queries within the specified time period. |
|Total |Integer |Indicates the number of DNS queries for this root domain and its subdomains within the specified time period. |
|ZID |Integer |Indicates the ID of the domain. |
|CacheStage |Integer |Indicates the status of the domain itself. This parameter has the following values:<br><br><br>* `0`: Indicates that you are the owner of the domain.<br><br>* `1`: Indicates that you are not the owner of the domain. You can call the [RetrieveZone API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-retrievezone) to retrieve the domain. |

## Example

### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=ListZoneStatistics&Threshold=100&Start=1639540000&End=1639550000
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20211215192232010225243153052A63E3",
        "Action": "ListZoneStatistics",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "Total": 2,
        "Data": [
            {
                "Timestamp": 0,
                "Success": 1610,
                "NotExists": 0,
                "Error": 0,
                "Total": 1610,
                "Name": "******.com.",
                "ZID": 839,
                "CacheStage": 0
            },
            {
                "Timestamp": 0,
                "Success": 1605,
                "NotExists": 0,
                "Error": 0,
                "Total": 1605,
                "Name": "******.com.",
                "ZID": 841,
                "CacheStage": 0
            }
        ]
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
