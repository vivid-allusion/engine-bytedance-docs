---
title: "GetPublicEndpoint"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/getpublicendpoint"
---

Obtain the public network access information of the Container Registry instance.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=GetPublicEndpoint&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetPublicEndpoint |The API name. The current API's name is `GetPublicEndpoint`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the Container Registry instance. On the **Instance List** page of the [Container Registry Console](https://console.byteplus.com/cr), get the instance name. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=GetPublicEndpoint&Version=2022-05-12
{
    "Registry": "registrya"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Registry |String |registrya |The name of the Container Registry instance. |
|Enabled |Boolean |true |Indicates whether public network access is enabled. Possible parameter values:<br><br><br>* **false**: not enabled<br><br>* **true**: enabled |
|AclPolicies |Array of [AclPolicy](https://docs.byteplus.com/en/docs/65/26088#aclpolicy) |["192.168.1.0/24"] |The list of public network IP allowlists. |
|Status |String |Enabled |The current status of the public network access. Possible parameter values:<br><br><br>* **Enabling**: turning on<br><br>* **Enabled**: turned on<br><br>* **Disabling**: turning off<br><br>* **Updating**: being updated<br><br>* **Failed**: failed<br><br>* **Disabled**: turned off |


<span id="aclpolicy"></span>
### AclPolicy


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Entry |String |192.168.1.0/24 |The IP entry address. |
|Description |String |xxx |The IP entry description. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "GetPublicEndpoint",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {
        "Registry": "registrya",
        "Enabled": true,
        "Status": "Enabled"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this API are listed in the table below. For public error codes, refer to [public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
