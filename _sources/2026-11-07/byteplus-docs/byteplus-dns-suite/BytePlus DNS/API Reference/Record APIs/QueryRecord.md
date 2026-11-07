---
title: "QueryRecord"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-queryrecord"
---

Gets detailed information of a DNS record.

<span id="usage"></span>
## Usage


* Rate limit: 50 calls per second.


<span id="request"></span>
## Request


* Method: GET

* Address: https://dns.byteplusapi.com/?Action=QueryRecord?Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`QueryRecord` |The name of the API. The value of this parameter is `QueryRecord`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|RecordID |String |No |`3170534137672961176` |The ID of the DNS record. This parameter has the following instructions:<br><br><br>* If you specify the `RecordID`, you do not need to specify the `PQDN`, `Line`, `Type`, and `Value` parameters.<br><br>* If you do not specify the `RecordID`, you need to specify all of the `PQDN`, `Line`, `Type`, and `Value` parameters. |
|FQDN |String |No |`www.example.com.` |(Deprecated) The hostname of the DNS record. You can use the FQDN (Fully Qualified Domain Name) format (such as `www.example.com.`) or the PQDN (Partially Qualified Domain Name) format (such as `www.example.com`). |
|PQDN |String |No |`www.example.com` |The hostname of the DNS record. You can use the FQDN (Fully Qualified Domain Name) format (such as `www.example.com.`) or the PQDN (Partially Qualified Domain Name) format (such as `www.example.com`). |
|Line |String |No |`Default` |The line of the DNS record. The value of this parameter comes from:<br><br>The `Value` parameter returned by the [ListLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones).<br><br>The `Line` parameter returned by the [ListCustomLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listcustomlines).<br><br>The lines that can be configured for a domain depend on the [edition](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions) of that domain. |
|Type |String |No |`A` |The type of the DNS record. |
|Value |String |No |`1234` |The value of the DNS record. |


<span id="ea42b7da"></span>
## Response body

<span id="9458b6d4"></span>
### ResponseMetadata Object


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="d7b09ccf"></span>
### Result Object


|**Name** |**Type** |**Description** |
|---|---|---|
|RecordID |String |The ID of the DNS record. |
|FQDN |String |(Deprecated) The hostname included in the DNS record in PQDN (Partially Qualified Domain Name) format. For example, `www.example.com`. |
|PQDN |String |The hostname included in the DNS record in PQDN (Partially Qualified Domain Name) format. For example, `www.example.com`. |
|Host |String |The domain prefix included in the DNS record. If the value of this parameter is `@`, it represents the root domain itself. |
|Type |String |The type of the DNS record. |
|TTL |Integer |The expiration time of the DNS record in seconds. |
|Line |String |The line code corresponding to the DNS record. |
|Value |String |The value included in the DNS record. |
|Weight |Integer |The weight of the DNS record. |
|RecordSetID |String |The ID of the record set where the DNS record is located. Only A, AAAA, and CNAME types of DNS records have record sets. |
|Enable |Boolean |Whether the DNS record is enabled. This parameter can have the following values:<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. In this case, the DNS record is not included in DNS responses. |
|Tags |Array of String |The tag information of the DNS record. If the value of this parameter contains `GTMLock`, it indicates that the DNS record is associated with a GTM instance in BytePlus Global Traffic Management (GTM). |
|Remark |String |Remark of the record. |
|CreatedAt |String |The creation time of the DNS record. |
|UpdatedAt |String |The last update time of the DNS record. |
|Operators |String[] |The ID of the account that last updated the DNS record. If the DNS record was updated by an IAM account, the value of this parameter is the ID of the IAM account. |


<span id="514e78ac"></span>
## Example

<span id="128d6805"></span>
### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=QueryRecord&RecordID=3170534137672596377
```


<span id="03fe09cd"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023052416510645D0D3D35334AD2EA31D",
        "Action": "QueryRecord",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "RecordID": "3170534137672961176",
        "FQDN": "www.example.com",
        "PQDN": "www.example.com",
        "Host": "www",
        "Type": "A",
        "TTL": 600,
        "Line": "default",
        "Value": "***.***.***.***",
        "Weight": 1000,
        "RecordSetID": "MzE3MDUzNDEzNzY2OTA5ODc5OHx0ZXN0MDIyLnlhbWFzaXRlLnRvcC58QXxkZWZhdWx0",
        "Enable": true,
        "Tags": [],
        "Remark": "",
        "CreatedAt": "2023-05-24T16:50:31Z",
        "UpdatedAt": "2023-05-24T16:50:31Z",
        "Operators": [
            "21xxxxxx1"
        ]
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
