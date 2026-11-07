---
title: "DeleteEndpointAclPolicies"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/deleteendpointaclpolicies"
---

Delete an Elastic IP Address allowlist endpoint.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=DeleteEndpointAclPolicies&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteEndpointAclPolicies |The API name. The current API's name is `DeleteEndpointAclPolicies`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the Container Registry instance. On the [Container Registry console](https://console.byteplus.com/cr) **instance list** page, find the instance name. |
|Type |String |Yes |Public |The network type for the allowlist. Currently, only Public is supported. |
|Entries |Array of String |Yes |["192.\*\*\*\*.\*\*\*\*.0/24", "1.\*\*\*\*.\*\*\*\*.0/8", "178.\*\*\*\*.\*\*\*\*.145"] |The list of IP addresses to be added to the allowlist. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=DeleteEndpointAclPolicies&Version=2022-05-12
{
    "Registry": "registrya",
    "Type": "Public",
    "Entries": [
        "192.****.****.0/24",
        "1.****.****.0/8",
        "178.****.****.145"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None

<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74B****",
        "Action": "DeleteEndpointAclPolicies",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface has no specific error codes. For public error codes, please refer to the [Public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes) documentation.
