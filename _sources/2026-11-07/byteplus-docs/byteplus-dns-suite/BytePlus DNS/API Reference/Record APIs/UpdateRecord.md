---
title: "UpdateRecord"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-updaterecord"
---

Updates a DNS record.

<span id="usage"></span>
## Usage


* Rate limit: 10 calls per second.


<span id="request"></span>
## Request


* Method: POST

* Address: https://dns.byteplusapi.com/?Action=UpdateRecord?Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdateRecord` |The name of the API. The value of this parameter is `UpdateRecord`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|RecordID |String |Yes |`3170534137672596377` |The ID of the DNS record to be updated. |
|Host |String |Yes |`@` |The domain prefix of the subdomain. If you need to update the DNS record for the root domain, set this parameter to `@`. For example, `@.example.com` represents `example.com`. |
|Line |String |Yes |`Default` |The line corresponding to the DNS record. The value of this parameter comes from:<br><br>The `Value` parameter returned by the [ListLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones).<br><br>The `Line` parameter returned by the [ListCustomLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listcustomlines).<br><br>The lines that can be configured for a domain depend on the [edition](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions) of that domain. |
|TTL |Integer |No |`600` |The Time\-To\-Live (TTL) of the DNS record, in seconds. If you don't set this parameter, its value remains unchanged. |
|Type |String |No |`A` |The record type. For information about different types of records, see [Supported DNS Record Types](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-dns-record-types). The value of this parameter can be:<br><br><br>* `A`: A record.<br><br>* `AAAA`: AAAA record.<br><br>* `CNAME`: CNAME record.<br><br>* `NS`: NS record.<br><br>* `MX`: MX record.<br><br>* `SRV`: SRV record.<br><br>* `TXT`: TXT record.<br><br>* `CAA`: CAA record.<br><br><br>If you don't set this parameter, its value remains unchanged. |
|Value |String |No |`1.1.1.1` |The value of the DNS record. For the format of record values for different types of records, see [Supported DNS Record Types](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-supported-dns-record-types). If you don't set this parameter, its value remains unchanged. |
|Weight |Integer |No |`1` |The weight of the DNS record. See [Editions](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-editions) for weight limitations.<br><br>The weight is only effective when load balancing is enabled for the record set to which the DNS record belongs. See [UpdateRecordSet API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-updaterecordset).<br><br>If you don't set this parameter, its value remains unchanged. |
|Remark |String |No |`Remark` |The remark for the DNS record. It supports UTF\-8 encoding and can be up to 255 characters long. If you don't set this parameter, its value remains unchanged. |


<span id="1f288c04"></span>
## Response body

<span id="f946fec4"></span>
### ResponseMetadata object


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="a00d9ea4"></span>
### Result object


|**Name** |**Type** |**Description** |
|---|---|---|
|RecordID |String |The ID of the DNS record. |
|FQDN |String |(Deprecated) The fully qualified domain name (FQDN) included in the DNS record in PQDN (Partially Qualified Domain Name) format. For example, `www.example.com`. |
|PQDN |String |The partially qualified domain name (PQDN) included in the DNS record. For example, `www.example.com`. |
|Host |String |The domain prefix included in the DNS record. If the value of this parameter is `@`, it represents the root domain itself. |
|Type |String |The type of the DNS record. |
|TTL |Integer |The expiration time of the DNS record in seconds. |
|Line |String |The line corresponding to the DNS record. The value of this parameter comes from:<br><br><br>* The `Value` parameter returned by the [ListLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones).<br><br>* The `Line` parameter returned by the [ListCustomLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listcustomlines).<br><br><br> |
|Value |String |The value included in the DNS record. |
|Weight |Integer |The weight of the DNS record. |
|RecordSetID |String |The ID of the record set where the DNS record is located. Only A, AAAA, and CNAME record types have record sets. |
|Enable |Boolean |Whether the DNS record is enabled. This parameter can have the following values:<br><br><br>* `true`: Enabled.<br><br>* `false`: Disabled. In this case, the DNS record is not effective. |
|Tags |Array of String |The tag information of the DNS record. If the value of this parameter contains `GTMLock`, it indicates that the DNS record is associated with a GTM instance in BytePlus Global Traffic Management (GTM). |
|Remark |String |Remark of the record. Supports UTF\-8 encoding. The length should not exceed 16 characters. |
|CreatedAt |String |The creation time of the DNS record. |
|UpdatedAt |String |The time when the DNS record was updated after calling this API. |
|Operators |String[] |The account ID that called this API. If the API is called by an IAM account, the value of this parameter is the ID of the IAM account. |


<span id="911f14dc"></span>
## Example

<span id="ea1a0447"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=UpdateRecord
{
  "Host": "@",
  "Line": "default",
  "RecordID": "3170534137672596377",
  "TTL": 600,
  "Type": "A",
  "Value": "***.***.***.***",
  "Weight": 1
}
```


<span id="05cbf1c5"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202407010850594B11F267786D8300200B",
        "Action": "UpdateRecord",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "RecordID": "3170534137673489320",
        "FQDN": "test.example.com",
        "PQDN": "test.example.com",
        "Host": "test",
        "Type": "A",
        "TTL": 600,
        "Line": "default",
        "Value": "***.***.***.***",
        "Weight": 1,
        "RecordSetID": "MzE3MDUzNDEzNzY2OTI1MjM0MHx0ZXN0LnRlc3QxMjMuY29tLnxBfGRlZmF1bHQ=",
        "Enable": true,
        "Tags": [],
        "Remark": "",
        "CreatedAt": "2024-07-01T08:51:01Z",
        "UpdatedAt": "2024-07-01T08:51:01Z",
        "Operators": [
            "30xxxxxx32"
        ]
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
