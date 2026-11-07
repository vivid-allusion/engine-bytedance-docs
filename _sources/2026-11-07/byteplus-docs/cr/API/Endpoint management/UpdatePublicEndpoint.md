---
title: "UpdatePublicEndpoint"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/updatepublicendpoint"
---

Update the public network access information of the Container Registry instance.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For more information, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=UpdatePublicEndpoint&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdatePublicEndpoint |The API name. The current API's name is `UpdatePublicEndpoint`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the Container Registry instance. On the **instance list** page of the [Container Registry console](https://console.byteplus.com/cr), obtain the instance name. |
|Enabled |Boolean |no |true |Indicates whether to enable public network access. Available methods:<br><br><br>* **false**: not enabled<br><br>* **true**: enabled<br><br><br>The default is **false**. |
|ClientToken |String |no |BC028527\-33B9\-4990\-A633\-84E9F9\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=UpdatePublicEndpoint&Version=2022-05-12
{
    "Registry": "registrya",
    "Enabled": true
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
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "UpdateRegistryEndpoint",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are shown in the following table. For public error codes, refer to [public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
|400 |OperationDenied.Status |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current access endpoint status. Please wait for the status transition to complete and try again. |
|400 |OperationDenied.NothingToUpdate |The action has been denied due to nothing to update. |The content specified for update is the same as the current information of the resource, and there are no properties to be updated. |
