---
title: "CreateNamespace"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/createnamespace"
---

Creates a namespace under a specified Container Registry instance.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

A single Standard Edition instance can create up to 50 namespaces.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For more information, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=CreateNamespace&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateNamespace |The API name. The current API's name is `CreateNamespace`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the specified Container Registry instance. Obtain via [ListRegistries](https://docs.byteplus.com/en/docs/cr/listregistries) or from the [Container Registry console](https://console.byteplus.com/cr) **Instance list** page. |
|Name |String |Yes |library |The name of the namespace. It supports lowercase English letters, numbers, periods (.), hyphens (\-), and underscores (_). Punctuation marks can not appear at the beginning or end, nor can they be entered consecutively. The length is limited to 2 to 90 characters.<br><br><br>* **For Standard Edition instances**: The name must be unique under the same Container Registry instance.<br><br>* For trial instances: The namespace name must be unique across all BytePlus root users within the same region. If the namespace name you set is already in use, please try another name or [purchase a Standard Edition instance](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance). |
|ClientToken |String |no |7fb07cc4\-dc14\-11ec\-a7ae\-af0220\*\*\*\*\*\* |A string used to ensure the idempotency of the request. This string is passed in by the caller and must be unique across different requests. ClientToken is case\-sensitive and can consist of 64 ASCII characters at most. |
|Project |String |no |projecta |The name of the project to which the namespace belongs. The parameter value is case\-sensitive and must not exceed 64 characters. When the parameter is empty, the namespace is associated with the default `default` project. |
|RepositoryDefaultAccessLevel |String |no |Public |The default public access level of the newly created OCI artifact repository under the namespace. The default value is Private. The public attribute can be changed subsequently.<br><br><br>* Public: Public, accessible directly without an access key.<br><br>* Private: Private, accessible only after entering an access key. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=CreateNamespace&Version=2022-05-12
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
        "RequestId": "540CFF28-407A-40B5-B6A5-74B****",
        "Action": "CreateNamespace",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are listed in the table below. For public error codes, refer to [Public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
|400 |QuotaExceeded.Namespace |The quota of cr namespace is exceeded. |The number of namespaces has reached the quota limit. It is recommended to clean up unused namespaces and try again.  |
