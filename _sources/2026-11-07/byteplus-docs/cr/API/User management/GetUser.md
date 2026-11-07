---
title: "GetUser"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/setuser"
---

Query the user information of the Container Registry.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=GetUser&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetUser |The API name. The current API's name is `GetUser`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the target Container Registry instance for querying user information. On the **instance list** page of the [Container Registry console](https://console.byteplus.com/cr), obtain the instance name. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=GetUser&Version=2022-05-12
{
    "Registry": "registrya"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Username |String |user@12345 |The username for logging into the Container Registry instance. |
|Status |String |Inactive |User status:<br><br><br>* **Active**: Indicates the user has set a permanent login password for the Container Registry instance.<br><br>* **Inactive**: Indicates the user has not set a permanent login password for the Container Registry instance. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "540CFF28-407A-40B5-B6A5-74Bxxxxxxxxx",
        "Action": "GetUser",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {
        "Status": "Active",
        "Username": "user@12345"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are shown in the table below. For public error codes, please refer to [public error code](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
