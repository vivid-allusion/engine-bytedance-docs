---
title: "DeleteTags"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/deletetags"
---

Deletes the OCI artifact (image, Helm Chart) versions, with support for batch deletion.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=DeleteTags&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |DeleteTags |The API name. The current API's name is `DeleteTags`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the Container Registry instance where the OCI artifacts are located. On the **Instance List** page of the [Container Registry Console](https://console.byteplus.com/cr), obtain the instance name. |
|Namespace |String |Yes |library |The name of the namespace where the OCI artifacts are located. |
|Repository |String |Yes |repositorya |The name of the OCI artifact repository where the OCI artifacts are located. |
|Names |Array of String |Yes |["v1","v2"] |The list of OCI artifact versions. Multiple versions can deleted in batch. Currently, a maximum of 20 canary versions can be passed in a single request. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=DeleteTags&Version=2022-05-12
{
    "Registry": "registrya",
    "Namespace": "library",
    "Repository": "repositorya",
    "Names": [
        "v1",
        "v2"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Successes |Array of [Success](https://docs.byteplus.com/en/docs/65/26083#success) |[{"Name":"tag1"}] |The versions that were successfully deleted. |
|Failures |Array of [Failure](https://docs.byteplus.com/en/docs/65/26083#failure) |[{"Name":"tag2", "Reason":""xxx"}] |The versions that failed to be deleted. |


<span id="success"></span>
### Success


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |v1 |Tag name. |


<span id="failure"></span>
### Failure


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Name |String |v1 |Tag name. |
|Reason |String |tag v1 not exist |The reason for the deletion failure. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74B****",
        "Action": "DeleteTags",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {
        "Successes": [
            {
                "Name": "v1"
            }
        ],
        "Failures": [
            {
                "Name": "v2",
                "Reason": "****"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are listed in the table below. For public error codes, refer to [public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
