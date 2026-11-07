---
title: "UpdateRecordStatus"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-updaterecordstatus"
---

Enables or disables a DNS record.

<span id="usage"></span>
## Usage


* Rate limit: 10 calls per second.


<span id="request"></span>
## Request


* Method: POST

* Address: https://dns.byteplusapi.com/?Action=UpdateRecordStatus?Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdateRecordStatus` |The name of the API. The value of this parameter is `UpdateRecordStatus`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|RecordID |String |Yes |`3170534137672596377` |The ID of the DNS record. |
|Enable |Boolean |No |`true` |Whether to enable the DNS record. This parameter can have the following values:<br><br><br>* `true`: Enable the DNS record.<br><br>* `false`: Disable the DNS record. |


<span id="3e8bbaaf"></span>
## Response body

<span id="bdaba663"></span>
### ResponseMetadata Object


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="dca0dfc0"></span>
### Result Object


|**Name** |**Type** |**Description** |
|---|---|---|
|RecordID |String |The ID of the DNS record. |
|FQDN |String |(Deprecated) The fully qualified domain name (FQDN) included in the DNS record in PQDN (Partially Qualified Domain Name) format. For example, `www.example.com`. |
|PQDN |String |The partially qualified domain name (PQDN) included in the DNS record in PQDN format. For example, `www.example.com`. |
|Host |String |The domain prefix included in the DNS record. If the value of this parameter is `@`, it represents the root domain itself. |
|Type |String |The type of the DNS record. |
|TTL |Integer |The time to live (TTL) of the DNS record in seconds. |
|Line |String |The line code corresponding to the DNS record. You can call the [ListLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listlines) to get the line names corresponding to the values of this parameter. |
|Value |String |The value of the DNS record. |
|Weight |Integer |The weight of the DNS record. |
|RecordSetID |String |The ID of the record set where the DNS record is located. Only A, AAAA, and CNAME types of DNS records have record sets. |
|Enable |Boolean |Whether the DNS record is enabled. This parameter can have the following values:<br><br><br>* `true`: Enable the DNS record.<br><br>* `false`: Disable the DNS record.<br><br><br> |
|Tags |Array of String |The tag information of the DNS record. If the value of this parameter contains `GTMLock`, it indicates that the DNS record is associated with a GTM instance in BytePlus Global Traffic Management (GTM). |
|Remark |String |Remark of the record. |
|CreatedAt |String |The creation time of the DNS record. |
|UpdatedAt |String |The time when the DNS record was updated after calling this API. |
|Operators |String[] |The account ID that called this API. If this API is called by an IAM account, the value of this parameter is the ID of the IAM account. |


<span id="f8b5d553"></span>
## Example

<span id="c036a92f"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=UpdateRecordStatus
{
  "Enable": false,
  "RecordID": "3170534137672596377"
}
```


<span id="29d31412"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202407010855259E97491DB7E902006CEF",
        "Action": "UpdateRecordStatus",
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
        "Enable": false,
        "Tags": [],
        "Remark": "",
        "CreatedAt": "2024-07-01T08:55:26Z",
        "UpdatedAt": "2024-07-01T08:55:26Z",
        "Operators": [
            "300xxxxx32"
        ]
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
