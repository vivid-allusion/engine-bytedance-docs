---
title: "UpdateRobotAccount"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/UpdateRobotAccount"
---

Updates a robot account.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request address: https://cr.cn\-beijing.byteplusapi.com.cn?Action=UpdateRobotAccount&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## 

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |UpdateRobotAccount |The API name. The current API's name is `UpdateRobotAccount`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The name of the instance where the robot account is located. |
|Username |String |Yes |crrobot@username |The name of the robot account. |
|Description |String |no |descriptionxxxxxx |The description of the robot account. |
|Disabled |Boolean |no |true |Indicates whether the account is disabled. |
|Duration |Long |no |40 |The effective time in days, with a maximum limit of 366. Use \-1 for an indefinite duration. |
|Permissions |Array of [Permission](https://docs.byteplus.com/en/docs/65/51815#permission) |no |[{"Resource":"\*","Actions":"CreateRepository"] |The operational permissions of the robot account. |


<span id="permission"></span>
### Permission


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Actions |Array of String |Yes |PushRepository |The supported operational permissions:<br><br><br>* CreateRepository: create a container registry.<br><br>* PullRepository: Pull images.<br><br>* PushRepository: Push images. |
|Resource |String |Yes |*  |The resource object on which the operation is performed. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=UpdateRobotAccount&Version=2022-05-12
{
    "Registry": "registrya",
    "Username": "crrobot@username",
    "Description": "descriptionxxxxxx",
    "Disabled": true,
    "Duration": 40,
    "Permissions": [
        {
            "Actions": [
                "PushRepository"
            ],
            "Resource": "*"
        }
    ]
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
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateRobotAccount",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-north-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface has no specific error codes. For public error codes, please refer to the [Public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes) documentation.
