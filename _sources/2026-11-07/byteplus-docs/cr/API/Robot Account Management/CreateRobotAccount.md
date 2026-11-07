---
title: "CreateRobotAccount"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/CreateRobotAccount"
---

Creates a robot account.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=CreateRobotAccount&Version=2022\-05\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateRobotAccount |The API name. The current API's name is `CreateRobotAccount`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The instance name where the robot account is located. |
|Username |String |Yes |crrobot@username1 |The name of the robot account, in the format `crrobot@****`. |
|Password |String |no |yourpassword |The password for logging into the robot account. If not provided, a random password will be generated. |
|Description |String |no |Used for cicd |The description of the robot account. |
|Duration |Long |Yes |\-1 |The effective time in days, with a maximum limit of 366. Use `-1` for an indefinite duration. |
|Permissions |Array of [Permission](https://docs.byteplus.com/en/docs/65/51813#permission) |Yes |[{"Resource":"\*","Actions":"CreateRepository"] |The permission scope for the robot account. |


<span id="permission"></span>
### Permission


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Actions |Array of String |Yes |PushRepository |The supported operational permissions:<br><br><br>* CreateRepository: create a container registry.<br><br>* PullRepository: Pull images.<br><br>* PushRepository: Push images. |
|Resource |String |Yes |*  |The resource object on which the operation is performed. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=CreateRobotAccount&Version=2022-05-12
{
    "Registry": "registrya",
    "Username": "crrobot@username1",
    "Duration": -1,
    "Permissions": [
        {
            "Resource": "*",
            "Actions": [
                "PullRepository"
            ]
        }
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Username |String |crrobot@username1 |The name of the robot account. |
|Password |String |password1 |The password for logging into the robot account. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateRobotAccount",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-north-1"
    },
    "Result": {
        "Username": "crrobot@username1",
        "Password": "password1"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface has no specific error codes. For public error codes, please refer to the [Public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes) documentation.
