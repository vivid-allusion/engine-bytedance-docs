---
title: "GetAppList"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/GetAppList"
---

Get the application list.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

RUM is deployed across multiple regions worldwide to provide more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/apmplus/service_address) topic to choose the most suitable access point based on your business location.


* Request method: POST

* Request URL: https://apmplus\-openapi.cn\-beijing.byteplusapi.com.cn?Action=GetAppList&Version=2022\-10\-12


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some public parameters. For details, see [Public parameters](https://docs.byteplus.com/en/docs/apmplus/Public_parameters).


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetAppList |The API name. The current API name is `GetAppList`. |
|Version |String |Yes |2022\-10\-12 |The API version. The current API version is `2022-10-12`. |
|aids |Array of Long |No |[] |All apps of the user are queried if not passed. |
|app_name |String |No |app_test |Fuzzy search by app_name. It can be omitted. |
|page_no |Integer |Yes |1 |Page number. |
|page_size |Integer |Yes |10 |Number of items per page. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://apmplus-openapi.cn-beijing.byteplusapi.com.cn?Action=GetAppList&Version=2022-10-12
{
    "page_no": 1,
    "page_size": 10,
    "aids": [],
    "app_name": "app_test"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|data |Object of [ListAppData](https://docs.byteplus.com/en/docs/299/67854#listappdata) |\- |Application list. |
|error_msg |String |"" |Error message. It is empty if the request succeeds. |
|error_no |Integer |0 |Error code. It is 0 if the request succeeds. |


<span id="listappdata"></span>
### ListAppData


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|total |Integer |10 |Total number of applications. |
|result |Array of [App](https://docs.byteplus.com/en/docs/299/67854#app) |\- |Application list. |
|permission_service_keys |Array of String |[app_monitor] |Services activated for the application. |


<span id="app"></span>
### App


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|aid |Long |123456 |Application ID. |
|app_name |String |test_APMPlus |Application Chinese name. |
|app_en_name |String |test_apmplus |Application English name. |
|icon_url |String |\- |icon url。 |
|app_token |String |\- |Returns the token created earliest by default. It is empty if none exists. |
|create_time |Integer |1666077679 |Application creation time. |
|accessable_services_map |JSON Map |\- |Services activated for this application. They are grouped by service_key. Data after multiple activation requirements. |


<span id="accessableservicesmap"></span>
### AccessableServicesMap


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|key |String |app_monitor |Services activated for this application. |
|value |Array of [ServiceInstance](https://docs.byteplus.com/en/docs/299/67854#serviceinstance) |test |Value corresponding to the product. |


<span id="serviceinstance"></span>
### ServiceInstance


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|service_key |String |app_monitor |Service type. |
|aid |Long |123456 |Application ID. |
|instance_status |String |expired |Service instance status.<br><br><br>* normal: Normal<br><br>* overrange: Overrun<br><br>* expired: Expiration<br><br>* closed: Disabled |
|pay_order_num |String |3252617\*\*\*\*\*\*\* |Payment order number. |
|preorder_nums |String |1234567\*\*\*\*\*\*\* |Configuration order number. |
|create_time |Long |1666077679 |Service creation time. |
|expire_time |Long |1666077679 |Service expiration time. |
|created_by |String |test_user |Service creator. |
|amount |Long |123 |Used event quota. |
|total |Long |12345 |Total purchase event count. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "error_no": 0,
    "error_msg": "",
    "data": {
        "result": [
            {
                "icon_url": "",
                "id": 1122334,
                "app_type": "",
                "app_key": "",
                "aid": 123456,
                "app_name": "test_apmplus",
                "app_en_name": "test_apmplus",
                "create_time": 1666077679
            }
        ],
        "total": 10,
        "permission_service_keys": "[app_monitor]"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

No error codes are specific to this API. If the API call returns an error code, refer to [Public error codes](https://docs.byteplus.com/en/docs/apmplus/Public_error_codes) for troubleshooting.
