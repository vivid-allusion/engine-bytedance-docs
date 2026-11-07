---
title: "DescribeZones - Querying the region information"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeZones"
---

Call the DescribeZones API to query the primary\-secondary availability zone mapping for the current region.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeZones&serviceCode=clb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple">String </span><span data-api-tag="require|EbHhBI">必选</span> `Example: DescribeZones`

Action to execute. Set the value to **DescribeZones**.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|1LFBf5">必选</span> `Example: 2020-04-01`

API version. The current version is **2020\-04\-01**.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**MasterZones ** <span data-label="purple">Object[] </span>`Example: -`

List of primary availability zones.


**ZoneId ** <span data-label="purple">String </span>`Example: cn-shanghai-a`

Primary availability zone ID.

When the current region is deployed in a single availability zone, this parameter returns the ID of the availability zone where the CLB instance is deployed.



**SlaveZones ** <span data-label="purple">String[] </span>`Example: ["cn-shanghai-b"]`

The list of secondary availability zones corresponding to this primary availability zone.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeZones&Version=2020-04-01
Host: clb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeZones",
        "Version": "2020-04-01",
        "Service": "clb",
        "Region": "cn-beijing"
    },
    "Result": {
        "MasterZones": [
            {
                "ZoneId": "cn-shanghai-a",
                "SlaveZones": [
                    "cn-shanghai-b"
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Public-error-codes).


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|403 |Forbidden |You are not authorized to perform operations on the specified service. |You do not have permission to perform operations on the specified service. |
|404 |InvalidZone.NotFound |The specified Zone mapping does not exist. |The specified primary\-secondary availability zone relationship does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
