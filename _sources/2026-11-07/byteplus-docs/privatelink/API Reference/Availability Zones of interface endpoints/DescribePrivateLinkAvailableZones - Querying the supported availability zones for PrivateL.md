---
title: "DescribePrivateLinkAvailableZones - Querying the supported availability zones for PrivateLink"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribePrivateLinkAvailableZones"
---

Use the DescribePrivateLinkAvailableZones API to query the availability zones supported by the PrivateLink service.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribePrivateLinkAvailableZones&serviceCode=privatelink&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribePrivateLinkAvailableZones`

Action to execute. Set the value to **DescribePrivateLinkAvailableZones**.

**Version ** String必选 `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.

## Response parameters

**RequestId ** String`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.

**ZoneIds ** String[]`Example: cn-guangzhou-a`

Availability zones supported by the PrivateLink service.

## Request examples

```json
GET /?Action=DescribePrivateLinkAvailableZones&Version=2020-04-01 HTTP/1.1
 Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribePrivateLinkAvailableZones",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "ZoneIds": [
            "cn-guangzhou-a",
            "cn-guangzhou-b"
        ]
    }
}
```

## Error codes

There are no service\-specific error codes. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).
