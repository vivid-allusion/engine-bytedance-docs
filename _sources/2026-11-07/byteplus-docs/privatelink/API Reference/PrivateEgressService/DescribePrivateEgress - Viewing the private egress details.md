---
title: "DescribePrivateEgress - Viewing the private egress details"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/DescribePrivateEgress"
---

Call the DescribePrivateEgress API to view details of the private network egress.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribePrivateEgress&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|Xo_Bpi">必选</span> `Example: DescribePrivateEgress`

The action to perform. Value: **DescribePrivateEgress**.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|JOHMvx">必选</span>`Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**PrivateEgressId ** <span data-label="purple"> String  </span><span data-api-tag="require|pN5ID3">必选</span>`Example: pre-p6q7r8s9t0****`

The ID of the private network egress.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**AccessLogStatus ** <span data-label="purple"> String </span>`Example: Enabled`

The access log status of the private network egress.


* Enabled

* Disabled



**AsyncTaskId ** <span data-label="purple"> String </span>`Example: asynctask-13f0odozfrdvk3n6nu41l****`

The ID of the asynchronous task.



**CreateTime ** <span data-label="purple"> String </span>`Example: 2026-08-18 15:19:00`

The time when the private network egress is created.



**Description ** <span data-label="purple"> String </span>`Example: Private-Egress-example`

The description of the private network egress.



**DnsBlockRuleStatus ** <span data-label="purple"> String </span>`Example: Disabled`

The DNS status of the private network egress.


* Disabled

* Enabling

* Enabled

* Disabling

* Suspended

* Pending



**DnsServers ** <span data-label="purple"> Object[]  </span>`Example: --`

The information about the DNS server.


**Ip ** <span data-label="purple"> String  </span>`Example: 192.168.1.11`

The IP address of the DNS server.



**Port ** <span data-label="purple"> Integer </span>`Example: 53`

The port of the DNS server.




**DnsStatus ** <span data-label="purple"> String  </span>`Example: Disabled`

The DNS status of the private network egress.


* Disabled

* Enabling

* Enabled

* Disabling

* Suspended

* Pending



**Domains ** <span data-label="purple"> String[]  </span>`Example: ["test.com"]`

The domain list.



**Name ** <span data-label="purple"> String  </span>`Example: Private-Egress-example`

The name of the private network egress.



**NetworkAccessPolicyId ** <span data-label="purple"> String  </span>`Example: pnap-2iqtovxg6ftvk3snftvgd****`

The network access policy ID of the private network egress.



**PrivateEgressId ** <span data-label="purple"> String </span>`Example: pre-p6q7r8s9t0****`

The ID of the private network egress.



**RequestId ** <span data-label="purple"> String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

The request ID.



**SpaceNetworkId ** <span data-label="purple">String</span> `Example: csn-3hxxy2a53tce81wincnyu****`

The space network ID.



**Status ** <span data-label="purple"> String </span>`Example: Enabled`

The status of the private network egress.


* Creating

* Pending

* Enabled

* Disabled



**UpdateTime ** <span data-label="purple"> String  </span>`Example: 2026-08-18 15:19:00`

The time when the private network egress is updated.



**WebAccessPolicyId ** <span data-label="purple"> String  </span>`Example: pwap-3iddkkpstr7cw3snftvmf****`

The Web access policy ID of the private network egress.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET /?Action=DescribePrivateEgress&Version=2020-04-01&PrivateEgressId=pre-p6q7r8s9t0****
Host: privatelink.cn-guangzhou.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-guangzhou/privatelink/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribePrivateEgress",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "AccessLogStatus": "Enabled",
        "AsyncTaskId": "asynctask-13f0odozfrdvk3n6nu41l****",
        "CreateTime": "2026-08-18 15:19:00",
        "Description": "Private-Egress-example",
        "DnsBlockRuleStatus": "Disabled",
        "DnsServers": [
            {
                "Ip": "192.168.1.11",
                "Port": 53
            }
        ],
        "DnsStatus": "Disabled",
        "Domains": [
            "test.com"
        ],
        "Name": "Private-Egress-example",
        "NetworkAccessPolicyId": "pnap-2iqtovxg6ftvk3snftvgd****",
        "PrivateEgressId": "pre-p6q7r8s9t0****",
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****",
        "SpaceNetworkId": "csn-3hxxy2a53tce81wincnyu****",
        "Status": "Enabled",
        "UpdateTime": "2026-08-18 15:19:00",
        "WebAccessPolicyId": "pwap-3iddkkpstr7cw3snftvmf****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This API has no service\-specific error codes. For more details, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).
