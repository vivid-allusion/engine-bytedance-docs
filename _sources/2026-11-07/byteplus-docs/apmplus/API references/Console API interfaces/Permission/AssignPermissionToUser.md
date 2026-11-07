---
title: "AssignPermissionToUser"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/AssignPermissionToUser"
---

Assign permissions to specified users.

<span id=".5o6l5Y-j6K-05piO"></span>
## API description

The IAM user has been granted administrator or member permissions for this application. For details, see [Permission management](https://docs.byteplus.com/en/docs/apmplus/Client_permissions_management).

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=AssignPermissionToUser&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |AssignPermissionToUser |The API name. The current API name is `AssignPermissionToUser`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|users |Array of String |Yes |["test_user"] |List of IAM users to be assigned permissions. |
|aid |Array of Integer |No |[12345] |List of application IDs for permission assignment. \-1 indicates all. |
|service_keys |Array of String |No |["app_monitor"] |List of services for permission assignment. It is not required when the assigned role is administrator. |
|role_type |Integer |Yes |1 |User role to be assigned.<br><br><br>* 1: Regular member<br><br>* 2: Administrator. The administrator has permissions for all services and all applications under the root user. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=AssignPermissionToUser&Version=2022-10-12
{
    "users": [
        "test_user"
    ],
    "role_type": 1,
    "aid": [
        12345
    ],
    "service_keys": [
        "app_monitor"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|error_msg |String |"" |Error message. It is empty if the request succeeds. |
|error_no |Integer |0 |Error code. 0 indicates success. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "error_no": 0,
    "error_msg": ""
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
