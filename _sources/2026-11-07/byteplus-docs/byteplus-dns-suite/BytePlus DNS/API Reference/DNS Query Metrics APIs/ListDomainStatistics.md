---
title: "ListDomainStatistics"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-listdomainstatistics"
---

Statistics of DNS queries for subdomains.

There may be a delay in the statistics of DNS queries for the most recent hour. Typically, the maximum delay is 1 hour.

## Usage

* Rate limit: Maximum 5 calls per second.

* Edition limit: This API cannot provide statistics for domains of the free edition.

## Request

* Method: GET

* URL: https://dns.byteplusapi.com/?Action=ListDomainStatistics&Version=2018\-08\-01

## Request Parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListDomainStatistics` |The name of the API. The value of this parameter is `ListDomainStatistics`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|ZID |Integer |Yes |`1234` |The ID of the root domain. BytePlus DNS will provide statistics for subdomains under this root domain. |
|Name |String |No |`www.example.com` |The subdomain for which request statistics are needed, or a keyword contained in the subdomain. BytePlus DNS determines these subdomains based on `Name` and `SearchMode`, and provides DNS query statistics for each subdomain. If you don't specify this parameter, statistics will be provided for all subdomains. |
|PageSize |Integer |No |`10` |The number of subdomains included on each page. The system will display the statistics of subdomains in pages. The number of pages is determined by the total number of subdomains being analyzed and `PageSize`. The default value of this parameter is `10`, and the maximum value is `500`. |
|PageNumber |Integer |No |`1` |The page number. The API returns statistical data for each subdomain included on this page. The default value of this parameter is `1`. |
|SearchMode |String |No |`like` |The matching mode for `Name`. This parameter has the following values:<br><br><br>* `like` (default): Fuzzy matching.<br><br>* `exact`: Exact matching. |
|Start |Integer |No |`1639540000` |The start time of the statistical period. The format is Unix timestamp (seconds). If you don't specify the `Start` parameter, the default statistical period starts from 3 days before the time you call the API. For example, if you call this API at 14:00:00 on June 8, 2023, the default statistical period would be from 14:00:00 on June 5, 2023, to 14:00:00 on June 8, 2023. |
|End |Integer |No |`1639550000` |The end time of the statistical period. The format is Unix timestamp (seconds). If you don't specify the `End` parameter, the default statistical period ends at the time you call the API, starting from the `Start` time. |
|Threshold |Integer |No |`100` |The threshold for the number of requests. If you specify this parameter, the API will filter out subdomains with a number of requests greater than this parameter. |

## Response body

### ResponseMetadata object

|Name |Type |Description |
|---|---|---|
|Total |Integer |The total number of returned subdomains. This parameter value is not affected by the `PageNumber` parameter. Suppose the `PageNumber` you specified does not include any subdomains. In this case, the `Data` parameter will not display statistical data for any subdomains. However, `TotalCount` will still show the actual total number of subdomains analyzed by this API. |
|PageSize |Integer |The number of subdomains included in each page. |
|PageNumber |Integer |The page number of the subdomains displayed in `Data`. |
|Data |Array of Objects |The list of subdomains. |
|Name |String |A subdomain being analyzed. |
|Timestamp |Integer |This parameter has no practical significance for this API. You can ignore it. |
|Success |Integer |The number of successful DNS resolutions for the subdomain within the specified time period. |
|NotExists |Integer |The number of times the DNS resolution response for the subdomain was `NXDOMAIN` within the specified time period. `NXDOMAIN` indicates that the subdomain does not exist. A common reason is that the subdomain has no corresponding DNS record. |
|Error |Integer |The number of internal errors that occurred while BytePlus DNS was processing resolution requests within the specified time period. |
|Total |Integer |The number of DNS queries for the subdomain within the specified time period. |
|ZID |Integer |This parameter has no practical significance for this API. You can ignore it. |
|CacheStage |Integer |This parameter has no practical significance for this API. You can ignore it. |

## Example

### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=ListDomainStatistics&ZID=1376&Threshold=100&Start=1639540000&End=1639550000
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2021121519272101022511001100278B8B",
        "Action": "ListDomainStatistics",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "Page": 1,
        "Size": 10,
        "Total": 1,
        "Data": [
            {
                "Timestamp": 0,
                "Success": 1607,
                "NotExists": 0,
                "Error": 0,
                "Total": 1607,
                "Name": "img.test3.com.",
                "ZID": 0,
                "CacheStage": 0
            }
        ]
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
