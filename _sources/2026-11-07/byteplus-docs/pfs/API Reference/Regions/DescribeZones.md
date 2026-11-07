---
title: "DescribeZones"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/DescribeZones"
---

Call the DescribeZones interface to query the list of available zones under the Region specified by PFS.

<span id="request-parameters"></span>
## Request parameters


|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|RegionId |String |No |ap\-southeast\-1 |Specifies the geo ID for the query. |


<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |2 |Number of Availability Zones. |
|Zones |Array of [ZoneInfo](https://docs.byteplus.com/en/docs/92/25011#zoneinfo) |See the return example for details |Availability zone details. |


<span id="zoneinfo"></span>
### ZoneInfo


|Name |Type |Example |Description |
|---|---|---|---|
|ZoneId |String |ap\-southeast\-1 |Area ID. |
|RegionId |String |ap\-southeast\-1a |Availability zone ID. |
|SaleInfos |Array of [SaleInfo](https://docs.byteplus.com/en/docs/92/25011#saleinfo) |See the return example for details |Availability zone sales information. |


<span id="saleinfo"></span>
### SaleInfo


|Name |Type |Example |Description |
|---|---|---|---|
|Status |String |OnSale |Sales status, value selection description is as follows:<br><br><br>* `OnSale`: During the sale, you can make new purchases and change instances normally.<br><br>* `UnSold`: Not sold, you can't buy new instances.<br><br>* `SoldOut`: Sold out, you can't buy new instances, existing instances are not affected. |
|ZoneId |String |ap\-southeast\-1a |Availability zone ID. |
|RegionId |String |ap\-southeast\-1 |Area ID. |
|StoreType |String |Advance_100 |File system specification, value selection description is as follows:<br><br><br>* Advance_100: 100MB/s/TiB |
|ProtocolType |String |VePFS |Protocol type, defaults to`VePFS`. |
|FileSystemType |String |VePFS |File system type, defaults to`VePFS`. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeZones&Version=2022-01-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/vepfs/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
{
    "RegionId": "ap-southeast-1"
}
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeZones",
        "Region": "ap-southeast-1",
        "Service": "vepfs",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "TotalCount": 2,
        "Zones": [
            {
                "ZoneId": "ap-southeast-1",
                "RegionId": "ap-southeast-1a",
                "SaleInfos": [
                    {
                        "Status": "OnSale",
                        "ZoneId": "ap-southeast-1a",
                        "RegionId": "ap-southeast-1",
                        "StoreType": "Advance_100",
                        "ProtocolType": "VePFS",
                        "FileSystemType": "VePFS",
                        "ProtocolServiceType": "Cache_Type1"
                    }
                ]
            }
        ]
    }
}
```
