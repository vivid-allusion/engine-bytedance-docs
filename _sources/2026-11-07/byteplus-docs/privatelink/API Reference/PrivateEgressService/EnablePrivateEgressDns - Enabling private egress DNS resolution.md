---
title: "EnablePrivateEgressDns - Enabling private egress DNS resolution"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/EnablePrivateEgressDns"
---

Call the EnablePrivateEgressDns API to enable DNS resolution for the private network egress.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=EnablePrivateEgressDns&serviceCode=privatelink&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|i2UKDf">必选</span> `Example: EnablePrivateEgressDns`

The action to perform. Value: **EnablePrivateEgressDns**.



**Version ** <span data-label="purple"> string </span><span data-api-tag="require|wa1fTF">必选</span> `Example: 2020-04-01`

The API version. The current version is **2020\-04\-01**.



**PrivateEgressId ** <span data-label="purple"> String  </span><span data-api-tag="require|_a8H-b">必选</span> `Example: pre-p6q7r8s9t0****`

The ID of the private network egress.



**DnsServers.N.Ip ** <span data-label="purple"> String  </span><span data-api-tag="require|nY0PMv">必选</span> `Example: 192.168.1.11`

The IP address of the external DNS server.


* N represents the sequence number of an IP address. Up to 10 IPs can be specified.

* You cannot configure the BytePlus DNS server addresses (100.96.0.2 and 100.96.0.3).

* Separate multiple IPs with ampersands (&).



**DnsServers.N.Port** <span data-label="purple">Integer</span> `optional` `Example: 53`

The port of the external DNS server.


* N represents the sequence number of an IP port.

* If not specified, the value defaults to 53.



**Domains.N ** <span data-label="purple"> String  </span><span data-api-tag="require|nWAkj0">必选</span> `Example: example.com`

The forwarding domain. The domain that need to be resolved through an external DNS server.


* N represents the sequence number of a domain. Up to 500 domains can be specified.

* Separate multiple domains with ampersands (&).

* Domains not specified here are still resolved through the BytePlus DNS servers.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**AsyncTaskId ** <span data-label="purple"> String  </span>`Example: asynctask-13f0odozfrdvk3n6nu41l****`

The ID of the asynchronous task.



**RequestId ** <span data-label="purple"> String  </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28D****`

The request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET /?Action=EnablePrivateEgressDns&Version=2020-04-01&PrivateEgressId=pre-p6q7r8s9t0****&DnsServers.1.Ip=192.168.1.11&DnsServers.1.Port=53&Domains.1=example.com
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
        "Action": "EnablePrivateEgressDns",
        "Version": "2020-04-01",
        "Service": "privatelink",
        "Region": "cn-guangzhou"
    },
    "Result": {
        "AsyncTaskId": "asynctask-13f0odozfrdvk3n6nu41l****",
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

This API has no service\-specific error codes. For more details, see [Common error codes](https://docs.byteplus.com/en/docs/privatelink/Public-error-codes).
