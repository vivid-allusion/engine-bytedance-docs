---
title: "DeleteNamespace"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/deletenamespace"
---

Deletes a namespace under a specified Container Registry instance.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

Before deleting a namespace, call [DeleteRepository](https://docs.byteplus.com/en/docs/cr/deleterepository) to delete the OCI artifact repositories under the target namespace.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=DeleteNamespace&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteNamespace |The API name. The current API's name is `DeleteNamespace`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the Container Registry instance to which the namespace to be deleted belongs. On the [Container Registry Console](https://console.byteplus.com/cr) **Instance List** page, obtain the instance name. |
|Name |String |Yes |library |The name of the namespace to be deleted. On the [Container Registry Console](https://console.byteplus.com/cr) namespace page of the target instance, obtain the namespace name. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=DeleteNamespace&Version=2022-05-12
{
    "Registry": "registrya",
    "Name": "library"
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
        "Action": "DeleteNamespace",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are listed in the following table. For additional public error codes, refer to [public error code](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
|400 |NotEmpty.Namespace |Delete namespace is forbidden due to repository exist. |There are uncleaned OCI artifacts under the namespace. Please delete all OCI artifacts under the namespace first and then try again. |
