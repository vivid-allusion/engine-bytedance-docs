---
title: "ListRecords"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-listrecords"
---

Gets the list of DNS records of a domain.

## Usage

* Rate limit: 100 calls per second.

## Request

* Method: GET

* Address: https://dns.byteplusapi.com/?Action=ListRecords?Version=2018\-08\-01

## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListRecords` |The name of the API. The value of this parameter is `ListRecords`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|ZID |Integer |Yes |`304092` |The ID of the domain. You can call the [ListZones API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones) to get the domain ID. |
|PageSize |Integer |No |`10` |The number of DNS records to be included per page. The retrieved DNS records are displayed in pages. The number of pages is determined by the total number of DNS records retrieved and the `PageSize` value. The default value of this parameter is `10`, and the maximum value is `500`. |
|PageNumber |Integer |No |`1` |The page number. The API will return the DNS records included in this page. The default value of this parameter is `1`. |
|SearchOrder |String |No |`asc` |The Method to sort the returned list of DNS records. The field used for sorting is the creation time of the DNS records. This parameter can have the following values:<br><br><br>* `asc`(Default): Sort in ascending order.<br><br>* `desc`: Sort in descending order. |
|SearchMode |String |No |`like` |The matching mode for the `Host` parameter. This parameter can have the following values:<br><br><br>* `like`(Default): Fuzzy matching.<br><br>* `exact`: Exact matching. |
|Host |String |No |`@` |Domain prefix of the DNS record. If the value of this parameter is `@`, it represents the root domain itself. |
|Line |String |No |`Default` |Line of the DNS record. The value of this parameter comes from:<br><br>The `Value` parameter returned by the [ListLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones).<br><br>The `Line` parameter returned by the [ListCustomLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listcustomlines).<br><br>The lines that can be configured for a domain depend on the [edition](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions) of that domain. |
|Type |String |No |`A` |Type of the DNS record. |
|Value |String |No |`1.1.1.1` |Value of the DNS record. |

## Response body

### ResponseMetadata Object

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
|TotalCount |Integer |The total number of DNS records returned. This parameter value is not affected by the `PageNumber` parameter. If the specified `PageNumber` does not contain any DNS records, the `Records` parameter will not display any DNS records. However, `TotalCount` will still show the actual total number of DNS records retrieved by this API. |
|PageSize |Integer |The number of DNS records contained in each page. |
|PageNumber |Integer |The page number of the DNS records displayed in `Records`. |
|Records |Array of Objects |A list of DNS records. |
|RecordID |String |The ID of the DNS record. |
|FQDN |String |(Deprecated) The hostname included in the DNS record, in PQDN (Partially Qualified Domain Name) format. For example, www.example.com. |
|PQDN |String |The hostname included in the DNS record, in PQDN (Partially Qualified Domain Name) format. For example, www.example.com. |
|Host |String |The host record included in the DNS record. If the value of this parameter is `@`, it represents the second\-level domain itself. |
|Type |String |The type of the DNS record. |
|TTL |Integer |The Time to Live (TTL) of the DNS record. The unit is seconds. |
|Line |String |The line code corresponding to the DNS record. |
|Value |String |The record value contained in the DNS record. |
|Weight |Integer |The weight of the DNS record. |
|RecordSetID |String |The ID of the record set to which the DNS record belongs. Only A, AAAA, and CNAME type DNS records have record sets. |
|Enable |Boolean |Indicates whether the DNS record is enabled. This parameter has the following values:<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. In this case, the DNS record is not included in DNS responses. |
|Tags |Array of String |The tag information of the DNS record. If the value of this parameter contains `GTMLock`, it indicates that the DNS record is associated with a GTM instance in BytePlus Global Traffic Management (GTM). |
|Remark |String |The remark of the DNS record. |
|CreatedAt |String |The creation time of the DNS record. |
|UpdatedAt |String |The time when the DNS record was last updated. |
|Operators |String[] |Indicates the ID of the BytePlus account that last updated the DNS record. If an IAM account updated the DNS record, the value of this parameter is the ID of the IAM account. |

## Example

### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=ListRecords&Version=2018-08-01&ZID=304092&PageSize=1
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230412142536C2B75D467F4E3722AAE6",
        "Action": "ListRecords",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "TotalCount": 15,
        "PageNumber": 1,
        "PageSize": 1,
        "Records": [
            {
                "RecordID": "3170534137670303887",
                "FQDN": "www.example.com",
                "PQDN": "www.example.com",
                "Host": "www",
                "Type": "A",
                "TTL": 600,
                "Line": "default",
                "Value": "***.***.***.***",
                "Weight": 1,
                "RecordSetID": "MzE3MDUzNDEzNzY2OTA5ODc5OHx3d3cueWFtYXNpdGUudG9wLnxBfGRlZmF1bHQ=",
                "Enable": true,
                "Tags": [],
                "Remark": "",
                "CreatedAt": "2022-11-09T10:05:08Z",
                "UpdatedAt": "2022-11-09T10:05:08Z",
                "Operators": [
                    "2100xxxx011"
                ]
            }
        ]
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
