---
title: "ListRecordSets"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-listrecordsets"
---

Gets a list of DNS record sets of a domain.

## Usage

* Rate limit: Maximum 50 calls per second.

## Request

* Method: GET

* URL: https://dns.byteplusapi.com/?Action=ListRecordSets&Version=2018\-08\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListRecordSets` |The name of the API. The value of this parameter is `ListRecordSets`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|ZID |Integer |Yes |`1376` |The domain ID. |
|PageSize |Integer |No |`10` |The number of DNS record sets per page.<br><br>The system will display the retrieved DNS record sets in pages. The number of pages is determined by the total number of retrieved DNS record sets and `PageSize`.<br><br>The default value of this parameter is `10`, and the maximum value is `500`. |
|PageNumber |Integer |No |`1` |The page number. The API returns the DNS record sets contained in this page number. The default value of this parameter is `1`. |
|SearchMode |String |No |`like` |The matching mode for `Host`. This parameter has the following values:<br><br><br>* `like` (default): Fuzzy matching.<br><br>* `exact`: Exact matching. |
|Host |String |No |`@` |The domain prefix of the record set. If the value of this parameter is `@`, it represents the second\-level domain itself. If you don't set this parameter, the API won't filter the query results based on this parameter. |
|RecordSetID |String |No |`MzE3MDUzNDEzNzY2OTA5ODc5OHxALnlhbWFzaXRlLnRvcC58QXxkZWZhdWx0` |The record set ID. DNS records in a record set have the same domain name, domain prefix, line, and type. If you don't set this parameter, the API won't filter the query results based on this parameter. |

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
|TotalCount |Integer |The total number of DNS record sets returned. This parameter value is not affected by the `PageNumber` parameter.<br><br> <br><br>If the specified `PageNumber` does not contain any DNS record sets, the `RecordSets` parameter will not display any DNS record sets. However, `TotalCount` will still show the actual total number of DNS record sets retrieved by this API. |
|PageSize |Integer |The number of DNS record sets contained in each page. |
|PageNumber |Integer |The page number where the DNS record sets displayed in `RecordSets` are located. |
|RecordSets |Array of Objects |Represents a list of DNS record sets. |
|ID |String |The ID of the DNS record set. |
|FQDN |String |(Deprecated) The domain prefix contained in the DNS record set, in PQDN (Partially Qualified Domain Name) format. For example, www.example.com. |
|PQDN |String |The domain prefix contained in the DNS record set, in PQDN (Partially Qualified Domain Name) format. For example, www.example.com. |
|Host |String |The host record contained in the DNS record set. If the value of this parameter is `@`, it represents the second\-level domain itself. |
|Type |String |The type of DNS records in the DNS record set. |
|Line |String |The line code corresponding to the DNS record set. |
|WeightEnabled |Boolean |Indicates whether load balancing is enabled for the DNS record set. If load balancing is enabled, BytePlus DNS will return DNS resolution results based on the weight of the DNS records. This parameter has the following values:<br><br><br>* `true`: Indicates that load balancing is enabled.<br><br>* `false`: Indicates that load balancing is not enabled. |

## Example

### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=ListRecordSets&ZID=1376&Host=mg
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230412153500E9CB7CBCE69BE15F449A",
        "Action": "ListRecordSets",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "TotalCount": 4,
        "PageNumber": 1,
        "PageSize": 1,
        "RecordSets": [
            {
                "ID": "MzE3MDUzNDEzNzY2OTA5ODc5OHxALnlhbWFzaXRlLnRvcC58QXxkZWZhdWx0",
                "FQDN": "@.example.com",
                "PQDN": "@.example.com",
                "Host": "@",
                "Type": "A",
                "Line": "default",
                "WeightEnabled": false
            }
        ]
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
