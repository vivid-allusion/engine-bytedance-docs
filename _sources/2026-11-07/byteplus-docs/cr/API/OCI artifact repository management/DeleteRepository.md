---
title: "DeleteRepository"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/deleterepository"
---

Deletes an OCI artifact repository from a specified namespace.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

When deleting an OCI artifact repository, all OCI artifact (image, Chart) versions within it will be deleted without any validation to check if there are existing OCI artifact versions. Please call this interface with caution.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=DeleteRepository&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteRepository |The API name. The current API's name is `DeleteRepository`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the Container Registry instance to which the specified namespace belongs. On the **Instance List** page of the [Container Registry Console](https://console.byteplus.com/cr), obtain the instance name. |
|Namespace |String |Yes |library |The name of the specified namespace. On the [Container Registry Console](https://console.byteplus.com/cr) **namespace** page of the target instance, obtain the namespace name. |
|Name |String |Yes |repositorya |The name of the OCI artifact repository to be deleted. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=DeleteRepository&Version=2022-05-12
{
    "Registry": "registrya",
    "Namespace": "library",
    "Name": "repositorya"
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
        "Action": "DeleteRepository",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are shown in the table below. For public error codes, refer to [public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
