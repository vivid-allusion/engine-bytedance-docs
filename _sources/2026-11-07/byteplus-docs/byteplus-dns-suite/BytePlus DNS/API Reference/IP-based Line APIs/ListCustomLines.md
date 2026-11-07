---
title: "ListCustomLines"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-listcustomlines"
---

Get the list of IP\-based lines.

## Usage

* Rate limit: Maximum 1 call per second.

## Request

* Method: GET

* URL: https://dns.byteplusapi.com/?Action=ListCustomLines&Version=2018\-08\-01

## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListCustomLines` |The name of the API. The value of this parameter is `ListCustomLines`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|PageSize |Integer |No |`10` |The number of lines per page. BytePlus DNS will display the retrieved lines in pages. The number of pages is determined by the total number of retrieved lines and `PageSize`. The value range for this parameter is 1 to 500. The default value is `10`. |
|PageNumber |Integer |No |`1` |The page number. The API returns the lines contained in this page number. The default value is `1`. |
|Line |String |No |`custom-2811` |The ID of the IP\-based line. If you don't set this parameter, the API will not filter the query results based on this parameter. |
|NameCN |String |No |`test` |The name of the IP\-based line. If you don't set this parameter, the API will not filter the query results based on this parameter. |
|Remark |String |No |`remark` |The remark for the IP\-based line. If you don't set this parameter, the API will not filter the query results based on this parameter. |
|IPSegment |String |No |`192.168.1.0/24` |The CIDR address block of the IP\-based line. If you don't set this parameter, the API will not filter the query results based on this parameter. |

## Response body

### ResponseMetadata object

|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |

### Result Object

|Name |Type |Description |
|---|---|---|
|TotalCount |Integer |The total number of IP\-based lines returned. This parameter value is not affected by the `PageNumber` parameter. Suppose the specified `PageNumber` does not contain any lines. In this case, the `CustomerLines` parameter will not display any lines. However, `TotalCount` will still show the actual total number of lines retrieved by this API. |
|PageSize |Integer |The number of lines contained in each page. |
|PageNumber |Integer |The page number of the lines displayed in `CustomerLines`. |
|IPSegmentCount |Integer |The total number of CIDR address blocks added to the current BytePlus account. |
|CustomerLines |Object Array |List of IP\-based lines. |
|Line |String |The ID of the IP\-based line. |
|NameCN |String |The name of the IP\-based line. |
|Remark |String |The remark for the IP\-based line. |
|IPSegments |String[] |The CIDR address blocks included in the IP\-based line. |
|CreatedAt |String |The creation time of the IP\-based line. |
|UpdatedAt |String |The time when the IP\-based line was last updated. |

## Example

### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=ListCustomLines
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023041217295515273366212067046A34",
        "Action": "ListCustomLines",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "TotalCount": 1,
        "PageSize": 10,
        "PageNumber": 1,
        "IPSegmentCount": 1,
        "CustomerLines": [
            {
                "Line": "custom-2811",
                "NameCN": "test",
                "Remark": "test",
                "IPSegments": [
                    "192.168.1.0/24"
                ],
                "CreatedAt": "2023-03-21T16:53:29Z",
                "UpdatedAt": "2023-04-03T19:30:20Z"
            }
        ]
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
