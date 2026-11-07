---
title: "ListRobotAccounts"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/ListRobotAccounts"
---

Lists the robot accounts.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To achieve low latency, it is recommended that you select the corresponding service address based on the region where your resources are located. For details, refer to [service address](https://docs.byteplus.com/en/docs/cr/Service_address).


* Request method: POST

* Request URL: https://cr.cn\-beijing.byteplusapi.com.cn?Action=ListRobotAccounts&Version=2022\-05\-12


<span id=".6LCD6K-V"></span>
## 

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

When calling this API, in addition to the following request parameters, you also need to provide the public request parameters.  See [Public parameters](https://docs.byteplus.com/en/docs/cr/common-parameters) for details.


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListRobotAccounts |The API name. The current API's name is `ListRobotAccounts`. |
|Version |String |Yes |2022\-05\-12 |The API version. The current version of the API is `2022-05-12`. |
|Registry |String |Yes |registrya |The instance name where the robot account is located. |
|Filter |Object of [RobotAccountFilter](https://docs.byteplus.com/en/docs/65/51814#robotaccountfilter) |no | |The search filter for robot accounts. |
|PageNumber |Long |no |2 |The page number, starting from 1, with a default value of 1. |
|PageSize |Long |no |10 |The number of items per page. |


<span id="robotaccountfilter"></span>
### RobotAccountFilter


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Disabled |Boolean |no |true |Indicates whether the account is disabled. |
|Usernames |Array of String |no |["*crrobot@usernam1*","*crrobot@username2*"] |The username filter. Supports fuzzy matching using \*. |
|Descriptions |Array of String |no |["*description*"] |The description filter for robot accounts. Supports fuzzy matching using \*. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```json
POST https://cr.cn-beijing.byteplusapi.com.cn?Action=ListRobotAccounts&Version=2022-05-12
{
    "Registry": "registrya"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TotalCount |Long |20 |The total number of robot accounts listed. |
|PageNumber |Long |2 |The page number. |
|PageSize |Long |10 |The number of items per page. |
|Items |Array of [RobotAccount](https://docs.byteplus.com/en/docs/65/51814#robotaccount) | |The detailed information of robot accounts. |


<span id="robotaccount"></span>
### RobotAccount


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Disabled |Boolean |true |Indicates whether the account is disabled. |
|Username |String |crrobot@username1 |The name of the robot account. |
|ExpiresAt |Long |\-1 |The expiration timestamp. |
|CreateTime |String |2022\-05\-20T13:00:55Z |The creation timestamp. |
|UpdateTime |String |2022\-05\-20T13:00:55Z |The update timestamp. |
|Description |String |descriptionxxxxx |The description of the robot account. |
|Permissions |Array of [Permission](https://docs.byteplus.com/en/docs/65/51814#permission) |[{"Resource":"\*","Actions":"CreateRepository"] |The operational permissions of the robot account. |


<span id="permission"></span>
### Permission


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Actions |Array of String |PushRepository |The supported operational permissions:<br><br><br>* CreateRepository: create a container registry.<br><br>* PullRepository: Pull images.<br><br>* PushRepository: Push images. |
|Resource |String |*  |The resource object on which the operation is performed. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListRobotAccounts",
        "Version": "2022-05-12",
        "Service": "cr",
        "Region": "cn-north-1"
    },
    "Result": {
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 10,
        "Items": [
            {
                "Disabled": true,
                "Username": "crrobot@username1",
                "ExpiresAt": -1,
                "CreateTime": "2022-05-20T13:00:55Z",
                "UpdateTime": "2022-05-20T13:00:55Z",
                "Description": "descriptionxxxxx",
                "Permissions": [
                    {
                        "Actions": [
                            ""
                        ],
                        "Resource": "*"
                    }
                ]
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

This interface has no specific error codes. For public error codes, please refer to the [Public error codes](https://docs.byteplus.com/en/docs/cr/common-error-codes) documentation.
