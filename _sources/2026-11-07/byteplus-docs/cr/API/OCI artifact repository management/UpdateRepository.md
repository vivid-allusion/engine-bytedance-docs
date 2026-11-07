---
title: "UpdateRepository"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/updaterepository"
---

Update the information of an OCI artifact repository under a specified namespace.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For more information, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=UpdateRepository&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateRepository |The API name. The current API's name is `UpdateRepository`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the Container Registry instance to which the specified namespace belongs. On the **Instance List** page of the [Container Registry Console](https://console.byteplus.com/cr), obtain the instance name. |
|Namespace |String |Yes |library |The name of the specified namespace. On the **namespace** page of the target instance in the [Container Registry console](https://console.byteplus.com/cr), obtain the namespace name. |
|Name |String |Yes |repositorya |The name of the OCI artifact repository. The name must be unique within the same namespace. It supports lowercase English letters, numbers, and separators (the separators can be one `.`or `/`, one or more `-`, one or two `_`, and the separators can not appear at the beginning or end, nor can they appear consecutively), with a length limit of 2 to 128 characters. |
|Description |String |no |This is a description |The description information of the OCI artifact repository. The length should not exceed 300 characters. |
|AccessLevel |String |no |Private |The type of the OCI artifact repository.<br><br><br>* **Public**: IAM users with full read\-write permissions can push or pull images, while other users can pull images anonymously.<br><br>* **Private**: IAM users with full read\-write permissions can push or pull images, while IAM users with read\-only permissions can pull images. The default value is **Private**. |
|ClientToken |String |no |dd1fc09f\-17ff\-4cf5\-929d\-643e36\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=UpdateRepository&Version=2022-05-12
{
    "Registry": "registrya",
    "Namespace": "library",
    "Name": "repositorya",
    "AccessLevel": "Private"
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
        "Action": "UpdateRepository",
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
|400 |OperationDenied.NothingToUpdate |The action has been denied due to nothing to update. |The content specified for update is the same as the current information of the resource, and there are no properties to be updated. |
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
