---
title: "ListRecordDigestByLine"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-listrecorddigestbyline"
---

Gets a list of DNS records that use an IP\-based line.

## Usage

* Rate limit: Maximum 1 call per second.

## Request

* Method: GET

* URL: https://dns.byteplusapi.com/?Action=ListRecordDigestByLine&Version=2018\-08\-01

## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListRecordDigestByLine` |The name of the API. The value of this parameter is `ListRecordDigestByLine`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|Line |String |Yes |`custom-2811` |The ID of the IP\-based line. You can obtain the IDs of the IP\-based lines from the `Line` parameter returned by the [ListCustomLines API](https://docs.byteplus.com/byteplus-dns-suite/reference/listcustomlines). |

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
|Line |String |The ID of the IP\-based line. |
|RecordDigests |Array of Object |The list of DNS records using this IP\-based line. |
|Name |String |The domain name of the DNS record in FQDN format. |
|Type |String |The type of the DNS record. |
|LineNameCN |String |The name of the IP\-based line. |

## Example

### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=ListRecordDigestByLine&Line=custom-2811
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023041218332400277C0FD011B31816AA",
        "Action": "ListRecordDigestByLine",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "Line": "custom-2811",
        "RecordDigests": [
            {
                "Name": "example.com.",
                "Type": "A",
                "LineNameCN": "mycustomeline001"
            }
        ]
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
