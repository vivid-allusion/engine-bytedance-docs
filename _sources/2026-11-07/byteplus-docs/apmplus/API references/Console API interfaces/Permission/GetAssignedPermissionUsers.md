---
title: "GetAssignedPermissionUsers"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAssignedPermissionUsers"
---

Get the list of users with assigned permissions.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

The IAM user has been granted administrator or member permissions for this application. For details, see [Permission Management](https://docs.byteplus.com/en/docs/apmplus/Client_permissions_management).

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: GET

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAssignedPermissionUsers&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAssignedPermissionUsers |The API name. The current API name is `GetAssignedPermissionUsers`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAssignedPermissionUsers&Version=2022-10-12
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |"" |Error message. It is empty if the request succeeds. |
|error_no |Integer |0 |Error code. It is 0 if the request succeeds. |
|data |Array of [UserListItem](https://docs.byteplus.com/en/docs/299/67862#userlistitem) |\- |List of users with assigned permissions. |


<span id="userlistitem"></span>
### UserListItem


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|user_id |Long |12345 |User ID. |
|user_name |String |user_name |Username. |
|apps |Array of [KeyLabel](https://docs.byteplus.com/en/docs/299/67862#keylabel) |\- |List of applications with read and write permissions. |
|services |Array of [KeyLabel](https://docs.byteplus.com/en/docs/299/67862#keylabel) |\- |List of services with read and write permissions. |
|create_time |Long |1642562396 |Creation time. |
|email |String |test_user@test.com |IAM user email. |
|phone |String |151\*\*\*\*\*\* |User phone number. |
|role_type |Integer |1，2 |User role.<br><br><br>* 1: Member<br><br>* 2: Administrator |


<span id="keylabel"></span>
### KeyLabel


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |sub_user_key |IAM user key. |
|label |String |sub_user_name |IAM username. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "data": [
        {
            "user_id": [12345],
            "create_time": 1642562396,
            "phone": "151******",
            "role_type": 1,
            "services": [
                {
                    "key": "sub_user_key",
                    "label": "sub_user_name"
                }
            ],
            "user_name": "user_name",
            "display_name": "",
            "apps": [
                {
                    "label": "12",
                    "key": "testapp"
                }
            ],
            "email": "test_user@test.com"
        }
    ],
    "error_no": 0,
    "error_msg": ""
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
