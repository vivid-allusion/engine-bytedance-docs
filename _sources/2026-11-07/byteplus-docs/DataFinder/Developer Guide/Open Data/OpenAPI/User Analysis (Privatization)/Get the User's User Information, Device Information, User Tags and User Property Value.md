---
title: "Get the User's User Information, Device Information, User Tags and User Property Value"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Get_the_Users_User_Information_Device_Information_User_Tags_and_User_Property_Value"
---

<span id="fdbee0b4"></span>
## Request description

**Path**:openapi/v1/{app_id}/behaviors/profiles

**Method**: POST

**Content\-type**: application/json

<span id="3656ab39"></span>
## Request parameters

**Body**: Refer to public parameter description

<span id="975f6834"></span>
## Return parameters

**Response**:

```json
{
    "code": 200,
    "message": "success",
    "data": {
        "user_info": {
            "register_time": 1670310396,
            "first_event_time": 1670310396,
            "last_use": "2023-01-18",
            "city": "",
            "ssid": "32cee072-0c1d-4bb4-8a24-31b605dfe673",
            "user_unique_id": "data_quality_report_38",
            "id_info": {
                "ssid": "32cee072-0c1d-4bb4-8a24-31b605dfe673",
                "user_unique_id": "data_quality_report_38",
                "device_id": ""
            }
        },
        "device_info": {
            "device_model": "",
            "app_version": "",
            ....
        },
        "custom_user_props": {
            "profile_1": "profile_value",
            ...
        },
        "user_tag_props"： {
            "tag_1": "tag value",
            ...
        }
}
```


Field meaning description


|**Parameter** |**Type** |**Sample value** |**Describe** |
|---|---|---|---|
|user_info |object |See the return example below |User information, including registration time, first event time, recent usage time, city where the latest IP is located, ID information, etc.<br><br>If the above information does not exist, it will be filled with null or empty strings. |
|device_info |object ||Device information, including device model, operating system, application version, application channel, Mini Program application version, device brand, browser, resolution, language, device price, etc.<br><br><br>* In the SaaS version, device information is extracted only from app_launch or predefine_pageview events.<br><br>   In the privatized version, the device information is only extracted from the user's latest event. If the user's latest event does not report the device model, the interface will not return it.<br><br>* If the above information does not exist, it will be filled with null or empty string |
|custom_user_props |object ||User attributes, containing the latest values of user attributes of last_value types reported by the customer via dataprofile or sdk. |
|user_tag_props |object ||User label, including all label values corresponding to the user |


<span id="f272f512"></span>
## Request example

`Bc`for the creation of RangersClient, its initialization please refer to [Instructions for use](https://docs.byteplus.com/docs/undefined/6a4ce4148a55b50525119a52#b9a8ccc7) the language SDK provides a similar interface.

Call (Python):

```python
body={
    "query_id": "test_1",
    "query_type": "user_unique_id"
}
res = bc.data_finder('/openapi/v1/12345/behaviors/profiles', body=body)
print(res.content)
```


<span id="44a27f09"></span>
## Back to example

Return result:

```python
{
    "code": 200,
    "message": "success",
    "data": {
        "user_info": {
            "register_time": 1670315402,
            "first_event_time": 1670315402,
            "last_use": "2023-01-28",
            "city": "",
            "ssid": "172020d7-2261-47d8-ae0d-5721d4445f79",
            "user_unique_id": "test_1",
            "id_info": {
                "ssid": "172020d7-2261-47d8-ae0d-5721d4445f79",
                "user_unique_id": "test_1",
                "device_id": ""
            }
        },
        "device_info": {
            "device_model": "",
            "app_version": "",
            "app_channel": "",
            "browser": "",
            "resolution": "",
            "language": "",
            "device_price": "",
            "device_brand": "",
            "os": "",
            "platform_version": ""
        },
        "custom_user_props": {
            "profile_name_a": "a",
        },
        "user_tag_props": {
            "66 (tag_66)": "2022-12-14 00:00:00.000",
            "77 (tag_77)": 7
        }
    }
}
```
