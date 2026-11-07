---
title: "SetUser"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/getuser"
---

Sets a user for the Container Registry, which refers to the user logging into the Container Registry instance.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

Currently, this interface only supports setting the user's login password.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=SetUser&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |SetUser |The API name. The current API's name is `SetUser`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the target Container Registry instance for which you want to set the login user. On the **Instance List** page of the [Container Registry Console](https://console.byteplus.com/cr), obtain the instance name. |
|Password |String |Yes |UGFzc3dvcmQxMj\*\*\*\*\*\* |The new Container Registry login password after Base64 encoding. It must be a valid Base64 string. When compiling with the `echo` command, you need to use `echo -n` to remove the trailing newline character. The length of the original password (before Base64 encoding) is limited to 8\-20 characters. It must contain uppercase and lowercase English letters, and at least one digit or punctuation mark. The supported punctuation marks are as follows:<br><br>`~!@#$%^&*()-_=+\\|[]:,<.>/;` |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=SetUser&Version=2022-05-12
{
    "Registry": "registrya",
    "Password": "UGFzc3dvcmQx****"
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
        "Action": "SetUser",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

The error codes for this interface are listed in the table below. For public error codes, refer to [public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes).


|**HTTP Status Code** |**Error code** |**Error Message** |**Descriptions** |
|---|---|---|---|
|400 |OperationDenied.RegistryStatus |The action has been denied due to wrong status %s. |The specified operation is not allowed under the current instance status. Please wait for the status transition to complete and try again. |
