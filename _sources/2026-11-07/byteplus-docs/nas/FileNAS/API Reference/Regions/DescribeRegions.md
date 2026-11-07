---
title: "DescribeRegions"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/DescribeRegions"
---

Call the DescribeRegions interface to enumerate the region information.

<span id="request-parameters"></span>
## Request parameters

Empty.

<span id="response-parameters"></span>
## Response parameters


|Name |Type |Example |Description |
|---|---|---|---|
|TotalCount |Integer |3 |Total number of regions. |
|Regions |Array of [Region](https://docs.byteplus.com/en/docs/91/24973#region) |\- |Regional information collection. |


<span id="region"></span>
### Region


|Name |Type |Example |Description |
|---|---|---|---|
|Status |String |OnSale |Sale status. The value selection description is as follows:<br><br><br>* `OnSale`: During the sale, you can make new purchases and change instances normally.<br><br>* `UnSold`: Not sold, you can't buy new instances.<br><br>* `SoldOut`: Sold out, you can't buy new instances, existing instances are not affected. |
|RegionId |String |ap\-southeast\-1 |Region ID. |


<span id="sample-request"></span>
## Sample request

```json
POST /?Action=DescribeRegions&Version=2022-01-01 HTTP/1.1
Host: filenas.ap-southeast-1.byteplusapi.com
Authorization: HMAC-SHA256 Credential=AKLTOGJhY2E1NTdkZGFmNDg0Yjk0ZDFiNjE5Y2NjZjI****/20230907/ap-southeast-1/filenas/request, SignedHeaders=host;x-date;x-content-sha256;content-type, Signature=7f1119a75111535b1d6e7929700f22e1474af0fb4fe26c59f5ac5cdba0cc****
Content-Type: application/json; charset=utf-8
X-Content-Sha256: 567112abe45bd6a09504fd244237f14c0ba120491da0d35097afd54d87bd****
X-Date: 20230907T124910Z
```


<span id="sample-response"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DescribeRegions",
        "Region": "ap-southeast-1",
        "Service": "filenas",
        "Version": "2022-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "TotalCount": 3,
        "Regions": [
            {
                "Status": "OnSale",
                "RegionId": "ap-southeast-1"
            }
        ]
    }
}
```
