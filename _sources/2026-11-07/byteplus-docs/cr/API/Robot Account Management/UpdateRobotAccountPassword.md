---
title: "UpdateRobotAccountPassword"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/UpdateRobotAccountPassword"
---

Updates the password of a robot account.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=UpdateRobotAccountPassword&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateRobotAccountPassword |The API name. The current API's name is `UpdateRobotAccountPassword`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The instance where the robot account is located. |
|Username |String |Yes |crrobot@username |The name of the robot account. |
|Password |String |no |yourpassword |The login password of the robot account. Required when `random` is `false`. |
|Random |Boolean |Yes |false |Indicates whether to automatically generate a random password. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=UpdateRobotAccountPassword&Version=2022-05-12
{
    "Registry": "registrya",
    "Username": "username",
    "Random": true
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Username |String |crrobot@username |The name of the robot account. |
|Password |String |password2 |The password of the robot account. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateRobotAccountPassword",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-north-1"
    },
    "Result": {
        "Username": "crrobot@username",
        "Password": "password2"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface has no specific error codes. For public error codes, please refer to the [Public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes) documentation.
